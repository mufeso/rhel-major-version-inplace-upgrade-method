# The stages, one by one

The method is an automation run (in practice an Ansible playbook) that carries each server through
the whole upgrade, from beginning to end. Between stages there is a **gate**: a server only moves to
the next stage when the current one finished cleanly. If a gate fails, the run stops for that server
and reports why, in plain terms.

The work is designed around the **change window**: a scheduled period, agreed with the business and
normally outside business hours, when the applications on a server can tolerate an outage.
Everything that can be done safely without touching the server is done before the window; the work
inside the window is automated so that as many servers as possible finish within it.

<p align="center">
  <img src="../images/upgrade-stages.svg" alt="The seven stages with a gate between each: pre-flight before the change window; recovery point, pre-upgrade with remediation, upgrade, patching, hardening and handoff inside the window; a separate rollback restores the recovery point." width="100%">
</p>

---

## 1. Pre-flight validation (read-only)

**When:** days or even weeks before the change window.

**What it checks**, before anything is changed:

- package and repository consistency;
- the state of the RPM database;
- available storage;
- the application and middleware components installed on the server, and the dependencies the
  upgrade will touch.

**Why it matters:** this stage makes no change and has no impact on running services. It decides
whether the server is a safe candidate before any work begins, so problems are found while there is
still time to fix them outside the window.

**Gate:** the server is scheduled for the window only if pre-flight passes.

## 2. Recovery point, by server type

**When:** at the start of the window, before the upgrade itself.

Large environments usually contain more than one kind of server, and the right way to take a recovery
point differs for each. The automation first determines what kind of server it is running on, then
captures a **full** recovery point suited to that type. A common mix is:

| Server type | Recovery point |
|-------------|----------------|
| Cloud instance (Amazon EC2) | Use the AWS APIs to find the instance, then create an AMI plus snapshots of all attached volumes |
| Virtual machine (on-premises VMware) | Use the VMware APIs to find the machine and its hypervisor, then snapshot the whole machine and its volumes |
| Physical server | Create a full ReAR (Relax-and-Recover) backup and store it on a separate network file system |

**Housekeeping:** the automation also schedules automatic deletion of these snapshots and backups
after a fixed period (for example fourteen days). A server that has run cleanly for that long is a
successful upgrade, and removing old recovery points keeps storage cost under control.

**Gate:** no recovery point, no upgrade.

## 3. Leapp pre-upgrade with automated remediation

Red Hat's documented process for an in-place upgrade is to run a pre-upgrade assessment, read its
report, resolve each blocking problem, re-run the assessment, and only then upgrade. This stage
automates that loop:

1. run the Leapp pre-upgrade;
2. read the resulting report automatically;
3. work through the blocking items one by one, **applying the fixes** instead of leaving them for an
   engineer;
4. re-run the pre-upgrade to confirm the blockers are gone.

**Gate:** the run moves on only when the report comes back clean. A blocker the automation has not
yet been taught to fix stops the run with a clear explanation (see
[05-improvement-loop.md](05-improvement-loop.md)).

## 4. Upgrade and reboots

The automation runs the Leapp upgrade to move the server to the next major version.

Reboots are needed at several points in the overall process: during the upgrade itself, after
patching, after hardening changes, and during a rollback. The automation drives **every** reboot and
waits for the server to come back and reach a healthy state before it continues, so the analyst never
has to step in between stages.

**Gate:** if a server does not come back as expected, the run stops, reports the failure and alerts
the analyst, so the problem is caught immediately instead of being discovered later.

## 5. Patching to the current baseline

A Leapp upgrade lands the server on a base release of the new major version, which is not the latest
patch level. The automation then patches the server up to the organization's current patch baseline,
for example through **Red Hat Satellite**.

**Gate:** the server must be at the baseline before hardening starts.

## 6. Hardening, including what the tool cannot fix

The upgraded, patched server must now meet the security baseline for the new release, for example the
**CIS benchmark**, checked with **OpenSCAP**.

1. Run OpenSCAP's own remediation, which applies most of the required fixes automatically.
2. Some findings always remain that OpenSCAP's remediation cannot resolve on its own. The automation
   reads the report and fixes each remaining item with remediations customized for the environment.
3. Re-run the scan, and repeat until it passes cleanly.

At this stage the automation also applies any operating-system changes that the application and
middleware components on that server need in order to run on the new major version.

**Gate:** a clean scan.

## 7. Completion and handoff

When the server is upgraded, patched and hardened, the automation:

- notifies the operations team that the upgrade is complete (for example by email);
- publishes the server's new status to a shared record (for example a database).

That published status is what lets the application teams' own automation start their
application-level validation, so the handoff does not depend on someone remembering to tell them.

From here the server belongs to the application and middleware owners, who test their software on
the new major version.

---

## Rollback (rarely needed)

Thanks to the gates, the upgrade itself very rarely has to be undone. A rollback is normally needed
for a different reason: during their testing after the handoff, the application or middleware
owners find that their software is not yet supported on the new major version. The decision is
theirs; the rollback itself is a **separate** automation that restores the recovery point taken in
stage 2. See [03-rollback.md](03-rollback.md).

## What this page does not include

This is the method, not an implementation. The real automation behind each stage depends on how each
organization builds and configures its servers, applications and tools; see
[07-adapting-to-your-organization.md](07-adapting-to-your-organization.md). Short illustrative
examples are in [../snippets/](../snippets/).

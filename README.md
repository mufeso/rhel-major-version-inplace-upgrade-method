# RHEL major-version in-place upgrade method

A reference method for upgrading large fleets of production Red Hat Enterprise Linux (RHEL)
servers to the next major version **in place**, from beginning to end, as one repeatable,
low-risk operation.

> **What this repository is:** a written methodology with checklists, short illustrative
> snippets and skeleton templates. **It is not a working product.** The snippets and templates
> show the shape of each step; a real implementation has to be built and customized for each
> environment (see [docs/07-adapting-to-your-organization.md](docs/07-adapting-to-your-organization.md)).

## The problem

Routine patching inside one RHEL major version is well understood. The hard step comes at the
end of a major version's life cycle, when servers must move to the next major version. Red Hat's
supported tool for an in-place upgrade, **Leapp**, performs the version change itself. Everything
around it is left to the engineer: a recovery point, fixing upgrade blockers, the reboots,
patching to the current baseline, security hardening, and rolling back if something fails.
Done by hand, that is a long sequence of steps that each need senior engineering judgment, so
many organizations defer the upgrade and keep running versions at or past end of maintenance.

This method automates all of the work around Leapp, so the in-place path becomes the faster
and safer choice.

## The method at a glance

An automation run (for example an Ansible playbook) carries each server through these stages,
with a gate between stages so a server only moves on when it is safe:

<p align="center">
  <img src="images/upgrade-stages.svg" alt="The stages of the method, with a gate between each and a separate rollback." width="100%">
</p>

| # | Stage | What happens |
|---|-------|--------------|
| 1 | Pre-flight validation | Read-only checks, run days or weeks before the change window |
| 2 | Recovery points | A full platform copy suited to the server type (AMI and EBS snapshots, VM snapshot or ReaR backup), plus an LVM snapshot for a faster OS-only rollback |
| 3 | Leapp pre-upgrade + remediation | Read the Leapp report, fix each blocker, re-run until clean |
| 4 | Upgrade | Run the Leapp upgrade and drive every reboot, waiting for a healthy state |
| 5 | Patching | Bring the upgraded server to the same baseline as its peer servers (e.g. through Red Hat Satellite) |
| 6 | Validation | Check, and reinstall where needed, the tools and agents the organization requires |
| 7 | Security hardening | CIS benchmark with OpenSCAP remediation, then fix what remains and re-scan until clean |
| 8 | Completion and handoff | Notify the team and publish the server's status for the next teams |
| — | Rollback | A separate, fully automated run that restores the recovery points, for many servers in parallel |
| — | Recovery point expiry | Platform recovery point and LVM snapshots removed automatically two weeks after the upgrade |

Details: [docs/02-stages.md](docs/02-stages.md) and [docs/03-rollback.md](docs/03-rollback.md).

## Why it works

- **A junior analyst can run it.** The engineering judgment is encoded in the automation, so a
  competent Linux analyst runs batches of servers in parallel inside one change window
  ([docs/04-operating-model.md](docs/04-operating-model.md)).
- **Safe by design.** Every server gets a recovery point before any change. Rollback is rarely
  needed, and when it is (usually because an application turns out not to be supported yet on the
  new version), it is automated.
- **It gets smarter over time.** The automation only applies fixes it was taught. When it meets
  something new, usually in a lower environment, it stops and reports; the fix is then engineered
  once and coded in ([docs/05-improvement-loop.md](docs/05-improvement-loop.md)).

## Contents

| Path | Contents |
|------|----------|
| [docs/](docs/) | The method, stage by stage, why it matters, and how to train the team that runs it ([docs/08-training-the-team.md](docs/08-training-the-team.md)) |
| [checklists/](checklists/) | Pre-flight, go/no-go, post-upgrade validation, rollback decision |
| [snippets/](snippets/) | Short illustrative examples (not a working playbook) |
| [templates/](templates/) | Skeleton inventory and variable files (not a working product) |
| [UPSTREAM-CONTRIBUTIONS.md](UPSTREAM-CONTRIBUTIONS.md) | Fixes I contributed to the open-source tools this method relies on |

## Related projects

This method does not replace any of the tools it uses; it combines them into one end-to-end run.
Each one is documented and maintained by its own project:

- **[infra.leapp](https://github.com/redhat-cop/infra.leapp)**: Red Hat's Ansible roles for Leapp
  upgrades (analysis, remediation, upgrade). As its README puts it, running upgrades at scale "needs
  automation tailored to your environment", and the roles are "the foundation" for that. This method
  is about that tailoring: the stages around the core Leapp steps.
- **[Leapp](https://github.com/oamg/leapp-repository)**: the in-place upgrade tool itself.
- **[Red Hat Satellite](https://www.redhat.com/en/technologies/management/satellite)**: patching to
  the environment's baseline.
- **[Linux System Roles](https://linux-system-roles.github.io/)**: the upstream of RHEL System Roles,
  used for standard configuration.
- **[OpenSCAP](https://github.com/OpenSCAP/openscap)** with the CIS content from
  **[ComplianceAsCode](https://github.com/ComplianceAsCode/content)**: security hardening.
- **[ReaR (Relax-and-Recover)](https://github.com/rear/rear)**: recovery points for physical servers.
- The Ansible collections for **[AWS](https://github.com/ansible-collections/amazon.aws)** and
  **[VMware](https://github.com/ansible-collections/community.vmware)**: recovery points for cloud
  instances and virtual machines.

Nothing here depends on a particular organization. Where a fix belongs in one of these projects, it
is sent there ([UPSTREAM-CONTRIBUTIONS.md](UPSTREAM-CONTRIBUTIONS.md)).

## Roadmap

- **Next: RHEL-compatible distributions.** Distributions such as AlmaLinux upgrade between major
  versions with the same Leapp tool, through the AlmaLinux ELevate project. The next step is to
  extend this method's checks to those distributions. The first upstream Leapp fix for that path,
  counting leftover upgrade boot files as available `/boot` space
  ([oamg/leapp-repository#1604](https://github.com/oamg/leapp-repository/pull/1604)), has been
  merged and is already included by AlmaLinux in ELevate NG.

## Author and license

Written by Murilo Souza from his own professional experience. It contains no employer source
code or confidential material.

Licensed under the [Apache License 2.0](LICENSE).

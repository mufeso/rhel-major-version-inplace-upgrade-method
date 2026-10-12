# Training the team to run it without you

The method is not finished when the automation works. It is finished when the organization's own
operations analysts run upgrades, patch cycles and rollbacks on their own, and the engineer who
built the automation is no longer needed in the change window. This page describes how to get there.

## The roles

| Role | Does | Does not |
|------|------|----------|
| **Operations analyst** | Starts runs against batches of servers, follows the output, uses the checklists, decides each server's outcome, runs a rollback when the application owners ask for one | Change the automation; improvise fixes on production servers |
| **Senior on-call engineer** | Takes escalations the analyst cannot resolve from the run's output | Run the batches |
| **Automation owner** | Engineers each new fix once and codes it in; keeps the runbooks and standards current | Sit in every change window once the team is trained |

## What an analyst needs before starting

- Everyday Linux administration: services, packages, storage, networking, logs.
- Reading Ansible output: which task failed, on which host, and the message it gave.
- Access to the tools the runs use (for example Red Hat Satellite and the automation platform) with
  the permissions the runbook lists, and nothing more.

No knowledge of Leapp internals is required. That knowledge is in the automation.

## The training path

Each step has a clear exit condition. An analyst moves on only when it is met.

| Step | Where | What the analyst does | Exit condition |
|------|-------|-----------------------|----------------|
| 1. Read | — | Reads this method ([02-stages.md](02-stages.md), [03-rollback.md](03-rollback.md), [04-operating-model.md](04-operating-model.md), [05-improvement-loop.md](05-improvement-loop.md)) and the checklists | Can explain each stage and gate in their own words |
| 2. Shadow | Development | Watches the trainer run a batch and narrates what each stage is doing | Correctly predicts the next stage and the outcome of each server |
| 3. Run, supervised | Development, test | Runs batches while the trainer watches and only answers questions | Completes a batch without the trainer touching the keyboard |
| 4. Rollback drill | Development or test | Restores a server from its recovery point with the rollback automation, start to finish | Server back in its pre-upgrade state and validated |
| 5. Gate stop | Development or test | Handles a server stopped at a gate: reads the output, resolves it or escalates it | Escalation written with everything the engineer needs (see below) |
| 6. Run, on call | Stage, then production | Runs real windows alone, with the engineer reachable but not present | A full window completed with no intervention from the engineer |

The rollback drill (step 4) is required before an analyst runs production. A rollback is rarely
needed, which is exactly why it has to be practiced before it is.

## What the analyst must be able to do

- Start a run against a batch and confirm every server in it passed pre-flight.
- Use the go/no-go checklist at the start of the window, per batch.
- Read the output at each gate and put every server in one of the three outcomes: completed,
  stopped at a gate, or rolled back ([04-operating-model.md](04-operating-model.md)).
- Run the post-upgrade validation before handing a server to the application owners.
- Run a rollback when the application owners decide on one, using the rollback-decision checklist.
- Escalate a stopped server in a way that does not need a follow-up question.

## The runbook and the standards

Training sticks only if the analyst works from written material that matches the automation.

- **One runbook per type of run** (upgrade, patch cycle, rollback): how to start it, what normal output
  looks like at each stage, what each gate stop means, and who to call.
- **Standards** for the decisions the analyst makes: what counts as a completed server, when to stop a
  batch, when to escalate.
- **Kept current through the improvement loop.** Every time a new problem is engineered into the
  automation ([05-improvement-loop.md](05-improvement-loop.md)), the runbook is updated in the same
  change, so the analyst never meets a gate the runbook does not explain.

## Escalating a stopped server

An escalation should let the engineer start working immediately. A short template:

```text
Server:          <hostname> (<environment>)
Batch / window:  <batch name>, <date and time>
Stage / gate:    <stage where the run stopped>
Run output:      <the failed task and its message, copied as is>
Already tried:   <what the analyst checked or did, if anything>
Server state:    <untouched since the stop / rolled back / other>
Deadline:        <end of the change window>
```

## When the team is ready

The team runs the work without you when:

- analysts complete full change windows with no intervention from the engineer;
- escalations are rare, and each one becomes a fix coded into the automation;
- new analysts are trained by the existing ones, with this path and the runbooks, without the engineer.

At that point the engineer's time goes back to engineering: new fixes, the next major version, and
fixes to the open-source tools themselves ([../UPSTREAM-CONTRIBUTIONS.md](../UPSTREAM-CONTRIBUTIONS.md)).

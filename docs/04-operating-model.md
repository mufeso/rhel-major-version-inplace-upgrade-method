# Who runs it, and why that matters

## A junior analyst runs the upgrade

The engineering judgment is captured in the automation. The person who runs an upgrade or a rollback
therefore does not need to be a senior engineer. A **competent Linux analyst** who can start the run,
follow its output and act on what it reports is enough.

| Without the method | With the method |
|---|---|
| A senior engineer works each server by hand | An analyst starts a run against a batch of servers |
| One server at a time | Many servers in parallel, in the same window |
| Senior engineers on standby for every server | The analyst intervenes only where the run asks for it; escalation is the exception |
| Engineering effort spent every time the task is repeated | Engineering effort spent once, to encode the solution |

## Parallel runs inside one change window

The run is started against many servers at once. A single analyst can have a batch of servers
upgrading at the same time through the same window, watching the output and stepping in only when a
gate stops a server. That is what lets a large number of servers be brought current and secure in one
window, at a fraction of the labor such programs normally need.

## Clear outcomes for each server

Every server ends a run in one of three states, which keeps the change window easy to manage:

1. **Completed:** upgraded, patched, hardened and handed off.
2. **Stopped at a gate:** nothing risky happened; the output says why (see
   [05-improvement-loop.md](05-improvement-loop.md)).
3. **Rolled back:** only when the application owners decide so after testing (see
   [03-rollback.md](03-rollback.md)).

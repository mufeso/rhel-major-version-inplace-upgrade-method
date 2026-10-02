# How the method gets smarter over time

## Stop and report instead of guessing

The automation only applies fixes it has been **explicitly** coded to apply. When it meets a problem
it has not been taught to handle, it does not guess or attempt a risky change. It stops that server and
reports, in plain terms, what the issue is and why it did not continue.

## Lower environments first

Upgrades run in order of risk:

```text
development  →  test / SIT  →  stage  →  production  →  disaster recovery
```

New problems therefore tend to appear first in the lower environments, where they cost the least.

## The loop

1. The run meets an unknown problem and stops with a clear explanation.
2. The analyst resolves it from that explanation, or escalates it to a senior on-call engineer.
3. Afterwards, the case is investigated and a solution is engineered.
4. The fix is coded into the automation, so the next server with the same configuration, usually in
   a higher environment, is handled automatically.

## The effect

Each environment adds cases the automation can handle on its own. In the environment where this
method was developed, over the RHEL 7-to-8 and 8-to-9 programs, the large majority of the problems
these upgrades produce were encoded, to the point where the vast majority of servers now upgrade
fully automatically from start to finish.

## Fixing the tools themselves

Sometimes the cause is not in the environment but in one of the open-source tools the method relies
on. In that case the right fix is upstream, in the tool itself, so that every organization using it
benefits. Fixes contributed this way are listed in
[../UPSTREAM-CONTRIBUTIONS.md](../UPSTREAM-CONTRIBUTIONS.md).

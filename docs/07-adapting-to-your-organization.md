# Adapting the method to an organization

## What transfers, and what does not

The method is built entirely on standard components: Linux, Leapp, Red Hat Satellite, OpenSCAP
with the CIS benchmark, ReAR, and the AWS and VMware APIs. None of it belongs to one company, and
the general approach is not a secret.

What makes it work is **not** a playbook as an artifact. A generic playbook copied unchanged from
one organization to another would fail the moment it met a real production environment.

| Transfers between organizations | Built again at each organization |
|---|---|
| The stages, gates and their order | How applications and middleware are installed and configured |
| The recovery-point strategy by server type | How applications are accessed and validated |
| The stop-and-report rule and the improvement loop | Storage and network conventions |
| The operating model (analysts running batches in a change window) | The compliance baseline and its exceptions |
| The engineering knowledge to recognize a failure, find its cause and code a correct fix | The specific fixes for that environment's problems |

## How to apply it

1. **Inventory and pre-flight.** Build the read-only checks first and run them across the fleet to
   see what the environment contains (see [../checklists/](../checklists/)).
2. **Recovery points.** Implement the recovery point and the rollback for each server type in the
   environment before upgrading anything that matters.
3. **Start low.** Upgrade development servers first; let the automation stop and report.
4. **Encode every fix.** Each problem found is engineered once and coded in (see
   [05-improvement-loop.md](05-improvement-loop.md)).
5. **Move up the environments.** Test, stage, production, then disaster recovery. With each step the
   automation handles more on its own.
6. **Hand over to analysts.** Once most servers complete without intervention, analysts run the
   batches and engineers focus on new cases.

## The result

Each organization that applies the method ends up with modernized systems, a capability it can
maintain, and analysts trained to run it.

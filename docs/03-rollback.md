# Rollback

## When it is needed

The gates in the upgrade run stop a server before anything risky happens, so the upgrade itself
very rarely has to be undone.

In practice, a rollback is almost always needed for one reason: after the handoff, the application
or middleware owners test their software on the new major version and find that some of it is
**not yet supported** there. Ideally this is caught during planning, before the upgrade (see the
pre-flight inventory of installed components in [02-stages.md](02-stages.md)). When it is only
discovered after the upgrade, the owners may decide to roll back so their services are back online
on the previous version while they work with their vendor on a supported path, for example a newer
version of their software, and the server is upgraded again later.

## Who decides, who runs it

- **The decision** belongs to the application and middleware owners, based on their testing.
- **The execution** is automated. An operations analyst starts the rollback run; it needs no manual
  steps.

## What the rollback run does

1. Shuts the server down.
2. Restores the recovery point taken in stage 2 of the upgrade, using the method that matches the
   server type:

   | Server type | Restored from |
   |-------------|---------------|
   | Cloud instance (Amazon EC2) | The AMI and volume snapshots |
   | Virtual machine (VMware) | The VM snapshot |
   | Physical server | The ReAR (Relax-and-Recover) backup |

3. Brings the server back up on the previous major version and confirms it is healthy.

Because it runs unattended and quickly, an incompatibility that would otherwise mean an extended
outage becomes a short, controlled return to a known-good state.

## Why the recovery points expire

Recovery points are kept only for a fixed period after the upgrade (for example fourteen days). Once
the application owners have tested and the server has run cleanly for that long, the upgrade is
considered successful and the old recovery point is removed to control storage cost.

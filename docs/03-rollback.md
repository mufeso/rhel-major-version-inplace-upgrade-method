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
2. Restores the recovery point that fits the decision:

   - **Operating system only**, inside the server (the application itself was not changed on the new
     version): reverts the LVM snapshots and restores `/boot`. This is the faster path.
   - **Whole server**, at the platform level, outside the operating system (for example the
     application team has already changed its software, data or configuration on the new version):
     restores the platform recovery point taken in stage 2 of the upgrade from the cloud, the
     hypervisor or the backup, using the method that matches the server type:

     | Server type | Restored from |
     |-------------|---------------|
     | Cloud instance (Amazon EC2) | The AMI and volume snapshots |
     | Virtual machine (VMware) | The VM snapshot |
     | Physical server | The ReAR (Relax-and-Recover) backup |

3. Brings the server back up on the previous major version, in its state at the start of the change
   window, and confirms it is healthy.

Once the decision is made, even a junior Linux analyst can start the rollback and recover as many
servers as needed, in parallel. Because it runs unattended and quickly, an incompatibility that
would otherwise mean an extended outage becomes a short, controlled return to a known-good state.

## Why the recovery points expire

The platform recovery point and the LVM snapshots are removed automatically two weeks after the
upgrade. That window gives the application owners plenty of time to make sure their software works as
expected on the new major version; once the server has run cleanly for that long, the upgrade is
considered successful and the old recovery points are removed to control storage cost.

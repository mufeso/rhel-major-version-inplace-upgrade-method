# Pre-flight checklist (read-only)

Run days or weeks before the change window. Nothing here changes the server.

## Platform

- [ ] The current and target major versions are a supported in-place upgrade path.
- [ ] The server is registered and its repositories for the target version are available
      (for example through Red Hat Satellite).
- [ ] Package and repository configuration is consistent; no broken or duplicate packages.
- [ ] The RPM database is healthy.
- [ ] Enough free space in the file systems the upgrade uses (for example `/`, `/var`, `/boot`).

## Applications and middleware

- [ ] Installed application and middleware components are inventoried.
- [ ] Each component's owner has confirmed it is **supported on the target major version**,
      or has a plan for it. *(Most rollbacks come from a component found unsupported only after
      the upgrade; this is the place to catch it.)*
- [ ] Known dependencies the upgrade will touch are listed (kernel modules, custom repositories,
      third-party agents).

## Recovery and access

- [ ] The server type is identified (cloud, virtual, physical) and the matching recovery point
      method works for it.
- [ ] Remote console or out-of-band access is available in case the server does not come back.

## Planning

- [ ] The server is assigned to a change window and a batch.
- [ ] The application owners know when they will receive the server for testing.

**Result:** the server is a candidate for the window only if every item is checked or has an
agreed exception.

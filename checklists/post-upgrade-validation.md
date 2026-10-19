# Post-upgrade validation checklist (before handoff)

The automation checks these at its gates; this list is what the analyst confirms in the run output
before the server is handed to the application owners.

- [ ] The server runs the target major version and the expected kernel.
- [ ] The server is at the current patch baseline.
- [ ] The hardening scan (for example CIS with OpenSCAP) passes cleanly.
- [ ] Required services are enabled and running; no failed system units.
- [ ] File systems are mounted as expected; network and name resolution work.
- [ ] The tools and agents the organization requires (security, vulnerability scanning, logging,
      monitoring, CMDB discovery, backup) are installed, running and reporting. *(example)*
- [ ] Operating-system changes required by the server's applications for the new version are applied.
- [ ] The completion notice was sent and the server's status was published for the application teams.
- [ ] The recovery points (platform copy and LVM snapshots) are still in place and their expiry
      date, two weeks after the upgrade, is recorded.

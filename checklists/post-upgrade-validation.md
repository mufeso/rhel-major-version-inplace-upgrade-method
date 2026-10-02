# Post-upgrade validation checklist (before handoff)

The automation checks these at its gates; this list is what the analyst confirms in the run output
before the server is handed to the application owners.

- [ ] The server runs the target major version and the expected kernel.
- [ ] The server is at the current patch baseline.
- [ ] The hardening scan (for example CIS with OpenSCAP) passes cleanly.
- [ ] Required services are enabled and running; no failed system units.
- [ ] File systems are mounted as expected; network and name resolution work.
- [ ] Monitoring, logging and security agents report in. *(example)*
- [ ] Operating-system changes required by the server's applications for the new version are applied.
- [ ] The completion notice was sent and the server's status was published for the application teams.
- [ ] The recovery point is still in place and its expiry date is recorded.

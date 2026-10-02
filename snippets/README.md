# Snippets (illustrative only)

Short examples that show the **shape** of individual steps. They are deliberately incomplete:
they are not a working playbook and are not meant to be run as they are. Variable names such as
`upgrade_*` are placeholders.

| Snippet | Shows |
|---------|-------|
| [stage-gate.yml](stage-gate.yml) | A gate: stop the server and report why, instead of continuing |
| [leapp-preupgrade-report.yml](leapp-preupgrade-report.yml) | Running the Leapp pre-upgrade and reading the inhibitors from its report |
| [reboot-and-wait.yml](reboot-and-wait.yml) | A reboot followed by a health check before the next stage |
| [openscap-loop.yml](openscap-loop.yml) | The scan, remediate, re-scan idea for hardening |

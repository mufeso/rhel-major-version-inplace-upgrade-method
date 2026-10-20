# Changelog

## Unreleased

## v1.0.2 - 2026-10-20

- Upstream contributions list updated (20 October 2026): amazon.aws #3140 and OpenSCAP #2451
  merged; nine fixes merged in total, five in review.

## v1.0.1 - 2026-10-19

- Stages updated to match the method as run in production: a full platform recovery point plus an
  LVM snapshot for a faster OS-only rollback; patching to the same baseline as peer servers; a new
  validation stage for the tools and agents the organization requires; security hardening as the
  last stage before handoff; automated rollback from either recovery point, for many servers in
  parallel; recovery points removed automatically two weeks after the upgrade. README table, stage
  diagram, docs/02-stages.md, docs/03-rollback.md and the post-upgrade checklist updated.
- README: new "Related projects" section (infra.leapp, Leapp, Red Hat Satellite, Linux System
  Roles, OpenSCAP and ComplianceAsCode, ReaR, the AWS and VMware Ansible collections), replacing
  "Built on standard components"; roadmap updated (leapp-repository #1604 merged and included in
  AlmaLinux ELevate NG).
- Upstream contributions list updated (19 October 2026): insights-core #4825 merged (14 October)
  and released in 3.8.3; OpenSCAP #2451 submitted; new "Adopted by other projects" section
  (AlmaLinux ELevate NG includes leapp-repository #1604).

## v1.0.0 - 2026-10-13

- README: roadmap section (next step: RHEL-compatible distributions through ELevate).
- Upstream contributions list updated (5 October 2026).
- Upstream contributions list updated (6 October 2026): aide #119 merged; merge dates added.
- Upstream contributions list updated (8 October 2026): foreman-ansible-modules #2048 and #2049 merged.
- Upstream contributions list updated (9 October 2026): theforeman.foreman 6.0.0 released with #2048 and #2049.
- Upstream contributions list updated (11 October 2026): infra.leapp #446 submitted.
- New: docs/08-training-the-team.md, how to train operations analysts to run upgrades, patch cycles and rollbacks without the engineer.
- Upstream contributions list updated (12 October 2026): infra.leapp #447 submitted.
- Upstream contributions list updated (13 October 2026): leapp-repository #1604 merged.

## v0.1.0 - 2026-10

First public release.

- The method: README and docs 01 to 07 (keeping servers current, the stages, rollback, operating
  model, improvement loop, why it matters, adapting to an organization).
- Stage diagram (`images/upgrade-stages.svg`).
- Checklists: pre-flight, go/no-go, post-upgrade validation, rollback decision.
- Illustrative snippets and templates (not a working product).
- List of upstream contributions to the tools the method relies on.

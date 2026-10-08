# Upstream contributions

When a problem comes from one of the open-source tools this method relies on, the right fix is in
the tool itself, so every organization that uses it benefits. These are the fixes I have contributed.

Status as of 8 October 2026.

## Merged (accepted into the project)

| Project | Pull request | What it fixes | Merged |
|---------|--------------|---------------|--------|
| linux-system-roles/podman (upstream of RHEL System Roles) | [#341](https://github.com/linux-system-roles/podman/pull/341) | Creates host directories from quadlet `Volume` host paths (issue [#336](https://github.com/linux-system-roles/podman/issues/336)) | 30 September 2026 |
| linux-system-roles/podman | [#345](https://github.com/linux-system-roles/podman/pull/345) | Resolves relative quadlet `Volume` paths the way Quadlet does (follow-up to #341) | 2 October 2026 |
| linux-system-roles/aide (upstream of RHEL System Roles) | [#119](https://github.com/linux-system-roles/aide/pull/119) | Configures the aide cron check before the AIDE database is created (issue [#47](https://github.com/linux-system-roles/aide/issues/47)) | 5 October 2026 |
| theforeman/foreman-ansible-modules (upstream of the Red Hat Satellite Ansible collection) | [#2048](https://github.com/theforeman/foreman-ansible-modules/pull/2048) | Documents that the inventory plugin's `legacy_hostvars` option needs `want_params` (issue [#1940](https://github.com/theforeman/foreman-ansible-modules/issues/1940)) | 7 October 2026 |
| theforeman/foreman-ansible-modules | [#2049](https://github.com/theforeman/foreman-ansible-modules/pull/2049) | Updates the `activation_keys` role documentation for Simple Content Access, where auto-attach is obsolete (issue [#1902](https://github.com/theforeman/foreman-ansible-modules/issues/1902)) | 8 October 2026 |

## In review (submitted, not merged yet)

| Project | Pull request | What it fixes |
|---------|--------------|---------------|
| candlepin/subscription-manager (RHEL registration client) | [#3786](https://github.com/candlepin/subscription-manager/pull/3786) | The real SSL error is hidden by a certificate error during first registration (issue [#3640](https://github.com/candlepin/subscription-manager/issues/3640)) |
| RedHatInsights/insights-core | [#4825](https://github.com/RedHatInsights/insights-core/pull/4825) | `show_rule_report` pages the wrong variable (issue [#4672](https://github.com/RedHatInsights/insights-core/issues/4672)) |
| redhat-cop/infra.leapp | [#439](https://github.com/redhat-cop/infra.leapp/pull/439) | Makes `cleanup_logs` idempotent (issue [#419](https://github.com/redhat-cop/infra.leapp/issues/419)) |
| oamg/leapp-repository | [#1602](https://github.com/oamg/leapp-repository/pull/1602) | Clarifies the SELinux report after the upgrade (issue [#815](https://github.com/oamg/leapp-repository/issues/815)) |
| oamg/leapp-repository | [#1604](https://github.com/oamg/leapp-repository/pull/1604) | Counts leftover upgrade boot files as available `/boot` space after a failed attempt (issue [#1311](https://github.com/oamg/leapp-repository/issues/1311)) |
| ansible-collections/amazon.aws | [#3140](https://github.com/ansible-collections/amazon.aws/pull/3140) | `acm` fails with `KeyError` when a certificate has no domain name (issue [#2405](https://github.com/ansible-collections/amazon.aws/issues/2405)) |

This list is updated as pull requests are reviewed and merged.

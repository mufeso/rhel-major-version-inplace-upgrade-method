# Upstream contributions

When a problem comes from one of the open-source tools this method relies on, the right fix is in
the tool itself, so every organization that uses it benefits. These are the fixes I have contributed.

Status as of 13 October 2026.

## Merged (accepted into the project)

| Project | Pull request | What it fixes | Merged |
|---------|--------------|---------------|--------|
| linux-system-roles/podman (upstream of RHEL System Roles) | [#341](https://github.com/linux-system-roles/podman/pull/341) | Creates host directories from quadlet `Volume` host paths (issue [#336](https://github.com/linux-system-roles/podman/issues/336)) | 30 September 2026 |
| linux-system-roles/podman | [#345](https://github.com/linux-system-roles/podman/pull/345) | Resolves relative quadlet `Volume` paths the way Quadlet does (follow-up to #341) | 2 October 2026 |
| linux-system-roles/aide (upstream of RHEL System Roles) | [#119](https://github.com/linux-system-roles/aide/pull/119) | Configures the aide cron check before the AIDE database is created (issue [#47](https://github.com/linux-system-roles/aide/issues/47)) | 5 October 2026 |
| theforeman/foreman-ansible-modules (upstream of the Red Hat Satellite Ansible collection) | [#2048](https://github.com/theforeman/foreman-ansible-modules/pull/2048) | Documents that the inventory plugin's `legacy_hostvars` option needs `want_params` (issue [#1940](https://github.com/theforeman/foreman-ansible-modules/issues/1940)) | 7 October 2026 |
| theforeman/foreman-ansible-modules | [#2049](https://github.com/theforeman/foreman-ansible-modules/pull/2049) | Updates the `activation_keys` role documentation for Simple Content Access, where auto-attach is obsolete (issue [#1902](https://github.com/theforeman/foreman-ansible-modules/issues/1902)) | 8 October 2026 |
| oamg/leapp-repository (upstream of the Leapp in-place upgrade tool in RHEL) | [#1604](https://github.com/oamg/leapp-repository/pull/1604) | Counts leftover upgrade boot files as available `/boot` space after a failed upgrade attempt (issue [#1311](https://github.com/oamg/leapp-repository/issues/1311)) | 13 October 2026 |

## Released (included in a published version)

| Project | Version | Released | Contains |
|---------|---------|----------|----------|
| theforeman.foreman Ansible collection (upstream of the Red Hat Satellite Ansible collection) | [6.0.0](https://github.com/theforeman/foreman-ansible-modules/releases/tag/v6.0.0) ([Ansible Galaxy](https://galaxy.ansible.com/ui/repo/published/theforeman/foreman/)) | 9 October 2026 | #2048, #2049 |

The Linux System Roles fixes (#341, #345, #119) will be listed here once a release includes them.

## In review (submitted, not merged yet)

| Project | Pull request | What it fixes |
|---------|--------------|---------------|
| candlepin/subscription-manager (RHEL registration client) | [#3786](https://github.com/candlepin/subscription-manager/pull/3786) | The real SSL error is hidden by a certificate error during first registration (issue [#3640](https://github.com/candlepin/subscription-manager/issues/3640)) |
| RedHatInsights/insights-core | [#4825](https://github.com/RedHatInsights/insights-core/pull/4825) | `show_rule_report` pages the wrong variable (issue [#4672](https://github.com/RedHatInsights/insights-core/issues/4672)) |
| redhat-cop/infra.leapp | [#439](https://github.com/redhat-cop/infra.leapp/pull/439) | Makes `cleanup_logs` idempotent (issue [#419](https://github.com/redhat-cop/infra.leapp/issues/419)) |
| oamg/leapp-repository | [#1602](https://github.com/oamg/leapp-repository/pull/1602) | Clarifies the SELinux report after the upgrade (issue [#815](https://github.com/oamg/leapp-repository/issues/815)) |
| ansible-collections/amazon.aws | [#3140](https://github.com/ansible-collections/amazon.aws/pull/3140) | `acm` fails with `KeyError` when a certificate has no domain name (issue [#2405](https://github.com/ansible-collections/amazon.aws/issues/2405)) |
| redhat-cop/infra.leapp | [#446](https://github.com/redhat-cop/infra.leapp/pull/446) | Re-registers with the post-upgrade Satellite activation key before setting the release, so a release such as `9` that only the post-upgrade content view offers can be set (issue [#386](https://github.com/redhat-cop/infra.leapp/issues/386)) |
| redhat-cop/infra.leapp | [#447](https://github.com/redhat-cop/infra.leapp/pull/447) | Restores the original rescue kernel files if recreating the rescue kernel after the upgrade fails (issue [#422](https://github.com/redhat-cop/infra.leapp/issues/422)) |

This list is updated as pull requests are reviewed and merged.

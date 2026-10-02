# How Linux servers are kept current, and where this method fits

## Routine patching is not the hard part

Every well-run organization patches its servers on a regular cycle, and those patches are applied
**within** a single major operating-system version. Red Hat Enterprise Linux, for example, follows a
ten-year life cycle in which minor releases arrive roughly every six months and security fixes are
delivered throughout, all within the same major version [1]. This is ordinary, well-understood
maintenance.

## The hard part: the major-version step

A major version does not receive security updates forever. When it reaches end of maintenance, its
servers have to move to the next major version, and there are two ways to do it.

| | Rebuild and migrate | Upgrade in place |
|---|---|---|
| What happens | Build a new server on the new version, reinstall applications and middleware, copy the data, cut clients over | Upgrade the existing server, keeping its applications, data and configuration |
| Red Hat's description | A clean install "removes all traces of the previously installed operating system, system data, configurations, and applications" [3] | "the recommended and supported way to upgrade your system to the next major version of RHEL" [3] |
| Who carries the effort | Every application and middleware team rebuilds and revalidates | The infrastructure team, if the upgrade is automated |

Red Hat's supported tool for the in-place path is **Leapp** [2]. Leapp performs the version change
itself. Red Hat's documented process is to run a pre-upgrade assessment, read its report, resolve
each blocking problem, re-run the assessment, then upgrade and complete the post-upgrade tasks [3].
Taking a recovery point, patching to the current level, hardening the result and rolling back if
something fails are left to the engineer. Done by hand, the in-place path becomes a long sequence of
steps that each need senior engineering judgment.

## Why it matters that this step is hard

Because the major-version step is demanding either way, many organizations postpone it and keep
running versions at or past end of maintenance. Those servers stop receiving security fixes, and the
exposure grows over time.

## Where this method fits

The method automates all of the manual work **around** Leapp, from beginning to end, so the in-place
upgrade becomes one repeatable, low-risk operation. That makes the in-place path the faster and safer
choice, removes the rebuild burden from the application and middleware teams, and lets an
organization stay current instead of deferring.

## References

1. Red Hat Enterprise Linux Life Cycle, Red Hat Customer Portal. <https://access.redhat.com/support/policy/updates/errata>
2. How to upgrade Red Hat Enterprise Linux with the Leapp utility, Red Hat. <https://www.redhat.com/en/resources/leapp-explained-detail>
3. Upgrading from RHEL 8 to RHEL 9, Red Hat Documentation. <https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/upgrading_from_rhel_8_to_rhel_9/index>

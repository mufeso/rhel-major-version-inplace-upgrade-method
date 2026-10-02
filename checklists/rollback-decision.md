# Rollback decision checklist

Rollback is rare. It is normally requested by the application or middleware owners after their
testing on the new major version.

## Before deciding

- [ ] The problem is reproduced and described (what fails, since when, on which server).
- [ ] It is confirmed to come from the new major version, not from an unrelated change.
- [ ] The owners checked with their vendor whether a supported fix or version exists that could be
      applied **without** rolling back.
- [ ] The recovery point is still within its retention period.

## Deciding

- [ ] The application owner requests the rollback; the decision and reason are recorded.
- [ ] A change is raised for the rollback window.

## After the rollback

- [ ] The server is back on the previous version and healthy; services are back online.
- [ ] The owners have a plan with their vendor (for example a newer, supported version of the
      software) and a target date for the next upgrade attempt.
- [ ] The finding is fed back into pre-flight, so the same component is caught **before** the next
      upgrade.

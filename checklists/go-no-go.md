# Go / no-go checklist (start of the change window)

Per batch, before the run starts.

- [ ] The change is approved and the window is open.
- [ ] Every server in the batch passed pre-flight; nothing changed since (new packages, new
      applications, configuration drift).
- [ ] Application owners have stopped or drained their services as agreed.
- [ ] The analyst running the batch knows the escalation path (on-call engineer, contacts).
- [ ] Notification of start sent to the operations team and the application owners.
- [ ] Recovery-point capacity is available (snapshot quotas, backup storage).

**Go** only when every item is checked. A server with an open item is removed from the batch,
not forced through.

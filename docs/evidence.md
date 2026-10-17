# Evidence and scope

This portfolio was reconstructed from the existing private README, service map, storage map, and Python integration source. No live Proxmox connections or guest changes were performed during preparation.

| Statement | Basis | Limit |
| --- | --- | --- |
| Three-node lab / ten guests | Existing service inventory | Historical snapshot; no fresh live inventory |
| Shared NFS and local ZFS | Existing storage inventory | No new storage health test |
| Seven guests selected for backup | Existing job notes | Not proof every scheduled run completed |
| Monitoring-container backup successful | October 12 notes, ~623 MB | Raw task log and restore evidence unavailable |
| Package-index update successful | Existing housekeeping notes | Not a complete OS-upgrade test |
| Guest agents not responding | Existing service-map notes | Follow-up diagnosis not yet recorded |
| Public integration checks | Companion repository's automated tests | Offline checks, not live API compatibility certification |

## Visual evidence

The architecture graphic is an authored diagram derived from the inventory. It is not a screenshot. No live-console screenshots were available for publication in this preparation.

Useful additions after a read-only review of the lab:

- Sanitized cluster overview showing the three nodes.
- Backup-job settings showing selected guests, schedule, and retention.
- A successful backup task log with hostnames, addresses, and user information redacted.
- A later isolated restore-test record and service verification.

The portfolio stands on its documentation today; screenshots should be added only when they correspond to an actual observed result.

# Storage inventory

Storage names are aliases. The key distinction is whether each target is shared across nodes or local to one node.

| Storage | Scope | Purpose | Notes |
| --- | --- | --- | --- |
| shared-nfs | Shared across A, B, C | Backup archives and VM images | Remote target provided by the NAS VM |
| node-a-zfs | Node A | VM and container disks | Local ZFS pool |
| node-b-zfs | Node B | VM and container disks | Local ZFS pool |
| node-b-ssd | Node B | Local backups, ISOs, templates, snippets, and VM images | Separate from shared NFS |
| transfer-local | Multiple nodes | Transfer / staging | Same label, separate node-local capacity |
| local | Per node | Installation media, templates, and local backups | Node-local directory storage |
| local-lvm | Per node | Guest disks | Node-local LVM-thin storage |

## Moving guests

A disk on node-local storage needs explicit storage handling during a guest move or recovery. A matching storage name on another node does not make that disk available there. Check the disk’s actual location and destination capacity before planning the move.

## Retention and exclusions

The shared NFS target uses `keep-last=4,keep-weekly=4,keep-monthly=2`. These retention rules keep eligible recent, weekly, and monthly recovery points from the scheduled backups; the number of distinct archives depends on the available backups and overlap between rules.

The NAS VM’s OS disk is included in the backup schedule, but its passthrough data disk is excluded. A separate backup for that data and an independent NAS recovery copy are planned improvements in [backup and recovery](backup-and-recovery.md).

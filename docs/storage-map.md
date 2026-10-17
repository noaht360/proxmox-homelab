# Storage inventory

Storage identifiers below are aliases. Original export paths, addresses, and mount locations are intentionally omitted.

| Public alias | Scope | Purpose | Operational distinction |
| --- | --- | --- | --- |
| shared-nfs | Shared across A, B, C | Backup archives and VM images | Same remote storage target, provided by the NAS VM |
| node-a-zfs | Node A | VM and container disks | Local ZFS pool; not shared |
| node-b-zfs | Node B | VM and container disks | Local ZFS pool; not shared |
| node-b-ssd | Node B | Local backups, ISOs, templates, snippets and VM images | Separate from shared NFS |
| transfer-local | Multiple nodes | Transfer / staging | Same label does not mean shared capacity |
| local | Per node | Installation media, templates and local backups | Node-local directory storage |
| local-lvm | Per node | Guest disks | Node-local LVM-thin storage |

## Why the distinction matters

A guest disk on node-local storage needs explicit storage handling during a move or recovery. A matching storage name on another node does not make the disk accessible there. The inventory was written to make these assumptions visible before maintenance.

## Backup boundaries

The shared NFS target has configured retention of four recent, four weekly, and two monthly backups. These are retention rules, not evidence of a fixed number of independent archives, and they do not create weekly/monthly backup jobs.

The NAS guest's passthrough disk is excluded from VM backup. There is no documented independent backup of that data in the source material. See the [recovery plan](backup-and-recovery.md).

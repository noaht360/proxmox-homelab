# Service inventory

Lab inventory as of October 12, 2026. Names and IDs are aliases. Backup entries show which guests are included in the schedule.

| Guest ID | Node | Type | Purpose | State | Startup / protection | Backup |
| --- | --- | --- | --- | --- | --- | --- |
| 110 | A | QEMU | Windows utility | Running | On; order 30; protected | Scheduled |
| 111 | A | QEMU | Primary AMP / game hosting | Running | On; order 20; protected | Scheduled |
| 112 | A | LXC | DNS / Pi-hole | Stopped intentionally | Off; unprotected | Excluded |
| 113 | A | LXC | Uptime Kuma monitoring | Running | On; protected | Scheduled; manual backup completed |
| 115 | A | QEMU | Datacenter management | Running | On; order 40; protected | Scheduled |
| 116 | A | QEMU | EVE network lab | Stopped | Off; unprotected | Excluded |
| 119 | A | QEMU | Kali lab | Stopped | Off; unprotected | Excluded |
| 214 | B | LXC | Nginx Proxy Manager | Running | On; protected | Scheduled |
| 211 | B | QEMU | Secondary AMP / game hosting | Running | On; order 20; protected | Scheduled |
| 311 | C | QEMU | OpenMediaVault NAS | Running | On; order 10; protected | OS disk scheduled; passthrough data excluded |

## Guest agents

Agent support is enabled in Proxmox for five QEMU guests. The agents were not responding at the time of this inventory, so the in-guest packages, services, and devices still need checking. The [guest-agent procedure](operations.md#guest-agent-investigation) covers that follow-up.

## Backup coverage

The seven core and utility guests are included in the backup job. The paused DNS and two lab guests are excluded. The NAS entry covers its OS disk; the passthrough data disk needs separate protection. See [backup and recovery](backup-and-recovery.md).

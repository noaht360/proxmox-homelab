# Service inventory

Historical snapshot from the October 12, 2026 lab notes. Node and guest identifiers are aliases. `Scheduled` describes configuration, not verified backup completion for each guest.

| Public ID | Node | Type | Purpose | Recorded state | Startup / protection | Backup |
| --- | --- | --- | --- | --- | --- | --- |
| 110 | A | QEMU | Windows utility | Running | On; order 30; protected | Scheduled |
| 111 | A | QEMU | Primary AMP / game hosting | Running | On; order 20; protected | Scheduled |
| 112 | A | LXC | DNS / Pi-hole | Stopped intentionally | Off; unprotected | Excluded |
| 113 | A | LXC | Uptime Kuma monitoring | Running | On; protected | Scheduled; manual backup recorded successful |
| 115 | A | QEMU | Datacenter management | Running | On; order 40; protected | Scheduled |
| 116 | A | QEMU | EVE network lab | Stopped | Off; unprotected | Excluded |
| 119 | A | QEMU | Kali lab | Stopped | Off; unprotected | Excluded |
| 214 | B | LXC | Nginx Proxy Manager | Running | On; protected | Scheduled |
| 211 | B | QEMU | Secondary AMP / game hosting | Running | On; order 20; protected | Scheduled |
| 311 | C | QEMU | OpenMediaVault NAS | Running | On; order 10; protected | OS disk scheduled; passthrough data excluded |

## Follow-up: guest agents

The notes record guest-agent support enabled in Proxmox for five QEMU guests, with no responding in-guest agents yet. A host-side checkbox does not prove that the guest package is installed or its service is running. See the [guest-agent runbook](operations.md#guest-agent-investigation).

No guest addresses or management URLs are published. This map is documentation and must not be applied as a live configuration.

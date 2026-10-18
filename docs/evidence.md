# Lab progress

## Completed work

| Area | Work completed |
| --- | --- |
| Inventory | Mapped ten guests across three Proxmox nodes, including purpose, startup settings, protection, and backup coverage |
| Storage | Separated shared NFS from node-local ZFS, SSD, and staging storage in the documentation |
| Networking | Connected the OVH-hosted OPNsense firewall to game-server nodes over WireGuard for public game connectivity; [networking walkthrough](networking.md) |
| Backups | Configured seven guests for Tuesday/Saturday backups with zstd compression and retention rules |
| Backup test | Successfully backed up the monitoring container to NFS on October 12, 2026; archive approximately 623 MB |
| Package sources | Switched one lab node to no-subscription repositories and completed `apt update` |
| Housekeeping | Added guest tags and core-guest protection, set on-boot behavior, ejected unused installation media, and removed two unused detached volumes |
| Automation | Added a [Python MCP adapter](https://github.com/noaht360/proxmox-mcp) with an offline demo and automated checks |

## In progress

**Guest agents:** agent support is enabled in Proxmox for five QEMU VMs, but communication was not working in the October 12 inventory. The next step is checking the in-guest packages, services, and communication devices using the [troubleshooting procedure](operations.md#guest-agent-investigation).

**Recovery testing:** the monitoring-container backup completed successfully; the isolated restore drill is pending. See the [restore procedure](backup-and-recovery.md#planned-restore-drill).

## Next improvements

- Keep a NAS bootstrap copy accessible independently of the NAS VM.
- Add separate protection for the NAS passthrough data disk.
- Test application readiness and startup behavior across nodes.
- Review scheduled backup results and test failure notifications.

The service and storage inventories reflect the lab on October 12, 2026. Integration test results are maintained in the [adapter repository](https://github.com/noaht360/proxmox-mcp/blob/main/docs/verification.md).

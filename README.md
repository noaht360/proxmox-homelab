# Proxmox Home Lab

**A three-node Proxmox lab with Linux and Windows workloads, shared storage, game servers, and OPNsense/WireGuard networking.**

I use this lab to host services and practice the work that keeps them running: managing VMs and containers, organizing storage, configuring backups, connecting game servers through a cloud firewall, and troubleshooting service issues. This repository walks through the setup, the decisions behind it, and the improvements I’m working on.

![Logical architecture of the three-node lab](assets/architecture.svg)

## Lab overview

| Component | Setup |
| --- | --- |
| Compute | Three Proxmox nodes running QEMU VMs and LXC containers |
| Workloads | AMP game servers, Windows utility VM, datacenter management, and network/security labs |
| Services | Uptime Kuma, Nginx Proxy Manager, and OpenMediaVault |
| Networking | Cloud-hosted OPNsense firewall on an OVH VPS, linked to game-server nodes through WireGuard |
| Storage | Node-local ZFS, local SSD storage, and shared NFS |
| Backups | Seven guests scheduled twice weekly with zstd compression and retention rules |
| Automation | A [Python MCP adapter](https://github.com/noaht360/proxmox-mcp) for the Proxmox API |

## Explore the setup

- [Architecture and design decisions](docs/architecture.md) — where services run and how storage connects
- [OPNsense and WireGuard](docs/networking.md) — how players reach the game servers through the cloud firewall and tunnels
- [Service inventory](docs/service-map.md) — guest roles, startup settings, and backup coverage
- [Storage inventory](docs/storage-map.md) — shared storage versus node-local storage
- [Backup and recovery](docs/backup-and-recovery.md) — schedule, exclusions, and restore procedure
- [Maintenance and troubleshooting](docs/operations.md) — repository maintenance, guest agents, and cleanup
- [Lab progress](docs/evidence.md) — completed work and next improvements

## Decisions that matter

**The public entry point is separate from game hosting.** OPNsense runs on a cloud VPS and forwards the required game traffic through WireGuard to the game-server nodes. This brings the public firewall, tunnel routing, and game services into one connection path.

**Local and shared storage need different handling.** A storage name can exist on several nodes while referring to separate local disks. I documented each storage target’s scope so moves and recovery work start with the right assumptions.

**Backup coverage needs to include individual disks.** The NAS VM’s OS disk is included in the backup schedule, while its large passthrough data disk is excluded. That data needs its own protection plan.

**Startup settings are part of service management.** Core guests have on-boot settings and deletion protection. Storage is assigned an earlier startup order than the game servers; service readiness across nodes still needs a separate check.

## Backup progress

A manual backup of the monitoring container completed successfully on **October 12, 2026**, producing an archive of approximately **623 MB**. An isolated restore drill is the next step toward checking recovery time and service functionality after a restore.

The backup target is provided by a NAS VM inside this lab. An independent recovery copy and protection for the NAS data disk are also on the [improvement list](docs/evidence.md).

Node names, guest IDs, and storage names in these docs are aliases. The service inventory reflects the lab on October 12, 2026.

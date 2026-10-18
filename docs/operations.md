# Maintenance and troubleshooting

## APT repository maintenance

One lab node was configured with Proxmox enterprise repositories. I switched it to the no-subscription repositories for the lab and completed `apt update` successfully.

The important checks are the installed Proxmox/Debian version, active source files, subscription status, and any repository warnings. Repository entries need to match the node’s release; copying entries from a different version can create package conflicts.

### Maintenance approach

1. Check the node’s Proxmox and Debian versions.
2. Inspect the active repository entries and keep a copy of the existing configuration.
3. Choose the appropriate repositories for that release and subscription status.
4. Refresh package indexes and review the result for errors.
5. Plan package upgrades separately, including maintenance timing and rollback.

**Result:** the package-index refresh succeeded. Package upgrades and a reboot were outside this maintenance step.

## Guest-agent investigation

Guest-agent support was enabled in Proxmox for five QEMU VMs, but the agents were not responding. Enabling the host-side setting only configures the Proxmox side of the connection; the guest also needs its package, service, and communication device working.

### Troubleshooting procedure

1. Confirm the VM is running and the guest-agent channel is configured.
2. Inside a Linux guest, check whether the QEMU guest-agent package is installed and its service is running. On Windows, check the installed service and drivers.
3. Read the service logs and confirm the communication device is present.
4. If adding the device requires a VM restart, schedule it before testing again.
5. Check agent communication from Proxmox and record the result.

**Status:** follow-up work remains on the guest side.

## Service inventory and housekeeping

I organized the guest inventory around each service’s purpose, startup settings, deletion protection, and backup coverage. During that work:

- Added tags for core, utility, lab, monitoring, storage, proxy, DNS, and game-server roles.
- Enabled deletion protection and on-boot behavior for core guests.
- Kept paused lab guests off at boot.
- Ejected installation media from selected VMs.
- Removed two unused detached volumes from the Windows utility VM.

This gives maintenance work a clearer starting point: identify the service, check its dependencies and backup coverage, then review the proposed change. Before removing a disk, confirm its ownership and that no guest still needs its contents.

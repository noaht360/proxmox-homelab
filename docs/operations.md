# Operational case studies

These writeups distinguish actions recorded in the existing lab notes from proposed verification. Commands are illustrative and are not executed by this repository.

## APT repository maintenance

**Problem:** one node's package-source configuration needed housekeeping for a home-lab installation.

**Recorded work:** the node was switched from enterprise repositories to no-subscription repositories, and `apt update` completed successfully.

**What this establishes:** package-index refresh completed after the source change. It does not prove that all packages were upgraded, that the node rebooted successfully, or that a production support policy was followed.

**Repeatable approach:** record the installed Proxmox/Debian release, inspect all active source files and repository warnings, choose sources appropriate to that exact release and subscription status, retain the previous configuration, then refresh indexes and inspect the task result. A package upgrade is a separate change with its own maintenance and rollback plan.

**Lesson:** inspect the repository configuration and task logs rather than treating a UI warning as an instruction to blindly upgrade.

## Guest-agent investigation

**Observation:** the host-side guest-agent setting was enabled for five VMs, but the agents were not responding in the recorded snapshot.

**Next diagnostic steps:**

1. Confirm the VM is running and the guest-agent channel is configured.
2. Inside a Linux guest, inspect whether the QEMU guest-agent package is installed and its service is running. On Windows, inspect the relevant installed service and drivers.
3. Read service logs and confirm the communication device is present.
4. If a VM restart is needed to add a device, schedule it; do not assume a guest service restart will always suffice.
5. Check agent communication again from Proxmox and record the result.

**Status:** unresolved in the available notes. The portfolio does not claim a completed fix.

**Lesson:** configuration intent at the hypervisor and working functionality inside a guest are separate checks.

## Service inventory and startup housekeeping

**Recorded work:** service tags were added, core guests received deletion protection and on-boot settings, and installation media was ejected from selected VMs. Two unused detached volumes were removed from the Windows utility VM.

**Why document it:** a guest list becomes more useful when it also records role, dependency, protection, and backup coverage. Disk cleanup is irreversible; a runbook should establish ownership and confirm that a volume is genuinely unused before removal.

**Remaining verification:** guest health after maintenance, startup/readiness behavior, and current backups. The source notes are not a substitute for these checks.

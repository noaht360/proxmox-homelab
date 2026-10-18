# Backup and recovery

## Backup policy

| Setting | Value |
| --- | --- |
| Target | Shared NFS storage |
| Schedule | Tuesday and Saturday at 03:00, using the scheduler’s local time |
| Method | Proxmox snapshot-mode vzdump |
| Compression | zstd |
| Included | Seven core and utility guests in the [service inventory](service-map.md) |
| Excluded | Paused DNS, network lab, and security lab |
| Retention | `keep-last=4,keep-weekly=4,keep-monthly=2` |
| Disk exclusion | NAS passthrough data disk |

The retention settings select which recovery points to keep; they do not create additional weekly or monthly jobs. Before planning around a specific backup window, check the scheduler’s timezone and recent job results.

## Backup test

On October 12, 2026, a manual backup of the Uptime Kuma LXC container completed successfully to NFS. The compressed archive was approximately 623 MB. A restore drill is still pending, so recovery time has not been measured.

## Recovery considerations

- The twice-weekly schedule leaves several days between planned recovery points. Failed jobs can extend that gap.
- The backup target is provided by a VM in the same lab. A NAS, host, or site failure can affect access to the archives.
- The NAS VM’s backup covers its OS disk, not the excluded passthrough data disk.
- Snapshot-mode backups need workload-specific checks for application consistency.
- Guest deletion protection helps prevent accidental deletion but does not protect the backup archives.

## Planned restore drill

Start with the monitoring container so the drill has a clear service to validate.

1. Select its backup archive and confirm there is enough destination capacity.
2. Record the archive timestamp and the drill start time.
3. Restore to a new, unused guest ID on an isolated network. Keep the original guest intact.
4. Start the restored guest and check its filesystem, service process, saved configuration, and local service response.
5. Compare the restored configuration with the source. Keep the copy from sending duplicate notifications or running duplicate jobs.
6. Record time to usable service, missing data, and any repairs needed.
7. Review the results before removing the temporary guest.

## Next improvements

| Improvement | Completion check |
| --- | --- |
| Restore drill | Restored monitoring service works; elapsed time and checks recorded |
| NAS bootstrap copy | NAS OS/configuration backup is reachable without the NAS VM running |
| NAS data backup | Excluded data has a separate backup and a successful sample restore |
| Independent recovery copy | Archives remain accessible after loss of the lab’s shared storage |
| Backup monitoring | Recent jobs reviewed and a failure notification tested |

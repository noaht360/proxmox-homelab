# Backup policy and recovery plan

## Recorded configuration

| Setting | Recorded value |
| --- | --- |
| Target | Shared NFS storage |
| Schedule | Tuesday and Saturday at 03:00, scheduler's configured local time |
| Method | Proxmox snapshot-mode vzdump |
| Compression | zstd |
| Selected guests | Seven core / utility guests in the service map |
| Intentionally skipped | Paused DNS, network lab, and security lab |
| Retention | keep-last=4, keep-weekly=4, keep-monthly=2 |
| Important exclusion | NAS passthrough data disk has backup disabled |

The inventory establishes policy configuration. It does not show a full history of successful scheduled runs. The scheduler timezone was not captured in the source notes and should be verified before quoting exact recovery windows.

## Recorded result

On October 12, 2026, the lab notes record a successful manual backup of the monitoring LXC container to NFS, about 623 MB compressed. This establishes one recorded backup operation, not recovery readiness. Raw logs and a restore result are not included in the source material.

## Recovery limitations

- No measured recovery-time objective (RTO) or demonstrated recovery-point objective (RPO) is claimed.
- A twice-weekly schedule leaves a gap of several days between planned copies; failures could extend it.
- Snapshot mode is not evidence of application-consistent backups for every workload.
- The NAS VM and shared backup target are in the same lab. Host, NAS, network, or site failure can affect recovery access.
- Backing up the NAS OS does not protect its excluded data disk.
- Deletion protection limits accidental guest deletion; it is not backup protection or immutability.

## Proposed isolated restore drill — not executed

1. Select the monitoring-container archive and confirm the source archive remains intact.
2. Record the backup timestamp and start time. Ensure enough destination capacity.
3. Restore under a new unused guest ID to an isolated network with production-facing access disabled.
4. Start the restored guest and check its filesystem, service process, saved configuration, and local service response.
5. Compare with the source service without allowing the copy to issue duplicate notifications or jobs.
6. Record time to usable service, missing data, and any manual repair required.
7. Retain the drill record; remove the temporary restored guest only after review.

Do not restore over a running guest. This plan is not a script and has not been used to change the lab.

## Improvement backlog

| Work | Acceptance evidence |
| --- | --- |
| Restore test | Isolated guest works; timestamps and validation recorded |
| NAS bootstrap copy | NAS OS/config backup reachable without depending on the NAS VM |
| Passthrough data protection | Separate data backup and sample restore demonstrated |
| Independent copy | Backup accessible after loss of the lab's shared storage |
| Schedule monitoring | Recent run history and a tested failure notification |

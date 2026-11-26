
# IBM AIX Installation and Administration

## 1. Overview

This document provides a general reference for IBM AIX installation, system administration, configuration and operational verification.

Topics include installation preparation, system configuration, device management, storage administration, system health checks and post-installation validation.

## 2. AIX Environment Information

Useful commands to identify the operating system and system configuration.

```bash
oslevel -s
oslevel -r
prtconf
uname -a
hostname
```

IBM Power Systems LPAR information:

```bash
lparstat -i
lsdev -Cc processor
lsdev -Cc memory
```

## 3. Installation Preparation

Before an AIX installation or rebuild:

- Confirm the target server and LPAR configuration.
- Verify hardware and firmware compatibility.
- Confirm installation media or NIM installation resources.
- Review network configuration and required connectivity.
- Verify storage availability and disk allocation.
- Confirm backup and recovery arrangements.
- Obtain required change approvals.
- Document the existing system configuration.

## 4. Installation Methods

AIX installation can be performed using supported installation media or Network Installation Management (NIM).

Common installation approaches:

- New and overwrite installation.
- Preservation installation, where supported and appropriate.
- NIM-based installation.
- Migration installation.

The installation method must be selected according to the target AIX release, source environment, application requirements and IBM-supported upgrade path.

## 5. Post-Installation Validation

Verify operating system level:

```bash
oslevel -s
```

Check installed filesets:

```bash
lslpp -l
```

Check devices:

```bash
lsdev -Cc disk
lsdev -Cc adapter
lsdev -Cc processor
```

Check physical volumes and volume groups:

```bash
lspv
lsvg
lsvg -o
```

Check filesystems:

```bash
df -g
lsfs
```

Check system errors:

```bash
errpt
errpt -a
```

Check boot configuration:

```bash
bootlist -m normal -o
```

## 6. Basic System Administration

### User and Group Management

```bash
lsuser ALL
lsgroup ALL
id username
```

### Filesystem Monitoring

```bash
df -g
lsfs
mount
```

### Process Monitoring

```bash
ps -ef
topas
vmstat 2 5
iostat 2 5
```

### System Resource Monitoring

```bash
lsps -a
svmon -G
lparstat 2 5
```

## 7. Service Management

View system resource groups:

```bash
lssrc -a
```

Check a specific subsystem:

```bash
lssrc -s subsystem_name
```

Start, stop and refresh services only after verifying the service requirements and operational impact.

## 8. System Health Checks

Regular operational checks should include:

- Operating system level verification.
- Filesystem utilization.
- Paging space utilization.
- CPU and memory utilization.
- Disk and adapter status.
- Error report review.
- Critical application service status.
- Backup status.
- Cluster status, where applicable.

## 9. Backup and Recovery Considerations

Before major configuration changes or system maintenance:

- Verify a recent MKSYSB backup.
- Confirm backup completion and accessibility.
- Review alternate disk recovery options.
- Document boot device configuration.
- Ensure recovery procedures are available.

## 10. Troubleshooting

Common diagnostic commands:

```bash
errpt
errpt -a
alog -o -t boot
lsdev -Cc disk
lspv
lsvg -o
df -g
```

Investigate errors, device failures, filesystem issues and resource utilization before implementing corrective actions.

## 11. Important Notes

- Validate commands against the installed AIX release.
- Execute administrative operations using appropriate privileges.
- Review change approvals before production modifications.
- Take required backups before significant changes.
- Test procedures in a non-production environment.
- Use IBM documentation for release-specific installation and upgrade requirements.


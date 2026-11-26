
# IBM AIX LVM and Filesystem Management

## 1. Overview

This document covers IBM AIX Logical Volume Manager (LVM),
physical volume administration, volume group management,
logical volume management and filesystem operations.

## 2. LVM Architecture

The AIX LVM hierarchy:

Physical Disk (PV)
       |
Volume Group (VG)
       |
Logical Volume (LV)
       |
Filesystem

## 3. Physical Volume Management

List physical volumes:

```bash
lspv
```

Display detailed physical volume information:

```bash
lspv hdisk0
```

Check disk attributes:

```bash
lsdev -Cc disk
```

## 4. Volume Group Management

List volume groups:

```bash
lsvg
```

Display volume group details:

```bash
lsvg rootvg
```

Display active volume groups:

```bash
lsvg -o
```

Display logical volumes within a VG:

```bash
lsvg -l rootvg
```

## 5. Logical Volume Management

List logical volumes:

```bash
lslv -l hd5
```

Display logical volume details:

```bash
lslv hd5
```

## 6. Filesystem Management

Display filesystem utilization:

```bash
df -g
```

Display filesystem configuration:

```bash
lsfs
```

Display mounted filesystems:

```bash
mount
```

## 7. Filesystem Extension

Before extending a filesystem:

- Verify current filesystem utilization.
- Identify the underlying logical volume.
- Confirm volume group free space.
- Check the proposed extension size.
- Obtain the required change approval.

Example:

```bash
df -g /data
lsfs /data
lsvg datavg
```

Example filesystem extension:

```bash
chfs -a size=+2G /data
```

Verify:

```bash
df -g /data
lsfs /data
```

## 8. Troubleshooting

Check filesystem utilization:

```bash
df -g
```

Check volume group free space:

```bash
lsvg datavg
```

Check disk and volume group mapping:

```bash
lspv
lsvg -p datavg
lsvg -l datavg
```

## 9. Operational Best Practices

- Verify disk ownership and VG membership before changes.
- Confirm free physical partitions before extending LVs.
- Check filesystem and LV relationships.
- Verify changes after implementation.
- Follow approved change procedures.
- Maintain backup and recovery arrangements.


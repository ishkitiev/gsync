# gsync System

Minimal, reliable offline backup toolkit for Linux systems.
The **gsync system** is a small set of Bash utilities built around `rsync`, designed for safe and predictable mirror backups over LAN.
It focuses on simplicity, offline safety and operational clarity.


## Components

### 1️⃣ gsync

Core synchronization engine.
A safe wrapper around `rsync` that provides:

- Interactive confirmation
- Clear source/destination display
- Explicit `--delete` warning
- LAN-optimized SSH settings
- Progress output
- Automatic `last_sync.log` creation

Designed to be minimal and composable.


### 2️⃣ gsync-menu

Optional interactive menu for predefined synchronization targets.
Features:

- Numbered preset selection
- Last sync date display
- Age indicator (today / X days ago)
- Colored status output
- Uses `gsync` internally

Presets are defined in:


~/.config/gsync/presets.conf


Format:

DESCRIPTION|LOCAL_DESTINATION|REMOTE_SOURCE

### 3️⃣ gsync-health

Health monitoring tool for the backup system.
Provides:

- SMART quick health (all disks)
- SMART detailed inspection
- Mount & free space overview
- Last sync status per preset
- Optional full system report logging

Report file (default):

~/.local/state/gsync/health_report.log


## Design Philosophy

The system is intentionally:

- Simple
- Predictable
- Offline-first
- Easy to restore
- Free of unnecessary storage complexity

It uses:
- ext4 filesystem
- rsync mirror replication
- SMART monitoring
- Manual integrity verification

No RAID, no ZFS, no snapshot systems by default.

## Operational Workflow

When powering on the backup machine:

1. Run synchronization  
gsync-menu
or
gsync <source_path>

2. Run health check  
gsync-health

3. Review status
4. Shutdown and disconnect


## Requirements

- Linux (Debian tested)
- rsync
- OpenSSH
- smartmontools (for gsync-health)

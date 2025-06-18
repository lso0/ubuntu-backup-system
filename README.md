# Ubuntu System Backup Project

This repository contains scripts and documentation for creating complete backups of an Ubuntu system using three different methods.

## System Information
- **OS**: Ubuntu Linux
- **Disk**: 954GB NVMe drive (/dev/nvme0n1)
- **Current Usage**: ~18GB
- **File System**: ext4 with EFI boot partition

## Backup Methods

### 🔧 Configuration Backup (Stored in GitHub)
Captures system configuration, installed packages, and settings - stored directly in the GitHub repository.

**What's included:**
- All installed packages (apt, snap)
- System configuration files
- User settings (.bashrc, .profile, etc.)
- Enabled services
- Hardware information

**Pros:**
- Stored directly in GitHub
- Tiny size (< 1MB)
- Can restore system state on fresh install
- Version controlled

**Usage:**
```bash
./config-backup.sh          # Backup configuration
./quick-restore.sh           # One-command restore on fresh Ubuntu
sudo apt install curl
curl -s https://raw.githubusercontent.com/lso0/ubuntu-backup-system/master/quick-restore.sh -o quick-restore.sh
chmod +x quick-restore.sh
./quick-restore.sh
```

### 1. System Image Backup (`method1-system-image/`)
Creates a complete disk image using `dd` command that captures everything including boot sectors, partitions, and all data.

**Pros:**
- Complete bit-for-bit copy
- Includes boot loader and partition table
- Perfect for disaster recovery

**Cons:**
- Large file size (full disk size)
- Longer backup/restore time

### 2. File System Backup (`method2-filesystem/`)
Uses `rsync` to copy all files while excluding system-specific directories.

**Pros:**
- Smaller backup size
- Faster than disk imaging
- Can be restored to different hardware

**Cons:**
- Requires manual bootloader setup
- May miss some system-specific configurations

### 3. Archive Backup (`method3-archive/`)
Creates compressed tar archives of the entire system excluding temporary/virtual directories.

**Pros:**
- Highly compressed
- Easy to transfer
- Can selectively restore parts

**Cons:**
- Requires manual system reconstruction
- More complex restore process

## Usage

Each method has its own directory with:
- `backup.sh` - Script to create the backup
- `restore.sh` - Script to restore from backup
- `README.md` - Method-specific documentation

## Quick Start

1. Choose your backup method
2. Run the appropriate backup script
3. Store the backup files safely
4. Use restore script when needed

## System Requirements for Restore

- Ubuntu installation media
- Target system with sufficient disk space
- Network access (for downloading dependencies)

Created: $(date)


# storage analysis.md
## 1. `df` - Disk Free
 * **Purpose**: Shows disk space usage for mounted filesystem
 * **Common Arguments**:
   * `-h`: Human-readable format *(e.g., MB, GB)*.
   * `-T`: Shows filesystem type.
   * `-i`: Show inode usage.
 * **Examples**:
```bash
df -h           # Display disk space in human-readable format
df -hT          # Display disk space with filesystem type
df -i           # Show inode usage (useful if running out of inodes
```
## 2. `du` - Disk Usage
 * **Purpose**: Shows disk space usage for directories and files
 * **Common Arguments**:
   * `-h`: Human-readable format.
   * `-s`: Summarize *(only show total size for directories)*.
   * `-a`: Show sizes of all files.
   * `--max-depth=N`: Limit depth of directory tree show.
 * **Examples**:
```bash
du -sh /path/to/dir         # Display total size of a directory in human-readable format
du -ah /path/to/dir         # Show size for each file within a directory
du -sh --max-depth=1
```

## 3. `lsblk` - List Block Devices
 * **Purpose**: List block devices *(disks, partitions, etc.)* and their mount points.
 * **Common Arguments**:
   * `-f`: Show filesystem info *(UUID, type, etc.)*
   * `-o`: Specify columns to display.
 * **Examples**:
```bash
lsblk                       # List all block devices
lsblk -f                    # Show filesyatem type, UUID, and mount points
lsblk -o NAME,SIZE,FSTYPE   # Display selected columns: name, size, filesystem type
```


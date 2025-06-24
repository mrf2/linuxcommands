# find - command
Basic uses of find:
```bash
find -name filename
```
this will look through every directory within our current directory

## Common "-type" options
|Type|Meaning|Example Match|
|---|---|---|
|f|Regular file|`text.txt`, `a.out`etc.|
|d|Directory|Any directory (folder)|
|l|Symbolic link (symlink)|Like `shortcut` to another file|
|c|Character device|e.g., `/dev/tty`|
|b|Block device|e.g., `/dev/sda1`|
|p|Named pipe (FIFO)|Used for interprocess communication|
|s|Socket|e.g., `/var/run/docker.sock`|


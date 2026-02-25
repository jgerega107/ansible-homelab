# Docker role

Simple role to install Docker Container Engine from scratch. Works with Ubuntu/Debian type systems only.

Includes functionality to backup the created Docker system directories via `restic`. Requires a `docker_backup_password` variable set.
You are expected to init the repository yourself.
1. `sudo -s`
2. `set -a` then `source /etc/restic/backup.env`
3. Create SSH keys under root, or ensure the target is mounted.
4. `restic init`

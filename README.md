# Restic Helper Scripts
Helper scripts to use restic more easily on Linux x86, x64 and ARM (such as Truenas Scale or generic Debian/Ubuntu/Arch etc.).
Scripts might work on BSD if you try that by setting OS to BSD.

## How to use
Simple steps:

1. Install `git`
2. Run `git clone https://github.com/christiaangoossens/restic-backup-scripts.git`
3. Go to the `restic-backup-scripts` directory using `cd restic-backup-scripts`
4. Copy `.env.example` to `.env` and fill in your repository path and password for the repository. Alternatively, you can also set `RESTIC_PASSWORD_FILE` in the .env file to use password files instead (or `RESTIC_PASSWORD_COMMAND`). Any restic env vars are supported.
5. Call `./restic` with your arguments to use restic directly with the env. For example `./restic version` should give you the current version.
6. Profit!

### Multiple env files
The scripts also support passing either `-e=PATH` or `--env-file=PATH` as commands to set the env var to a different path.

## Convenience scripts
#### ./init
Initializes the repository that you configured in .env.

#### ./backup
Automatically runs the backup and cleanup as configured. Use .env file to configure paths to be included and retention policy.

#### ./restore-all
Automatically restores the last snapshot to the configured directories. Use .env file to configure paths to be included/restored.

#### ./cleanup
Automatically runs the backup retention policy as configured. Use .env file to configure paths to be included and retention policy.

#### ./file-tree
Gives a file tree of the latest snapshot, only showing files and their sizes

#### ./update
Update the scripts to the latest version.

## Common commands
#### ./restic prune
Manually prune the repository if you have `BACKUP_PRUNE` set to `false`. Make this a regular cron task, probably monthly.

#### ./restic snapshots
View existing snapshots on your repository.

#### ./restic self-update
Update restic binary automatically in `/tmp/restic`.

#### ./restic stats
Show statistics on your repository, such as total size and file count.

## Append-only backups
You might have append-only backups running from one machine using these scripts, while having the `./cleanup` command run from another machine. For this, configure all backup retentions to `0` on the `sending` machine and run `./run-backup` and configure the correct retentions on the `admin` machine and run `./cleanup` there. Please review the [safety considerations documentation](https://github.com/restic/restic/blob/master/doc/060_forget.rst#security-considerations-in-append-only-mode) for more info.
## Restic Helper Scripts
Helper scripts to use restic more easily on Linux x86, x64 and ARM (such as Truenas Scale or generic Debian/Ubuntu/Arch etc.).
Scripts might work on BSD if you try that by setting OS to BSD.

### How to use
Simple steps:

1. Copy `.env.example` to `.env` and fill in your repository path and password for the repository. Alternatively, you can also set `RESTIC_PASSWORD_FILE` in the .env file to use password files instead (or `RESTIC_PASSWORD_COMMAND`). Any restic env vars are supported.
2. Call `./restic` with your arguments to use restic directly with the env. For example `./restic version` should give you the current version.
3. Profit!

### Convenience scripts
#### ./init
Initializes the repository that you configured in .env.

#### ./run-backup
Automatically runs the backup as configured. Use .env file to configure paths to be included and retention policy.

### Common commands
#### ./restic prune
Manually prune the repository if you have `BACKUP_PRUNE` set to `false`. Make this a regular cron task, probably monthly.
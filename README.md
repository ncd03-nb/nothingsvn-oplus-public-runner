# NothingsVN Oplus Public Build Runner

Public GitHub Actions wrapper for two private source forks:

- `build.yml`: OPlus, from `ncd03-nb/nothingsvn_oplus-pt.toolbuild` (`/bp`).
- `xiaomi.yml`: Xiaomi, from `ncd03-nb/nothingsvn_xiaomi-toolbuild` (`/b`).

Source repositories remain private; neither workflow publishes their source tree.

The workflow can only be started manually. It checks out the private source with
a separate read-only SSH deploy key for each source repository, builds inside the temporary GitHub-hosted runner,
and uploads the result using the private source repository's existing scripts.

## Required repository secrets

Configure these under **Settings > Secrets and variables > Actions**:

- `PRIVATE_REPO_DEPLOY_KEY`: private half of an SSH deploy key whose public half
  is installed read-only on `ncd03-nb/nothingsvn_oplus-pt.toolbuild`.
- `XIAOMI_REPO_DEPLOY_KEY`: read-only deploy key for the private Xiaomi fork.
- `TELEGRAM_BOT_TOKEN`
- `TELEGRAM_CHANNEL_ID`
- `GDRIVE_FOLDER_ID`
- `GOOGLE_SERVICE_ACCOUNT_JSON` or `GOOGLE_OAUTH_CREDENTIALS_JSON`, according to
  the authentication method used by the private upload script.

Do not add pull-request triggers or `pull_request_target`. Workflow files and job
logs in this repository are public. Never print secrets or private source files.

## Run

Open **Actions > NothingsVN Oplus ROM Build > Run workflow** and enter the ROM
URLs and build options.

## Xiaomi dependency setup

The Xiaomi workflow installs APT/Python dependencies and Java **before** the
build-space action resizes the runner disk. It keeps 4 GiB on the OS filesystem
and avoids the extra toolchain PPA/GTK development dependency chain. The old
ordering could fail with `mkinitramfs: No space left on device` and dpkg exit 1.

Set `check_only=true` to verify the real dependency installation, private
checkout and writable Drive destination without downloading or building a ROM.

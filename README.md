# NothingsVN Oplus Public Build Runner

Public GitHub Actions wrapper for building the private repository
`ncd03-nb/nothingsvn_oplus-pt.toolbuild` without publishing its source code.

The workflow can only be started manually. It checks out the private source with
a read-only fine-grained token, builds inside the temporary GitHub-hosted runner,
and uploads the result using the private source repository's existing scripts.

## Required repository secrets

Configure these under **Settings > Secrets and variables > Actions**:

- `PRIVATE_REPO_TOKEN`: fine-grained PAT restricted to
  `ncd03-nb/nothingsvn_oplus-pt.toolbuild`, with only **Contents: Read-only**.
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

# git-secrets-pre-commit

A set of pre-commit hook definitions for [git-secrets](https://github.com/awslabs/git-secrets).

`git-secrets` prevents you from committing passwords and other sensitive information to a git repository.

These hooks use Docker to run pre-commit, so it's not necessary to install it manually in the host.

## Usage

### Scan all files

`pre-commit try-repo https://github.com/denis-trofimov/git-secrets-pre-commit-hook git-secrets-scan --verbose --all-files`

### Scans repository including all revisions

`pre-commit try-repo https://github.com/denis-trofimov/git-secrets-pre-commit-hook git-secrets-scan-history --verbose --hook-stage manual`

### Install

Add this to your `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/denis-trofimov/git-secrets-pre-commit-hook
    hooks:
      - id: git-secrets-scan
```

and install `pre-commit install`

### Available hooks

#### git-secrets-scan

Scans all files that are about to be committed.

#### git-secrets-scan-history

Scans repository including all revisions. When a file contains a secret,
the matched text from the file being scanned will be written to stdout and
the script will exit with a non-zero status.
Each matched line will be written with the name of the file that matched,
a colon, the line number that matched, a colon, and then the line of text that matched.

You can trigger it only manually:

`pre-commit try-repo https://github.com/denis-trofimov/git-secrets-pre-commit-hook git-secrets-scan-history --verbose --hook-stage manual`

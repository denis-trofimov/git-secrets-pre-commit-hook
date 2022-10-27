# git-secrets-pre-commit

A set of pre-commit hook definitions for [git-secrets](https://github.com/awslabs/git-secrets).

`git-secrets` prevents you from committing passwords and other sensitive information to a git repository.

These hooks use Docker to run pre-commit, so it's not necessary to install it manually in the host.

## Usage

### Scan all files

```sh
$ pre-commit try-repo https://github.com/denis-trofimov/git-secrets-pre-commit-hook --verbose
[INFO] Initializing environment for https://github.com/denis-trofimov/git-secrets-pre-commit-hook.
===============================================================================
Using config:
===============================================================================
repos:
-   repo: https://github.com/denis-trofimov/git-secrets-pre-commit-hook
    rev: 966ff29df84278142baae49a9f7516ee6827c2ef
    hooks:
    -   id: git-secrets-scan
    -   id: git-secrets-scan-history
===============================================================================
git-secrets: scan new files..............................................Passed
- hook id: git-secrets-scan
- duration: 0.99s
```

### Scans repository including all revisions

```sh
$ pre-commit try-repo https://github.com/denis-trofimov/git-secrets-pre-commit-hook git-secrets-scan-history --verbose --hook-stage manual
===============================================================================
Using config:
===============================================================================
repos:
-   repo: https://github.com/denis-trofimov/git-secrets-pre-commit-hook
    rev: 966ff29df84278142baae49a9f7516ee6827c2ef
    hooks:
    -   id: git-secrets-scan-history
===============================================================================
[INFO] Initializing environment for https://github.com/denis-trofimov/git-secrets-pre-commit-hook.
git-secrets: scans repository including all revisions.......................Passed
- hook id: git-secrets-scan-history
- duration: 1.16s
```

### Install

Add this to your `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/denis-trofimov/git-secrets-pre-commit-hook
    rev: v0.2.0
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

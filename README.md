# git-secrets-pre-commit

A set of pre-commit hook definitions for [git-secrets](https://github.com/awslabs/git-secrets).

`git-secrets` prevents you from committing passwords and other sensitive information to a git repository.

These hooks use Docker to run pre-commit, so it's not necessary to install it manually in the host.

## Usage

Add this to your `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/denis-trofimov/git-secrets-pre-commit
    hooks:
      - id: git-secrets-scan
      - id: git-secrets-commit-msg
      - id: git-secrets-merge-check
```

and install:

```sh
pre-commit install
```

## Available hooks

### git-secrets

Scans all files that are about to be committed.

### git-secrets-commit-msg

Checks the commit message for secrets.

### git-secrets-merge-check

Determines if merging in a commit will introduce tainted history


## Scan all files

`pre-commit run --verbose --all-files git-secrets`

## Scans repository including all revisions

`pre-commit try-repo /home/denis/huma/git-secrets-pre-commit git-secrets-scan-history --verbose --hook-stage manual`

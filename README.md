git-secrets-pre-commit
======================

A set of pre-commit hook definitions for [git-secrets](https://github.com/awslabs/git-secrets).

`git-secrets` prevents you from committing passwords and other sensitive information to a git repository.

These hooks use Docker to run pre-commit, so it's not necessary to install it manually in the host.

### Usage

Add this to your `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/denis-trofimov/git-secrets-pre-commit
    hooks:
      - id: git-secrets-scan
```

and install:

```
pre-commit install -t pre-commit -t commit-msg -t prepare-commit-msg
```

## Available hooks

### git-secrets-scan

Scans all files that are about to be committed.

### git-secrets-commit-msg

Checks the commit message for secrets.

### git-secrets-merge-check

Determines if merging in a commit will introduce tainted history

## Scanning all history

These hooks do not scan the repository history. For that, refer to the [git-secrets docs](https://github.com/awslabs/git-secrets).

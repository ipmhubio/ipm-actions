# IPM GitHub Actions

Composite GitHub Actions for using [IPM (Infrastructure Package Manager)](https://ipmhub.io) in your CI/CD workflows. These actions simplify IPM integration across Windows, Linux, and macOS runners.

## What is IPM?

IPM is an Infrastructure Package Manager that helps teams share, manage, and deploy Infrastructure as Code (IaC) efficiently. It supports Bicep, Terraform, PowerShell, Python, Ansible, and combinations of multiple file types. IPM enables language-agnostic package distribution with nested dependencies and tracked workspace visibility.

## Available Actions

### setup-ipm
Downloads and installs the IPM CLI for your runner's OS and architecture.

```yaml
- uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@v1
  with:
    version: ''        # Optional: specific version without 'v' prefix (default: latest)
    alias-name: 'ipm'  # Optional: custom alias (default: 'ipm')
```

### ipm-init
Creates a new IPM workspace in the specified directory.

```yaml
- uses: ipmhubio/ipm-actions/.github/actions/ipm-init@v1
  with:
    working-directory: '.'  # Optional: workspace directory (default: '.')
```

### ipm-sync
Synchronizes packages in your IPM workspace.

```yaml
- uses: ipmhubio/ipm-actions/.github/actions/ipm-sync@v1
  with:
    working-directory: '.'           # Optional: workspace directory (default: '.')
    sync-mode: 'KeepAllChanges'      # Optional: Clean | KeepChangesOnly | KeepNewFilesOnly | KeepAllChanges
    package-name: ''                 # Optional: specific package to sync
    package-names: ''                # Optional: semicolon/comma/space separated list
  env:
    IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

### ipm-status
Checks the status of packages in your IPM workspace.

```yaml
- uses: ipmhubio/ipm-actions/.github/actions/ipm-status@v1
  with:
    working-directory: '.'  # Optional: workspace directory (default: '.')
    package-name: ''        # Optional: specific package to check
  env:
    IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

## Quick Start

```yaml
name: Deploy Infrastructure

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup IPM
        uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@v1
      
      - name: Sync packages
        uses: ipmhubio/ipm-actions/.github/actions/ipm-sync@v1
        with:
          working-directory: ./infrastructure
          sync-mode: KeepAllChanges
        env:
          IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
      
      - name: Check status
        uses: ipmhubio/ipm-actions/.github/actions/ipm-status@v1
        with:
          working-directory: ./infrastructure
        env:
          IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

## Examples

### Initialize a new workspace

```yaml
- name: Setup IPM
  uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@v1

- name: Initialize workspace
  uses: ipmhubio/ipm-actions/.github/actions/ipm-init@v1
  with:
    working-directory: ./new-project
```

### Sync specific packages

```yaml
- name: Sync network packages
  uses: ipmhubio/ipm-actions/.github/actions/ipm-sync@v1
  with:
    package-names: 'avm-bicep/virtual-networks; avm-bicep/storage-accounts'
    sync-mode: Clean
  env:
    IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

### Multi-platform testing

```yaml
jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
    steps:
      - uses: actions/checkout@v4
      - uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@v1
      - uses: ipmhubio/ipm-actions/.github/actions/ipm-sync@v1
        env:
          IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

## Authentication

All actions that interact with IPMHub (sync, status) require authentication via the `IPM_CLIENT_SECRETS` environment variable. Store your client secret as a GitHub repository secret and pass it through the workflow.

```yaml
env:
  IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

For multiple client secrets, separate them with spaces.

## Sync Modes

- `Clean`: Removes all local changes and downloads fresh packages
- `KeepChangesOnly`: Preserves modified files, removes new files
- `KeepNewFilesOnly`: Keeps new files, removes modified files
- `KeepAllChanges`: Preserves all local modifications (default)

## Prerequisites

- GitHub Actions runner (Ubuntu, macOS, or Windows)
- IPMHub account with client secrets configured
- Repository secret `IPM_CLIENT_SECRETS` configured

## Support

- Documentation: https://docs.ipmhub.io
- Website: https://ipmhub.io
- Issues: https://github.com/ipmhubio/ipm-actions/issues

## License

MIT License - see [LICENSE](LICENSE) file for details.
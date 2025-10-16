# Security Policy

## Reporting Security Issues

If you discover a security vulnerability in these GitHub Actions, please report it to:

**security@ipmhub.io**

Please do not report security vulnerabilities through public GitHub issues.

## What to Include

Help us address the issue quickly by including:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Any suggested fixes (optional)

## Response Timeline

We'll acknowledge your report within 48 hours and provide updates as we investigate and address the issue.

## Security Best Practices

When using these actions in your workflows:

### Handle Secrets Properly

Always store IPM client secrets as GitHub repository secrets:

```yaml
env:
  IPM_CLIENT_SECRETS: ${{ secrets.IPM_CLIENT_SECRETS }}
```

Never hardcode secrets in workflow files or commit them to your repository.

### Keep Actions Updated

Use specific version tags or SHA references for production workflows:

```yaml
# Recommended: use specific version
uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@v1.0.0

# Or: pin to specific commit
uses: ipmhubio/ipm-actions/.github/actions/ipm-setup@abc123...
```

### Review Workflow Logs

GitHub Actions logs may contain sensitive information. Review logs before sharing them publicly when troubleshooting issues.

### Limit Permissions

Use the principle of least privilege for workflow permissions:

```yaml
permissions:
  contents: read
```

## Scope

This security policy covers:
- The GitHub Actions defined in this repository
- The integration between these actions and IPM CLI
- Workflow configuration and secret handling

For security issues with IPM CLI itself, contact security@ipmhub.io directly.
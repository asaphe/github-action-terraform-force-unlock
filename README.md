# github-action-terraform-force-unlock

A composite GitHub Action that detects and force-unlocks Terraform state locks.

## Usage

```yaml
- uses: asaphe/github-action-terraform-force-unlock@v1
  with:
    working-directory: devops/terraform/my-module
    workspace: production
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `working-directory` | Directory to run Terraform in | Yes | - |
| `workspace` | Terraform workspace name | No | Current workspace |

## How It Works

1. Probes for a state lock by attempting `force-unlock` with a dummy ID
2. If a lock is detected, extracts the real lock ID from the error output
3. Force-unlocks using the real lock ID
4. Verifies the unlock was successful

This avoids running `terraform plan` (which would fail on required variables) just to detect a lock.

## License

Apache 2.0 - See [LICENSE](LICENSE) for details.

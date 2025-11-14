# Setup Instructions for POC Repository

## Quick Start

1. **Create a new GitHub repository** (or use a test repository you control)
   ```bash
   # Create a new directory
   mkdir atlas-action-poc
   cd atlas-action-poc
   git init
   ```

2. **Copy the POC files to your repository**
   ```bash
   # Copy the .github/workflows directory
   cp -r POC/.github .github
   
   # Copy the README
   cp POC/README.md POC-README.md
   ```

3. **Commit and push**
   ```bash
   git add .
   git commit -m "Add POC workflows for command injection vulnerability"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

4. **Trigger the workflows**
   - Go to the "Actions" tab in your GitHub repository
   - Select any of the POC workflows
   - Click "Run workflow" (for workflow_dispatch) or push to main (for push trigger)

## What to Expect

When the workflows run, you should see:

1. **The workflow will fail** (because we're using fake project IDs/cluster names)
2. **BUT** the injected commands will execute **before** the failure
3. **Check the workflow logs** to see:
   - The injected commands executing
   - Files being created in `/tmp/`
   - Environment information being printed

## Understanding the Output

### Successful Injection Indicators

- Files created in `/tmp/` (e.g., `/tmp/poc-success.txt`)
- Echo statements from injected commands appearing in logs
- System information (whoami, pwd, etc.) printed by injected commands

### Why the Workflow Fails

The workflows intentionally use invalid project IDs and cluster names. The `atlas` CLI commands will fail, but **the injected commands execute first** because of shell command chaining with `;`.

## Testing Different Injection Vectors

Each workflow demonstrates a different vulnerable input:

- `poc-delete-project.yml` - `delete-project-id`
- `poc-create-cluster.yml` - `create-cluster-name`
- `poc-setup-username.yml` - `username` in setup
- `poc-setup-password.yml` - `password` in setup
- `poc-comprehensive.yml` - Multiple vectors at once

## Safety Reminders

⚠️ **Only run these in a test repository you control!**

- These POCs use benign commands (echo, touch, etc.)
- In a real attack, malicious commands could:
  - Steal secrets
  - Modify code
  - Access other repositories
  - Install backdoors

## Next Steps

After confirming the vulnerability:

1. **Report to MongoDB** (if not already done)
2. **Document the findings** with screenshots/logs
3. **Wait for a fix** before using the action in production
4. **Review other GitHub Actions** you use for similar issues

## Cleanup

After testing, you can delete the POC workflows:

```bash
rm -rf .github/workflows/poc-*.yml
git add .
git commit -m "Remove POC workflows after testing"
git push
```

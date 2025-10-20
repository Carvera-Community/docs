# GitHub Actions Workflows

## Cascade Merge Workflow

The `cascade-merge.yml` workflow automatically cascades merges from the `main` branch to the `dev` branch.

### How it works

1. **Trigger**: Runs automatically when changes are pushed to the `main` branch
2. **Conflict Detection**: Checks if merging `main` into `dev` would cause conflicts
3. **Two Paths**:
   - **No Conflicts**: Automatically merges `main` into `dev` and pushes the changes
   - **Conflicts Detected**: Creates a conflict branch and opens a PR for manual resolution

### Features

- ✅ Automatic conflict detection using `git merge-tree`
- ✅ Creates `dev` branch if it doesn't exist
- ✅ Non-fast-forward merges to preserve merge history
- ✅ Automatic PR creation with detailed conflict information
- ✅ Proper Git configuration for automated commits
- ✅ Comprehensive error handling and logging

### Conflict Resolution Process

When conflicts are detected:

1. A new branch is created with the format: `conflict-merge-main-to-dev-YYYYMMDD-HHMMSS`
2. The merge is attempted to create conflict markers in the files
3. A PR is automatically created with:
   - Clear title indicating manual intervention is needed
   - Detailed description of what happened
   - List of files with conflicts
   - Instructions for resolution
   - Appropriate labels (`conflict-resolution`, `automated`)

### Manual Testing

You can manually trigger the workflow:

1. Go to the "Actions" tab in your GitHub repository
2. Select "Cascade Merge Main to Dev" workflow
3. Click "Run workflow" button
4. Choose the branch and click "Run workflow"

### Requirements

- The workflow requires `GITHUB_TOKEN` with `contents: write` and `pull-requests: write` permissions
- These permissions are automatically granted for workflows in the same repository

### Troubleshooting

- **Workflow fails to create PR**: Ensure the repository has GitHub CLI (`gh`) available or the token has sufficient permissions
- **Merge conflicts not detected**: The workflow uses `git merge-tree` which may not catch all types of conflicts; manual verification may be needed
- **Dev branch not created**: Check that the workflow has write permissions to the repository

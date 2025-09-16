# Clone Action

This repository contains GitHub Actions workflows for deploying applications to Fly.io.

## Workflows

### 1. Install Dependencies (`install.yml`)

This workflow logs into a Fly.io machine and installs dependencies using pnpm.

**Usage:**
1. Go to the Actions tab in your GitHub repository
2. Select "Install Dependencies on Fly.io Machine"
3. Click "Run workflow"
4. Provide the required inputs:
   - `fly_api_token`: Your Fly.io API token
   - `fly_app_name`: Name of the Fly.io app to install dependencies on
   - `github_repo_url`: GitHub repository URL to pull from
   - `github_token`: GitHub Personal Access Token for repository access
   - `custom_dependencies`: Custom dependencies to install (e.g., "remotion @remotion/cli @remotion/player framer-motion prismjs react-syntax-highlighter @types/prismjs")
   - `git_user_email`: Git user email for commits (default: "needwareofficial@gmail.com")
   - `git_user_name`: Git user name for commits (default: "needware")
   - `commit_message`: Commit message for dependency updates (default: "Update package.json dependencies")
   - `client_id`: Client ID for state tracking (optional, defaults to "install-client")

**What it does:**
- Checks if the Fly.io app is running
- Logs into the Fly.io machine via SSH
- Installs Node.js and pnpm if not already installed
- Clones/pulls the latest code from the GitHub repository
- Installs base dependencies using `pnpm install`
- Installs custom dependencies specified in the input (e.g., remotion, framer-motion, etc.)
- Configures Git user settings
- Adds package.json to git and commits changes
- Pushes changes to the remote repository
- Provides detailed logging and error handling
- Sends status callbacks for tracking

**Example Custom Dependencies:**
```
remotion @remotion/cli @remotion/player framer-motion prismjs react-syntax-highlighter @types/prismjs
```

### 2. Clone, Push, and Deploy (`clone.yml`)

Complete workflow that clones a repository, creates a new GitHub repo, and deploys to Fly.io.

### 3. Restart and Deploy (`restart.yml`)

Workflow for restarting and redeploying an existing Fly.io application.

## Requirements

- Fly.io account and API token
- GitHub Personal Access Token with appropriate permissions
- Existing Fly.io app (for install workflow)

## Setup

1. Set up your Fly.io API token as a GitHub secret or provide it when running the workflow
2. Ensure your Fly.io app is running before using the install workflow
3. Make sure your GitHub token has access to the repositories you want to work with

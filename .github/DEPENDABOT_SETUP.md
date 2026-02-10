# Dependabot Setup for Forked Repositories

## Issue: Dependabot PRs Not Being Created

If you've forked this repository and notice that Dependabot is not creating pull requests for dependency updates, this is expected behavior. **GitHub disables Dependabot by default on forked repositories** to prevent automated update spam.

## Solution: Enable Dependabot in Repository Settings

To enable Dependabot on your fork, follow these steps:

### 1. Navigate to Repository Settings
1. Go to your forked repository on GitHub
2. Click on **Settings** (top right of the repository page)
3. In the left sidebar, scroll down to **Code security and analysis**

### 2. Enable Dependabot Features
In the Code security and analysis section, you'll find three Dependabot options:

#### Dependabot alerts
- **Purpose**: Notifies you about known security vulnerabilities in your dependencies
- **Action**: Click **Enable** to turn on alerts

#### Dependabot security updates
- **Purpose**: Automatically creates PRs to update vulnerable dependencies
- **Action**: Click **Enable** to turn on security updates
- **Note**: This requires "Dependabot alerts" to be enabled first

#### Dependabot version updates
- **Purpose**: Automatically creates PRs to keep dependencies up to date (uses `.github/dependabot.yml` config)
- **Action**: Click **Enable** to turn on version updates
- **Note**: This is the setting needed for regular dependency updates

### 3. Verify Configuration
Once enabled, Dependabot will use the existing `.github/dependabot.yml` configuration file in this repository. The current configuration:
- Monitors both root (`/`) and frontend (`/frontend`) npm dependencies
- Runs daily checks for updates
- Targets the `develop` branch for PRs
- Adds the `dependencies` label to PRs

### 4. Manually Trigger an Update (Optional)
If you want to trigger Dependabot immediately after enabling:
1. Go to **Insights** → **Dependency graph** → **Dependabot**
2. Click **Check for updates** to manually trigger a scan

## Expected Behavior After Enabling

Once Dependabot is enabled:
- It will scan your dependencies according to the daily schedule
- It will create separate PRs for dependency updates
- PRs will be created against the `develop` branch
- Each PR will be labeled with `dependencies`
- The repository owner (`bkimminich`) will be added as a reviewer

## Troubleshooting

### Still Not Seeing PRs?
1. **Check Dependabot logs**: Go to Insights → Dependency graph → Dependabot and look for error messages
2. **Verify branch exists**: Make sure the `develop` branch exists in your fork
3. **Check for paused updates**: If Dependabot says "updates are paused," merge an existing PR or manually trigger an update
4. **Review ignored packages**: The config ignores certain package versions (see `.github/dependabot.yml`)

### Additional Resources
- [GitHub Docs: Dependabot on forks](https://docs.github.com/en/code-security/tutorials/secure-your-dependencies/dependabot-quickstart-guide)
- [Troubleshooting Dependabot errors](https://docs.github.com/en/code-security/how-tos/secure-your-supply-chain/troubleshoot-dependency-security/troubleshooting-dependabot-errors)

## Why Is Dependabot Disabled on Forks?

GitHub disables Dependabot on forks by default because:
- Forks are often used for contributing back to the original project
- Automatic dependency updates on forks could create unnecessary noise
- Users typically want to sync with the upstream repository instead
- It prevents spam from automated PRs on forks that may not be actively maintained

If you're actively maintaining this fork and want to keep dependencies up to date independently from the upstream repository, you should enable Dependabot as described above.

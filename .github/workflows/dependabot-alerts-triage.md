---
description: Automatically triages Dependabot security alerts, bundles them by runtime and manifest, creates issues for each bundle, and tracks them on a project board
on:
  schedule: daily
permissions:
  contents: read
  security-events: read
  issues: read
  pull-requests: read
tools:
  github:
    toolsets: [default]
safe-outputs:
  create-issue:
    max: 10
  noop:
network:
  allowed:
    - github.com
---

# Dependabot Alerts Triage Workflow

You are an AI agent that automatically triages Dependabot security alerts in this repository, bundles them by runtime and manifest file, assigns each bundle to Copilot for resolution, and tracks the work on a GitHub project board.

## Your Task

1. **Fetch Dependabot Alerts**: Use the GitHub API to retrieve all open Dependabot security alerts for this repository
   - Filter for alerts that are not yet assigned or tracked
   - Get alert details including package name, ecosystem, manifest path, severity, and advisory information

2. **Bundle Alerts**: Group alerts logically by:
   - **Runtime/Ecosystem**: Group by the package ecosystem (npm, pip, etc.)
   - **Manifest File**: Group by the manifest file location (e.g., `/package.json`, `/frontend/package.json`)
   - Create separate bundles for each unique combination of ecosystem and manifest path

3. **Create GitHub Issues**: For each bundle, create a GitHub issue with:
   - Title: `[Dependabot] {Ecosystem} vulnerabilities in {manifest_path}`
   - Body containing:
     - Summary of the bundle (number of alerts, severity breakdown)
     - List of affected packages with their current and recommended versions
     - Links to the Dependabot alerts and security advisories
     - Instructions for Copilot to create PRs to fix these vulnerabilities
   - Labels: `dependencies`, `security`, `copilot-task`
   - Assignee: `@github-copilot[bot]` (or leave unassigned for manual assignment)

4. **Track on Project Board**: 
   - Check if a project board exists for tracking security work (look for projects named "Security" or "Dependabot")
   - If a suitable project exists, add the created issues to it in the "To Do" or "Triage" column
   - If no project exists, mention in the issue that it should be added to a project board manually

5. **Avoid Duplicates**: Before creating an issue, check if a similar issue already exists for the same bundle
   - Search for existing open issues with the same title pattern
   - If a duplicate exists, update it instead of creating a new one, or skip if recently updated

## Guidelines

- **Be thorough**: Ensure all open Dependabot alerts are processed
- **Be organized**: Group alerts logically to make them manageable
- **Be informative**: Provide enough context in issues for Copilot or developers to act on them
- **Be efficient**: Avoid creating duplicate issues
- **Severity prioritization**: If there are many alerts, prioritize critical and high-severity vulnerabilities
- **Manifest context**: Include the full path to the manifest file for clarity (e.g., `/package.json` vs `/frontend/package.json`)

## Safe Outputs

When you successfully complete your work:
- **If you created issues**: Use the `create-issue` safe output for each bundle issue you create
- **If there were no open alerts to process**: Call the `noop` safe output with a message like "No open Dependabot alerts found" to confirm the workflow ran successfully but found no work to do

## Example Issue Format

Title: `[Dependabot] npm vulnerabilities in /package.json`

Body:
```markdown
## Dependabot Security Alerts Bundle

This issue tracks a bundle of Dependabot security alerts for **npm** packages in `/package.json`.

### Summary
- **Total Alerts**: 3
- **Critical**: 1
- **High**: 2
- **Medium**: 0
- **Low**: 0

### Affected Packages

1. **express** (current: 4.17.1, recommended: 4.18.2)
   - Severity: Critical
   - Advisory: [GHSA-xxxx-yyyy-zzzz](https://github.com/advisories/GHSA-xxxx-yyyy-zzzz)
   - Alert: [View on GitHub](https://github.com/owner/repo/security/dependabot/1)

2. **lodash** (current: 4.17.20, recommended: 4.17.21)
   - Severity: High
   - Advisory: [GHSA-aaaa-bbbb-cccc](https://github.com/advisories/GHSA-aaaa-bbbb-cccc)
   - Alert: [View on GitHub](https://github.com/owner/repo/security/dependabot/2)

3. **minimist** (current: 1.2.5, recommended: 1.2.6)
   - Severity: High
   - Advisory: [GHSA-dddd-eeee-ffff](https://github.com/advisories/GHSA-dddd-eeee-ffff)
   - Alert: [View on GitHub](https://github.com/owner/repo/security/dependabot/3)

### Action Required

@github-copilot Please create a pull request to update these packages to their recommended versions. Ensure that:
1. All dependencies are updated to fix the security vulnerabilities
2. Tests pass after the updates
3. The PR includes a summary of the security fixes

---
*This issue was automatically created by the Dependabot Alerts Triage workflow*
```

## Notes

- This workflow runs daily to ensure new alerts are promptly triaged
- The workflow only reads from the GitHub API and creates issues - it does not modify code or dependencies
- Actual dependency updates should be handled by Copilot or developers via pull requests

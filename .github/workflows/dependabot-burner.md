---
name: Dependabot Burner
description: Burns down open Dependabot pull requests.

on:
  schedule: daily
  skip-if-no-match: 'is:pr is:open author:app/dependabot'
  workflow_dispatch:

permissions:
  issues: read
  pull-requests: read
  contents: read
  security-events: read

safe-outputs:
  create-issue:
    expires: 7d
    title-prefix: "[dependabot burner] "
    assignees: [copilot]
    max: 20
    group: false
---

# Dependabot Burner

- Find all open Dependabot PRs and add them to the project.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Add bundle issues to the project, and assign them to Copilot.

# gitsynctest

A Git repository for testing Grafana 13 Git Sync functionality with the Azure Managed Grafana team.

## Overview

This repository is structured to be used as a Git Sync source for Grafana 13. Dashboards stored as JSON files under the `grafana/` directory will be automatically synced to and from a connected Grafana instance.

## Repository Structure

```
grafana/
  bug-bash-overview.json          ← Root-level overview dashboard for the bug bash
  AzureManagedGrafana/
    team-dashboard.json           ← Team-specific dashboard (inside Grafana folder)
    metrics-overview.json         ← Metrics overview dashboard (inside Grafana folder)
```

- Files at the top level of `grafana/` appear in the root of Grafana dashboards.
- Subdirectories (e.g., `AzureManagedGrafana/`) map to Grafana folders of the same name.

## Connecting Grafana 13 Git Sync

1. In Grafana, go to **Administration → Provisioning**.
2. Click **Configure Git Sync**.
3. Enter your GitHub Personal Access Token and this repository's details:
   - **Repository URL**: `https://github.com/Jeralan/gitsynctest`
   - **Branch**: `main`
4. Follow the prompts to begin synchronization.

For full setup instructions, see the [Grafana Git Sync documentation](https://grafana.com/docs/grafana/latest/observability-as-code/provision-resources/git-sync-setup/).

## Dashboard JSON Format

Each dashboard file uses the Grafana 13 API resource format:

```json
{
  "apiVersion": "dashboard.grafana.app/v1beta1",
  "kind": "Dashboard",
  "metadata": {
    "name": "unique-dashboard-name"
  },
  "spec": {
    "title": "My Dashboard",
    "schemaVersion": 41,
    "panels": []
  }
}
```

## Bug Bash Scenarios

| Scenario | Steps |
|---|---|
| Edit from Grafana UI | Open a dashboard → edit a panel → save → push to branch → open PR → merge |
| Edit from GitHub | Edit a `.json` file in this repo → commit → verify change appears in Grafana |
| Folder operations | Create/rename/delete a subfolder under `grafana/` → verify Grafana folder structure updates |
| PR preview | Make a change via Grafana UI, open a PR, and check the before/after dashboard screenshot comment |

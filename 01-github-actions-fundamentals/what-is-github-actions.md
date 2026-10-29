# What Is GitHub Actions?

## 1. Introduction

GitHub Actions is a CI/CD and workflow automation platform integrated into GitHub. It allows teams to automate software development tasks using workflow files written in YAML.

These workflows can run in response to repository events, on a schedule, or through manual execution.

Common use cases include:

- Running automated tests.
- Building and packaging applications.
- Performing code quality and security checks.
- Building and publishing Docker images.
- Deploying applications to cloud platforms.
- Automating repository maintenance tasks.

---

## 2. Why Do We Need GitHub Actions?

In a manual software delivery process, developers or DevOps engineers may repeatedly execute the same commands whenever code changes.

This can introduce inconsistent results, missed steps, and unnecessary delays.

GitHub Actions allows teams to define these tasks once and execute them automatically when the configured conditions are met.

For example, a team can configure a workflow to run unit tests whenever a pull request targets the `main` branch.

---

## 3. How GitHub Actions Works

A typical workflow follows this sequence:

1. A repository event occurs.
2. GitHub evaluates the workflow triggers.
3. A workflow run is created.
4. Jobs are scheduled on eligible runners.
5. The runner executes the job's steps.
6. GitHub records the execution logs and results.

A workflow consists of jobs, and each job contains one or more steps. Steps can execute shell commands or call reusable actions.

---

## 4. Example Workflow

Create this file:

`.github/workflows/python-tests.yml`

```yaml
name: Python Tests

on:
  pull_request:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Display Python version
        run: python --version

      - name: Display repository files
        run: ls -la
```

### What does this workflow do?

- `name`: gives the workflow a readable name.
- `on`: defines the events that trigger it.
- `pull_request`: runs when a pull request targets `main`.
- `workflow_dispatch`: allows a manual run from GitHub's Actions interface.
- `permissions`: limits the workflow's repository token to read-only content access.
- `jobs`: defines the work to execute.
- `runs-on`: selects an Ubuntu runner.
- `steps`: lists tasks executed by the job.
- `uses`: invokes a reusable action.
- `with`: passes configuration to an action.
- `run`: executes a shell command.

This is an introductory workflow. It prepares Python and displays the repository files; it does not yet run application tests.

---

## 5. GitHub Actions in a DevOps Pipeline

A larger CI/CD workflow may perform the following tasks:

1. Check out application source code.
2. Install dependencies.
3. Run tests.
4. Perform code quality and security checks.
5. Build a Docker image.
6. Publish the image to a container registry.
7. Deploy the application to a target environment.

These stages must be explicitly configured, and deployments should use suitable permissions, secrets, and approval rules.

---

## 6. Under the Hood

GitHub processes repository events and evaluates matching workflow definitions. It then schedules jobs on eligible runners.

The runner executes the configured steps and reports their results to GitHub.

Important details:

- Each job normally runs in its own execution environment.
- Steps within a job share the job's workspace.
- Shell variables do not automatically persist between separate shell steps.
- Repository files are normally checked out explicitly using an action such as `actions/checkout`.
- A failed step generally causes the job to fail unless failure handling is configured.
- Secrets and token permissions must be configured deliberately.

---

## 7. Interview Questions

### Q1. What is GitHub Actions?

GitHub Actions is a workflow automation platform integrated into GitHub. It is commonly used to implement CI/CD pipelines that build, test, package, and deploy applications.

### Q2. What is a workflow?

A workflow is an automated process defined in a YAML file under `.github/workflows/`. It contains triggers, jobs, and steps.

### Q3. What is a runner?

A runner is the execution environment that runs workflow jobs. GitHub-hosted runners are managed by GitHub, while self-hosted runners are managed by the organization or team.

### Q4. Does GitHub Actions automatically test every code change?

No. The repository must contain a workflow configured with appropriate triggers and test steps.

### Q5. What is the difference between GitHub Actions and Jenkins?

GitHub Actions is integrated into GitHub and uses repository-based workflow definitions. Jenkins is a separate automation server that teams install or use through a managed service. Both can implement CI/CD pipelines.

---

## 8. Key Takeaway

GitHub Actions turns repository events into automated workflows. The team defines what should happen, when it should happen, and which execution environment should perform the work.
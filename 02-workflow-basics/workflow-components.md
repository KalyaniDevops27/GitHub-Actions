# GitHub Actions Workflow Components

## 1. Overview

GitHub Actions is an automation platform used to build, test, and deploy applications. A workflow is defined in a YAML file stored inside the `.github/workflows/` directory of a GitHub repository.

A workflow consists of events, jobs, and steps. Jobs execute on runners, and steps can run shell commands or reusable actions.

---

## 2. Workflow

A workflow is a configurable automated process.

A repository can contain multiple workflows for different purposes, such as:

- Running tests when a Pull Request is opened.
- Building a Docker image after code is merged.
- Deploying an application after a release is created.
- Running scheduled maintenance tasks.

Example workflow filename:

```text
.github/workflows/ci.yml
```

---

## 3. Events and Triggers

An event is an activity that can trigger a workflow.

Common triggers include:

| Trigger | Purpose |
|---|---|
| `push` | Run when commits are pushed to matching branches |
| `pull_request` | Run for configured Pull Request activities |
| `workflow_dispatch` | Allow a manual workflow run |
| `schedule` | Run according to a cron schedule |

Example:

```yaml
on:
  push:
    branches:
      - main
  workflow_dispatch:
```

---

This configuration allows the workflow to run when a push occurs on `main`, or when someone manually starts it.

---

## 4. Jobs

A job is a group of steps that execute on the same runner.

A workflow can contain multiple jobs, such as:

- `test`: execute automated tests.
- `build`: build the application.
- `deploy`: deploy the application.

By default, independent jobs can run in parallel. Use `needs` to declare job dependencies.

Example:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Run a test command
        run: echo "Testing application"

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Build application
        run: echo "Building application"
```

Here, `build` waits for `test` to complete successfully under the default job conditions.

---

## 5. Runners

A runner is the machine or execution environment that runs a job.

GitHub-hosted runners are managed by GitHub. Self-hosted runners are machines that you configure and maintain.

Example:

```yaml
runs-on: ubuntu-latest
```

This requests a GitHub-hosted Ubuntu runner.

A separate job normally receives its own execution environment. Do not assume files are automatically shared between jobs.

---

## 6. Steps

A step is an individual task within a job.

Steps run in sequence by default. A step can execute a shell command using `run` or invoke an action using `uses`.

Example:

```yaml
steps:
  - name: Show working directory
    run: pwd

  - name: Print a message
    run: echo "GitHub Actions is working"
```

Steps within a job can access the job's workspace, but ordinary shell variables do not automatically persist between separate `run` steps.

---

## 7. Actions

An action is a reusable component that performs a specific task.

One common example is `actions/checkout`, which checks out repository content into the runner's workspace.

Example:

```yaml
steps:
  - name: Checkout repository
    uses: actions/checkout@v4
```

Use `run` for commands you write yourself and `uses` to invoke an action.

For production workflows, review third-party actions and pin them according to your organization's security policy.

---

## 8. Complete Example

```yaml
name: Lesson 2 - Workflow Components

on:
  push:
    branches:
      - main
      - feature/lesson-2-components
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  learn-components:
    name: Explore workflow components
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Show runner operating system
        run: uname -a

      - name: Show current directory
        run: pwd

      - name: List repository files
        run: ls -la

      - name: Print success message
        run: echo "Workflow components practice completed"
```

---

## 9. Under the Hood

1. GitHub receives a repository event.
2. GitHub evaluates workflow triggers and applicable branch filters.
3. A matching workflow run is created.
4. GitHub schedules eligible jobs.
5. A runner executes each job and processes its steps.
6. Logs and the final result are reported to GitHub.

---

## 10. DevOps Example

A typical CI workflow might:

1. Check out source code.
2. Install dependencies.
3. Run tests.
4. Build the application.
5. Build a Docker image.
6. Publish the image to a container registry.

A deployment workflow may then deploy the image to a test or production environment after the required checks and approvals.

---

## 11. Interview Questions

### Q1. What is a workflow in GitHub Actions?

A workflow is an automated process defined in a YAML file. It contains triggers and one or more jobs.

### Q2. What is the difference between a job and a step?

A job groups steps and runs on a runner. A step is an individual command or action within that job.

### Q3. What is a runner?

A runner is the machine or execution environment that executes a job.

### Q4. What is the difference between `run` and `uses`?

`run` executes a shell command or script. `uses` invokes a reusable action or workflow component.

### Q5. Do jobs run sequentially by default?

No. Independent jobs can run in parallel. Use `needs` to define dependencies.

### Q6. Why is `actions/checkout` commonly used?

It checks out repository content into the runner's workspace so later steps can access the source code.

### Q7. Are files automatically shared between jobs?

No. Separate jobs normally run in separate environments. Use artifacts or another explicit transfer mechanism when files must be shared.

---

## Official References

- [Understanding GitHub Actions](https://docs.github.com/en/actions/get-started/understand-github-actions)
- [Workflows](https://docs.github.com/en/actions/concepts/workflows-and-actions/workflows)
- [Workflow syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [Events that trigger workflows](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows)

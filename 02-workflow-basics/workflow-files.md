# GitHub Actions Workflow Files

## 1. What Is a Workflow File?

A GitHub Actions workflow file is a YAML file that defines an automated process for a repository. It specifies when the workflow should run, which jobs should execute, and what steps those jobs should perform.

For example, a workflow can automatically run tests whenever a developer pushes code or opens a pull request.

Workflow files are stored in:

```text
.github/workflows/
```

Common workflow file extensions include `.yml` and `.yaml`.

---

## 2. Why Do We Need Workflow Files?

Without automation, developers or DevOps engineers may need to run repetitive tasks manually.

Workflow files help teams automate tasks such as:

- Running application tests.
- Checking code quality.
- Building Docker images.
- Publishing artifacts.
- Deploying applications.
- Running scheduled maintenance tasks.

This makes the software delivery process more consistent and repeatable.

---

## 3. Basic Workflow Structure

A workflow commonly contains the following components:

| Component | Purpose |
|---|---|
| `name` | Gives the workflow a readable name. |
| `on` | Defines the events that trigger the workflow. |
| `permissions` | Controls the workflow's access through its GitHub token. |
| `jobs` | Defines the jobs to execute. |
| `runs-on` | Specifies the runner environment for a job. |
| `steps` | Lists the tasks performed within a job. |
| `uses` | Invokes an action. |
| `run` | Executes shell commands. |

Not every workflow needs every optional field.

---

## 4. Example Workflow

Create a file named `workflow-files.yml` inside `.github/workflows/`.

```yaml
name: Workflow Files Practice

on:
  push:
    branches:
      - feature/workflow-basics
  workflow_dispatch:

permissions:
  contents: read

jobs:
  inspect-repository:
    name: Inspect Repository
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Display current directory
        run: pwd

      - name: List repository files
        run: ls -la

      - name: Print completion message
        run: echo "Workflow file practice completed"
```

### Explanation

**`name`**

Provides a readable name that appears in the GitHub Actions interface.

**`on`**

Configures the events that trigger the workflow. Here, it runs when a push targets `feature/workflow-basics` or when someone manually starts the workflow using the GitHub interface.

**`permissions`**

Grants the workflow's `GITHUB_TOKEN` read access to repository contents. This is sufficient for this example and follows the principle of least privilege.

**`jobs`**

Defines the work that GitHub Actions needs to execute.

**`runs-on`**

Selects an Ubuntu-hosted runner.

**`steps`**

Defines the individual tasks that run in sequence within the job.

**`uses: actions/checkout@v4`**

Uses the checkout action to make the repository's files available to subsequent steps.

**`run`**

Executes shell commands on the runner.

---

## 5. How a Workflow Runs Internally

1. A developer pushes a commit to GitHub.
2. GitHub evaluates whether the event matches the workflow's trigger configuration.
3. GitHub creates a workflow run when the configured event qualifies.
4. The job is assigned to an available compatible runner.
5. The runner executes the steps in their defined order.
6. GitHub collects the logs and records the result.

A workflow run can succeed, fail, be cancelled, or be skipped depending on its execution and conditions.

---

## 6. Common Mistakes

### Placing the workflow in the wrong directory

GitHub Actions expects repository workflow files under `.github/workflows/`. A YAML file placed only in a documentation folder will not be discovered as a workflow.

### Invalid YAML indentation

YAML uses indentation to represent structure. Use consistent spaces and avoid tabs for indentation.

### Forgetting the checkout action

Commands that inspect repository files may not see those files unless the workflow checks out the repository.

### Incorrect branch filters

If a push targets a branch that does not match the configured branch filter, the workflow will not start from that push event.

### Expecting a local commit to run the workflow

Committing locally does not itself start a GitHub-hosted workflow. You need to push the commit or trigger the workflow through another configured event.

---

## 7. DevOps Example

A development team configures a workflow to run automated tests on every pull request targeting `main`.

The workflow checks out the proposed code, installs the required dependencies, and runs tests. The team can configure branch protection to require successful checks before merging.

This helps catch problems before they reach the main branch.

---

## 9. Interview Questions

**Q1. What is a GitHub Actions workflow file?**

It is a YAML file that defines the events, jobs, and steps used to automate tasks in a GitHub repository.

**Q2. Where should workflow files be stored?**

Inside the repository's `.github/workflows/` directory.

**Q3. What is the difference between a workflow and a workflow run?**

A workflow is the configured automation. A workflow run is one execution of that automation in response to a qualifying event or manual trigger.

**Q4. Why do we use `actions/checkout`?**

It checks out the repository code so subsequent steps can access the files.

**Q5. What does `runs-on: ubuntu-latest` mean?**

It requests a GitHub-hosted runner using the Ubuntu environment specified by the `ubuntu-latest` label.

**Q6. What is the difference between `run` and `uses`?**

`run` executes shell commands, while `uses` invokes an action that provides reusable functionality.

**Q7. Does creating a workflow file automatically run it?**

No. It must be in the expected directory and a configured trigger must occur, or the workflow must be started manually if a manual trigger is configured.

---

## Key Takeaway

A workflow file defines the automation, triggers determine when it runs, and runners execute its jobs. Understanding this separation is essential when designing reliable CI/CD pipelines.
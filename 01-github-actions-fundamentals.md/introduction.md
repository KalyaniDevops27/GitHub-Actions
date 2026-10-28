# Introduction to GitHub Actions

## 1. What is GitHub Actions?

GitHub Actions is a CI/CD automation platform integrated with GitHub. It allows teams to automate software development workflows by defining events, jobs, and steps in YAML files.

It can automate tasks such as:

- Running application tests
- Building and packaging applications
- Building and publishing Docker images
- Validating Terraform configuration
- Deploying applications to AWS or Kubernetes
- Running scheduled maintenance and security checks

---

## 2. Why do we need GitHub Actions?

In a traditional workflow, developers or DevOps engineers may need to execute build, test, and deployment commands manually.

This can be repetitive, time-consuming, and inconsistent.

GitHub Actions makes these procedures repeatable by executing configured tasks automatically when the appropriate events occur.

**Important:** Automation improves consistency, but it does not guarantee application correctness. The quality of the result depends on the checks and safeguards implemented in the workflow.

---

## 3. How GitHub Actions works

A typical workflow follows this sequence:

1. A developer pushes a commit or opens a pull request.
2. GitHub receives the event.
3. GitHub evaluates workflow triggers and conditions.
4. Eligible jobs are scheduled on compatible runners.
5. Runners execute the configured steps.
6. GitHub reports the results and execution logs.

Workflows are generally stored in:

`.github/workflows/`

---

## 4. Under the hood

When a developer executes `git push origin main`, Git transfers new commits to the remote repository.

GitHub updates the branch reference and processes the resulting push event. It evaluates applicable workflow definitions and determines whether their trigger rules match.

For an eligible workflow, GitHub schedules its jobs. Each job executes on an assigned runner. The runner prepares its environment and executes the defined steps in order, reporting their status and logs.

The runner does not automatically receive every file or secret in the repository. The workflow must explicitly check out code when needed, and access to credentials depends on the workflow's permissions and configuration.

GitHub-hosted runners are supplied by GitHub. Self-hosted runners are managed by the organization using them.

---

## 5. Integration with DevOps tools

| Tool | How GitHub Actions integrates |
|---|---|
| Git | Responds to repository events and commit changes |
| Linux / Bash | Executes shell commands on compatible runners |
| Docker | Builds, tests, tags, and publishes container images |
| AWS | Authenticates and deploys resources or applications |
| Terraform | Validates infrastructure code and runs plans and approved applies |
| Kubernetes | Deploys new application versions and checks rollout status |
| Prometheus / Grafana | Can participate in monitoring and notification workflows through appropriate integrations |

GitHub Actions orchestrates the automation; each integrated tool performs its own specialized function.

---

## 6. CI vs CD

**Continuous Integration (CI):** Automatically builds and tests code changes so that problems are discovered early.

**Continuous Delivery:** Keeps software ready for release, with production deployment potentially requiring approval.

**Continuous Deployment:** Automatically deploys qualifying changes to production after the required checks pass.

These practices are related, but they are not interchangeable.

---

## 7. Advantages

- Automates repetitive development tasks.
- Integrates directly with GitHub repositories and pull requests.
- Supports Linux, Windows, and macOS runners.
- Provides reusable actions and workflows.
- Integrates with cloud providers, containers, and deployment platforms.
- Provides execution logs for troubleshooting.

---

## 8. Limitations and considerations

- Poorly designed workflows can introduce deployment risks.
- Hosted runners have usage limits and can incur costs depending on the plan and runner type.
- Secrets and permissions require careful handling.
- Third-party actions must be reviewed and maintained.
- CI/CD automation cannot replace good testing, monitoring, or release controls.

---

## 9. Interview questions

**Q1. What is GitHub Actions?**

GitHub Actions is a CI/CD automation platform that runs configured workflows in response to events such as pushes, pull requests, manual triggers, or schedules.

**Q2. Why would a company use GitHub Actions?**

To automate testing, builds, security checks, packaging, and deployment, reducing repetitive manual work and improving consistency.

**Q3. What is the difference between Git and GitHub Actions?**

Git is a version control system. GitHub Actions is an automation platform that can respond to events in GitHub repositories and execute defined workflows.

**Q4. Can GitHub Actions deploy an application to AWS?**

Yes. A workflow can authenticate to AWS using a suitable method, such as OpenID Connect, and invoke deployment tools with appropriately scoped permissions.

**Q5. Does GitHub Actions automatically run every script in a repository?**

No. Tasks must be defined in workflow files, and the configured events and conditions determine when eligible workflows run.

**Q6. What is a runner?**

A runner is the machine or execution environment that executes a workflow job's steps.

---

## 10. Summary

GitHub Actions connects source-code events with repeatable automation. Understanding workflows, triggers, jobs, steps, actions, and runners provides the foundation for building secure and reliable CI/CD pipelines.
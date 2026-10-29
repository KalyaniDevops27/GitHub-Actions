# CI vs CD

## 1. Introduction

CI/CD is a software delivery approach that uses automation to validate code changes and make application releases more consistent and repeatable.

CI stands for Continuous Integration.

CD can stand for Continuous Delivery or Continuous Deployment. These concepts are related, but they do not mean exactly the same thing.

---

## 2. What Is Continuous Integration (CI)?

Continuous Integration is the practice of frequently integrating code changes into a shared repository and validating those changes using automated checks.

A typical CI pipeline performs the following tasks:

1. Checks out the source code.
2. Installs application dependencies.
3. Builds or compiles the application.
4. Runs automated tests.
5. Performs code quality or security checks.

The purpose is to identify problems early, while changes are still relatively small and easier to investigate.

### Example

A developer opens a pull request to merge a Python application change into `main`.

GitHub Actions runs the configured tests. If the tests fail, the developer investigates and fixes the problem before the change is merged, assuming the repository requires the checks to pass.

---

## 3. What Is Continuous Delivery?

Continuous Delivery extends the automated build and validation process so that the application can be released reliably whenever the team chooses.

The pipeline may prepare a versioned artifact, publish a Docker image, deploy to a staging environment, and perform validation checks.

Production deployment typically requires an intentional release action or approval, although the exact process depends on the team's configuration.

---

## 4. What Is Continuous Deployment?

Continuous Deployment automatically releases every change that passes the required pipeline checks to production.

It requires sufficient automated testing, monitoring, deployment safeguards, and recovery mechanisms because a manual production approval is not required for each release.

Continuous Deployment is not simply automatic deployment to a test environment. The term specifically refers to automatic production releases.

---

## 5. CI vs Continuous Delivery vs Continuous Deployment

| Area | Continuous Integration | Continuous Delivery | Continuous Deployment |
|---|---|---|---|
| Main purpose | Validate code changes | Keep releases ready | Automatically release to production |
| Automated tests | Commonly included | Commonly included | Commonly included |
| Artifact creation | Often included | Included in the release process | Included in the release process |
| Production release | Not required | Usually requires a deliberate release action | Automatic after required checks pass |
| Primary focus | Code integration and quality | Release readiness | End-to-end automated release |

---

## 6. Example DevOps Pipeline

Consider an application packaged using Docker and deployed to a cloud environment.

1. A developer opens a pull request.
2. GitHub Actions checks out the code and runs tests.
3. Required code quality and security checks execute.
4. After merging, the pipeline builds a versioned Docker image.
5. The image is published to a container registry.
6. The deployment pipeline releases that image to the target environment.
7. Health checks and monitoring help the team validate the deployment.

The production release may require approval under Continuous Delivery or happen automatically under Continuous Deployment.

---

## 7. How GitHub Actions Supports CI/CD

GitHub Actions allows teams to define workflows in YAML files under `.github/workflows/`.

Workflows can respond to events such as `pull_request` and `push`, run shell commands, use reusable actions, and execute jobs on hosted or self-hosted runners.

A CI workflow might run tests for a pull request. A separate workflow or a later job may build an image and deploy it after the appropriate conditions are met.

GitHub Actions provides the automation platform, but the team must design the pipeline, tests, security controls, and deployment process.

---

## 8. Under the Hood

During CI, GitHub evaluates the configured trigger, schedules a job, and runs the validation steps on a runner. The job reports its outcome to GitHub.

During CD, the workflow may package the validated application, publish the artifact, authenticate to the deployment target, and execute deployment steps.

Important distinctions:

- Passing tests does not guarantee that an application is free of defects.
- A successful build does not mean the application has been deployed.
- Publishing an image is different from running that image in a target environment.
- Production deployment should use least-privilege permissions and appropriate release safeguards.
- Rollback and monitoring strategies help teams respond to failed deployments.

---

## 9. Interview Questions

### Q1. What is CI?

CI is the practice of frequently integrating code changes and validating them through automated checks such as builds and tests.

### Q2. What is the difference between Continuous Delivery and Continuous Deployment?

Continuous Delivery keeps software ready to release, usually with a deliberate production-release action. Continuous Deployment automatically releases every change that passes the required checks to production.

### Q3. Can GitHub Actions be used for both CI and CD?

Yes. It can run tests and builds, publish artifacts, and deploy applications when the workflows and required access are configured.

### Q4. Does a successful CI pipeline mean the application is deployed?

No. CI validates changes. Deployment requires additional configured stages that release the application to an environment.

### Q5. Why are automated tests important in CI/CD?

They provide fast feedback about known failure conditions and reduce the risk of releasing changes that break existing functionality. Their effectiveness depends on the quality and coverage of the tests.

### Q6. How would you explain CI/CD in a DevOps interview?

"I use CI to automatically validate code changes through builds, tests, and quality checks. I use a CD pipeline to package the validated application and make it ready for release or deploy it to the target environment. Depending on the release model, production deployment can require approval or happen automatically after all required checks pass."

---

## 10. Key Takeaway

CI helps teams validate changes continuously. Continuous Delivery keeps software ready to release, while Continuous Deployment automatically releases qualifying changes to production.

A reliable CI/CD pipeline combines automation with testing, secure access, deployment safeguards, monitoring, and recovery planning.
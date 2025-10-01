# Comprehensive Guide to GitHub Actions Workflows

## Table of Contents
1. Introduction to GitHub Actions
2. Workflow Structure
3. Events and Triggers
4. Jobs and Steps
5. Runners
6. Actions
7. Inputs, Outputs, and Environment Variables
8. Caching
9. Secrets and Security
10. Common Use Cases
11. Debugging and Best Practices
12. References

---

## 1. Introduction to GitHub Actions
GitHub Actions is a CI/CD platform that automates software workflows directly in your GitHub repository. You can build, test, and deploy your code based on events like pushes, pull requests, or scheduled times.

## 2. Workflow Structure
A workflow is defined in a YAML file under `.github/workflows/`. Example:
```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: npm test
```

## 3. Events and Triggers
- **on:** Specifies what events trigger the workflow (e.g., `push`, `pull_request`, `schedule`).
- You can filter events by branch, path, or type.

## 4. Jobs and Steps
- **jobs:** Each workflow can have multiple jobs that run in parallel (unless specified otherwise).
- **steps:** Each job contains steps, which can run commands or use actions.

## 5. Runners
- **runs-on:** Specifies the environment (e.g., `ubuntu-latest`, `windows-latest`).
- GitHub-hosted runners are free for public repos; private repos have usage limits.

## 6. Actions
- **uses:** Reusable code or community actions (e.g., `actions/checkout@v4`).
- **run:** Execute shell commands.
- You can create your own actions (JavaScript, Docker, or Composite).

## 7. Inputs, Outputs, and Environment Variables
- **inputs:** Pass parameters to actions (especially composite actions).
- **outputs:** Share data between steps/jobs.
- **env:** Set environment variables for steps/jobs.
- Inputs in composite actions are referenced as `${{ inputs.input_name }}`.

## 8. Caching
- Use `actions/cache` to speed up builds by storing dependencies.
- Example for Composer:
```yaml
- uses: actions/cache@v4
  with:
    path: vendor
    key: composer-cache-${{ hashFiles('**/composer.lock') }}
    restore-keys: composer-cache-
```
- Caching Composer's cache directory is safer than caching `vendor`.

## 9. Secrets and Security
- Store sensitive data in GitHub Secrets (`Settings > Secrets and variables > Actions`).
- Reference secrets in workflows: `${{ secrets.SECRET_NAME }}`.
- Never hardcode secrets in workflow files.

## 10. Common Use Cases
- **CI/CD:** Build, test, and deploy code.
- **Linting:** Run code quality checks.
- **Release Automation:** Publish packages or create releases.
- **Notifications:** Post comments or send messages on events.

## 11. Debugging and Best Practices
- Use `actions/upload-artifact` to save logs or build outputs.
- Add `continue-on-error: true` for non-blocking steps.
- Use `jobs.<job_id>.needs` to control job dependencies.
- Keep workflows modular and DRY (reuse actions).
- Use matrix builds for testing across multiple environments.

## 12. References
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Actions Marketplace](https://github.com/marketplace?type=actions)
- [GitHub Actions Examples](https://github.com/actions)

---

This guide covers the essentials and best practices for working with GitHub Actions workflows. For advanced scenarios, consult the official documentation and explore community actions in the marketplace.

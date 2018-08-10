# Git Guidelines

## Summary

This document has two main purposes:
* Document the direction around git practices within the organization
* Provide guidance and resources for common git tasks

## Checklist
* [ ] Use [Trunk-based Development](docs/development-process.md)
* [ ] Use the correct [Github Configuration](docs/github-configuration.md)
* [ ] Follow the [PR Submission Checklist](#pr-submission-checklist)
* [ ] Follow the [PR Review Checklist](#pr-review-checklist)

### PR Submission Checklist
* [ ] Motivations are satisfied
* [ ] Added new Unit Tests
* [ ] All Commits are squashed into a single commit
* [ ] Commit Message is in the correct format
* [ ] Code is **Up to Date** with latest `develop`
* [ ] Format files: `npm run format`
* [ ] Run Linting: `npm run affected:lint --base=upstream/develop`
* [ ] Run Tests: `npm run affected:test --base=upstream/develop`
* [ ] Run E2E Tests: `npm run affected:e2e --base=upstream/develop`

### PR Review Checklist
* [ ] Does the PR description follow Standards?
* [ ] Does the CI process pass?
* [ ] Do the changes produce the desired change?
* [ ] Are there any unintended changes in behavior?
* [ ] Are the coding standards met?
* [ ] Is the code maintainable?

## Development Process
* [Development Process - Trunk-based Development](docs/development-process.md)
* [Github Configuration](docs/github-configuration.md)
* [PR Process](docs/pr-process.md)
* [PR Format](docs/pr-format.md)

## Git Resources
* [Git Cheatsheet](docs/git-cheatsheet.md)
* [Commit Format](docs/commit-format.md)

## External Resources

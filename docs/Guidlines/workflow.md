# Pull Request Workflow
## Introduction

This document outlines the workflow for contributing to our project using Pull Requests. Pull Requests are a fundamental part of our collaborative development process, allowing team members and contributors to propose changes, discuss them, and eventually merge them into the main codebase.


## Workflow Overview

Our Pull Request Workflow follows these main steps:

-   Fork the Repository: If you're not a project collaborator, fork the repository to create your own copy.

-   Clone the Repository: Clone your forked repository to your local development environment.

-   Create a Feature Branch: Before making any changes, create a new branch for your work. Branch names should be descriptive of the feature or fix you're implementing.

-   Make Changes: Make your code changes, following our coding style and guidelines. Commit your changes to your feature branch regularly.

-   Open a Pull Request: When your feature or fix is complete, open a Pull Request from your feature branch to the main branch of the main repository. Provide a clear title and description of your changes.

-   Code Review: Team members will review your code, provide feedback, and discuss any necessary changes. Be responsive to feedback and update your branch accordingly.

-   Continuous Integration: Automated tests will run on your branch to ensure that your changes do not introduce regressions or errors.

-   Merge: Once your Pull Request has been approved and passes all tests, it can be merged into the main branch.

-   Cleanup: After merging, delete your feature branch and ensure your local and remote repositories are up-to-date.

## Detailed Workflow Steps
1. Fork the Repository

-   If you're not a project collaborator, click the "Fork" button on the top right of the repository page to create a fork in your own GitHub account.

2. Clone the Repository

```bash
git clone git@github.com:EpitechPromo2026/B-CPP-500-PAR-5-1-rtype-julian.emery.git
cd B-CPP-500-PAR-5-1-rtype-julian.emery
```

3. Create a Feature Branch

```bash
# Create a new branch and switch to it
git checkout -b feature/your-feature-name
```

4. Make Changes

-   Make your code changes following our coding guidelines.
    Commit your changes with descriptive commit messages:

```bash
git commit -m "[ADD]: your feature description"
```

- Additionnaly, you may use the commit body to add additonnal informations.

5. Open a Pull Request

-   Push your feature branch to your forked repository:

```bash
git push origin feature/your-feature-name
```
-    Visit the main repository on GitHub and click the "New Pull Request" button.

6. Code Review

-   Participate in the code review process, addressing feedback and making necessary changes to your code.

7. Continuous Integration

-   Automated tests and checks will run on the dev and main branch. Ensure all checks pass.

8. Merge

-   Once approved by reviewers and all checks pass, a project collaborator will merge your Pull Request into the main branch.

9. Cleanup

-   After merging, delete your feature branch both locally and remotely.

## Contribution Guidelines

-   Follow our coding style and guidelines as outlined in our [CONTRIBUTING.md](CONTRIBUTE.md) document.

## Code of Conduct

-   Please review and adhere to our project's [Code of Conduct](CODE_OF_CONDUCT.md) at all times.
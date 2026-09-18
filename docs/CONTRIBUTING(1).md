# Contributing Guidelines

Thank you for your interest in contributing to this project! This guide explains how to set up your development environment, make changes, open a pull request, and participate in code reviews.

Please read this document before submitting your first contribution.

---

## 1. Code of Conduct

All contributors are expected to:

- Be respectful and professional.
- Communicate clearly and constructively.
- Welcome feedback and different perspectives.
- Avoid personal attacks, harassment, or discriminatory behavior.
- Focus discussions on the code, requirements, and project goals.

---

## 2. Before You Start

Before making changes:

1. Read the project `README.md`.
2. Follow the [Environment Setup Runbook](./ENVIRONMENT_SETUP_RUNBOOK.md).
3. Check existing issues and pull requests.
4. If an issue already exists for your proposed change, review the discussion before starting work.
5. For significant changes, open or discuss an issue first so the approach can be agreed upon.

Avoid working on large changes without first confirming that they fit the project's direction.

---

## 3. Repository Setup

Clone the repository:

```bash
git clone <REPOSITORY_URL>
cd <PROJECT_DIRECTORY>
```

Follow the project's environment setup instructions in:

```text
ENVIRONMENT_SETUP_RUNBOOK.md
```

Verify that the project runs successfully before making changes.

---

## 4. Create a Branch

Do not make changes directly on the `main` branch.

Create a separate branch:

```bash
git checkout main
git pull origin main
git checkout -b <type>/<short-description>
```

Recommended branch naming:

```text
feature/add-user-search
fix/login-validation
docs/update-setup-guide
refactor/api-client
test/add-auth-tests
chore/update-dependencies
```

Common branch types:

| Type | Use For |
|---|---|
| `feature/` | New functionality |
| `fix/` | Bug fixes |
| `docs/` | Documentation changes |
| `refactor/` | Code restructuring without behavior changes |
| `test/` | Adding or improving tests |
| `chore/` | Maintenance and tooling |

Keep branch names short and descriptive.

---

## 5. Make Your Changes

When implementing a change:

- Keep the change focused on the issue.
- Follow the existing project structure.
- Follow existing coding conventions.
- Avoid unrelated refactoring.
- Reuse existing utilities and components when appropriate.
- Add comments only when they explain non-obvious behavior.
- Do not commit generated files unless the project requires them.
- Do not commit credentials, API keys, passwords, or other secrets.

Prefer small, understandable changes over large changes that are difficult to review.

---

## 6. Code Quality

Before opening a pull request, make sure your code:

- Is readable and maintainable.
- Uses meaningful variable and function names.
- Does not contain unnecessary duplication.
- Handles expected error conditions.
- Does not introduce obvious security issues.
- Follows the project's existing architecture.
- Does not introduce unnecessary dependencies.

If the repository already provides formatting, linting, or static-analysis tools, use them rather than introducing new tools.

---

## 7. Tests

Every behavior-changing contribution should include appropriate tests when practical.

Tests should:

- Cover the new or changed behavior.
- Cover important edge cases.
- Avoid relying on external services unless required.
- Be deterministic and repeatable.
- Follow the existing test structure.

Run the project's test suite before opening a PR.

Examples:

```bash
npm test
```

or:

```bash
npm run test
```

For Python projects:

```bash
pytest
```

or:

```bash
python -m pytest
```

Use the commands documented by the repository if they differ.

---

## 8. Linting and Formatting

Run the project's configured linting and formatting commands.

Common examples:

```bash
npm run lint
npm run format
```

Python examples:

```bash
ruff check .
black .
```

Do not introduce a new formatter or linter configuration without discussing it with maintainers.

---

## 9. Commit Guidelines

Write clear commit messages that explain what changed.

Good examples:

```text
Add user search endpoint
Fix validation for login requests
Update contributor documentation
Add tests for payment validation
```

Avoid vague messages such as:

```text
changes
fix
update
asdf
final
```

Keep commits focused. Avoid mixing unrelated changes into a single commit.

If the project has an established commit-message convention, follow that convention.

---

## 10. Keep Your Branch Updated

Before opening a pull request, update your branch with the latest changes from `main`.

```bash
git checkout main
git pull origin main
git checkout <your-branch>
```

Then use the repository's preferred approach to integrate the latest changes.

If the project uses merge:

```bash
git merge main
```

If the project uses rebase:

```bash
git rebase main
```

If you are unsure which approach to use, follow the repository's existing contribution practices or ask a maintainer.

---

## 11. Pull Request Requirements

Every pull request should clearly explain:

### What changed?

Provide a short summary of the implementation.

### Why was it changed?

Explain the issue, requirement, or problem being addressed.

### How was it tested?

List the tests or verification steps performed.

### Additional considerations

Mention anything reviewers should know, such as:

- Database changes
- API changes
- Configuration changes
- Dependency changes
- Breaking changes
- Migration requirements
- Known limitations

---

## 12. Pull Request Template

Use the following structure when creating a pull request:

```markdown
## Summary

<!-- Briefly describe what this PR changes. -->

## Related Issue

<!-- Link the issue this PR addresses. -->

Closes #<issue-number>

## Changes

- Change 1
- Change 2
- Change 3

## Testing

- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual testing
- [ ] Linting
- [ ] Formatting

### Test Details

<!-- Describe the commands and/or manual steps used to verify the changes. -->

## Screenshots

<!-- Include screenshots or recordings when they help explain UI changes. -->

## Breaking Changes

<!-- Describe any breaking changes, or write "None". -->

## Additional Notes

<!-- Add any information reviewers should know. -->
```

---

## 13. PR Checklist

Before submitting a pull request, verify:

- [ ] The PR addresses a specific issue or requirement.
- [ ] The branch is up to date with `main`.
- [ ] The code follows project conventions.
- [ ] Tests have been added or updated where appropriate.
- [ ] Existing tests pass.
- [ ] Linting passes.
- [ ] Formatting passes.
- [ ] Documentation has been updated when necessary.
- [ ] No secrets or credentials are included.
- [ ] No unnecessary files are committed.
- [ ] The PR description explains what changed and why.
- [ ] Breaking changes are clearly documented.
- [ ] Screenshots or other evidence are included for relevant UI changes.

---

## 14. How Code Review Works

Pull requests are reviewed before they are merged.

Reviewers may check:

1. Correctness
2. Readability
3. Maintainability
4. Test coverage
5. Security
6. Performance where relevant
7. Compatibility with existing functionality
8. Documentation
9. Scope of the change

Review comments are intended to improve the code and should be treated as part of the development process.

---

## 15. Responding to Review Comments

When a reviewer requests a change:

1. Understand the requested change.
2. Ask for clarification if necessary.
3. Make the appropriate update.
4. Run relevant tests.
5. Push the changes to the same branch.
6. Reply to the review comment with a brief explanation.

Example:

```text
Updated the validation logic and added a test for the empty-input case.
```

If you disagree with a suggestion, explain your reasoning respectfully and provide technical context or evidence.

Do not resolve disagreements by changing code without understanding the underlying concern.

---

## 16. Review Expectations for Contributors

Contributors should expect reviewers to focus on the code rather than the person.

Good review discussions are:

- Specific
- Technical
- Constructive
- Respectful
- Focused on project requirements

A requested change does not necessarily mean the contribution is rejected. It usually means the reviewer wants the implementation clarified, corrected, or improved before merging.

---

## 17. Review Expectations for Reviewers

Reviewers should:

- Review the actual scope of the PR.
- Explain why a change is needed when the reason is not obvious.
- Distinguish required changes from optional suggestions.
- Avoid unnecessary style preferences when the project already has established conventions.
- Consider tests and documentation.
- Review security-sensitive changes carefully.
- Keep feedback respectful and actionable.

Reviewers should avoid blocking a PR over minor preferences that do not materially affect the project.

---

## 18. Addressing Review Feedback

After making requested changes:

```bash
git status
git diff
```

Review your changes before committing.

Run the relevant tests again:

```bash
npm test
```

or:

```bash
pytest
```

Commit and push the changes:

```bash
git add .
git commit -m "Address review feedback"
git push
```

The pull request will automatically update with the new commit(s).

---

## 19. Handling Merge Conflicts

If your branch has conflicts with `main`, update your branch using the project's preferred workflow.

First check the current state:

```bash
git status
```

Resolve conflicts carefully.

After resolving them:

```bash
git add .
```

Then complete the merge or rebase according to the workflow being used.

Run the full relevant test suite after resolving conflicts.

Never blindly accept all incoming or local changes without reviewing the resulting code.

---

## 20. Documentation Changes

Documentation contributions are welcome.

Update documentation when a code change affects:

- Installation
- Configuration
- API usage
- User workflows
- Development setup
- Testing
- Troubleshooting

Keep documentation:

- Clear
- Accurate
- Concise
- Easy for new contributors to follow

If setup requirements change, update both the relevant documentation and `ENVIRONMENT_SETUP_RUNBOOK.md` where appropriate.

---

## 21. Dependency Changes

Before adding or upgrading a dependency:

1. Confirm that it is necessary.
2. Check whether the functionality already exists in the project.
3. Consider maintenance and security implications.
4. Update the appropriate lock file.
5. Run the relevant tests.
6. Explain the dependency change in the PR.

Avoid adding dependencies for functionality that can reasonably be implemented using existing project dependencies or standard library features.

---

## 22. Security Issues

Do not report security vulnerabilities through a public GitHub issue if the repository provides a private security-reporting process.

If a security policy exists, follow:

```text
SECURITY.md
```

If no security policy exists, contact the project maintainers through the project's designated private communication channel.

Never publish:

- Passwords
- API keys
- Access tokens
- Private keys
- Database credentials
- Personal information
- Exploit details that could put users at risk

---

## 23. Issue Reporting

Before opening an issue:

1. Search existing issues.
2. Confirm that the problem still exists on the latest supported version.
3. Collect relevant logs and error messages.
4. Remove sensitive information from logs.

A useful bug report should include:

```text
Description:
Expected behavior:
Actual behavior:
Steps to reproduce:
Environment:
Relevant logs:
Possible workaround:
```

For feature requests, explain:

```text
Problem:
Proposed solution:
Use case:
Alternatives considered:
```

---

## 24. What Makes a Good Contribution?

A good contribution generally:

- Solves a clearly defined problem.
- Is focused and appropriately scoped.
- Includes tests when applicable.
- Follows existing project conventions.
- Includes necessary documentation.
- Has a clear PR description.
- Is easy for another developer to review and maintain.

---

## 25. After Your PR Is Approved

Once the required reviews and automated checks are complete, the PR can be merged according to the repository's merge policy.

After merging:

```bash
git checkout main
git pull origin main
```

You can optionally delete the local feature branch:

```bash
git branch -d <your-branch>
```

---

## 26. Quick Contribution Workflow

For experienced contributors:

```bash
# Get the latest code
git checkout main
git pull origin main

# Create a branch
git checkout -b feature/<short-description>

# Make changes
# Add/update tests

# Review changes
git status
git diff

# Run tests/linting
npm test
npm run lint

# Commit
git add .
git commit -m "Describe the change"

# Push
git push -u origin feature/<short-description>

# Open a Pull Request on GitHub
```

Use the project's actual test, lint, and formatting commands if they differ.

---

## 27. Final Contributor Checklist

Before submitting your contribution:

- [ ] I read the README.
- [ ] I followed the environment setup instructions.
- [ ] I created a separate branch.
- [ ] My changes are focused on the intended issue.
- [ ] I followed existing coding conventions.
- [ ] I added or updated tests where appropriate.
- [ ] All relevant tests pass.
- [ ] Linting passes.
- [ ] Formatting passes.
- [ ] Documentation is updated where necessary.
- [ ] I did not commit secrets or credentials.
- [ ] I reviewed my own diff.
- [ ] My PR description explains what changed and why.
- [ ] I documented breaking changes if applicable.
- [ ] I am ready to respond to code review feedback.

---

## 28. Thank You

Thank you for contributing to the project.

Every contribution—whether it is code, documentation, testing, bug reporting, or review feedback—helps improve the project for everyone.

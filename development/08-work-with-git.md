# Work with Git

## Quick Setup

Check the current branch.

```bash
git branch
```

Switch to the development branch.

```bash
git checkout develop
```

Download the latest changes.

```bash
git pull origin develop
```

Check modified files.

```bash
git status
```

Stage your changes.

```bash
git add .
```

Or stage specific files.

```bash
git add app.php

git add sidebar.php
```

Commit your changes.

```bash
git commit -m "Describe your changes"
```

Push your commit.

```bash
git push
```

When your work is complete:

1. Push to `develop`.
2. Create a Pull Request.
3. Review the changes.
4. Merge into `main`.

---

# Complete Guide

Git tracks every change made to the project. Using a consistent workflow helps prevent lost work, merge conflicts, and accidental changes to the production branch.

---

## Step 1 — Update Your Local Repository

Before making changes, switch to the development branch.

```bash
git checkout develop
```

Download the latest changes.

```bash
git pull origin develop
```

### Why?

Always start with the latest version of the project.

This reduces the chance of merge conflicts and ensures you're building on the newest code.

---

## Step 2 — Make Your Changes

Edit the project files.

Example:

```text
sidebar.php

index.php

login.php
```

After making changes, check what has changed.

```bash
git status
```

Example:

```text
modified: sidebar.php

modified: login.php
```

---

## Step 3 — Stage Your Changes

Stage every modified file.

```bash
git add .
```

Or stage only selected files.

```bash
git add sidebar.php

git add login.php
```

### What does `git add` do?

`git add` tells Git which changes should be included in the next commit.

Changes that are not staged are ignored when you commit.

---

## Step 4 — Commit Your Changes

Create a commit.

```bash
git commit -m "Improve sidebar navigation"
```

### Good Commit Messages

```text
Fix login validation

Add user profile page

Update dashboard layout

Refactor authentication logic
```

Avoid messages like:

```text
Update

Changes

Fix

Test
```

A clear commit message helps everyone understand what changed without opening the code.

---

## Step 5 — Push Your Changes

Upload your commits.

```bash
git push
```

If this is a new branch:

```bash
git push -u origin develop
```

Your changes are now available on GitHub.

---

## Step 6 — Create a Pull Request

After finishing your work:

Open GitHub.

Navigate to:

```text
Repository

Pull Requests

New Pull Request
```

Choose:

```text
Base Branch

main
```

```text
Compare Branch

develop
```

Review the changes.

If everything looks correct, create the Pull Request.

### Why use Pull Requests?

A Pull Request allows changes to be reviewed before they reach the production branch.

This keeps `main` stable.

---

## Step 7 — Merge into Main

Only project maintainers should merge Pull Requests.

Before merging:

* Review the code.
* Check that the application works.
* Resolve any merge conflicts.
* Verify that automated tests (if available) pass.

Merge the Pull Request.

GitHub automatically updates the `main` branch.

---

## Step 8 — Update Your Local Repository Again

After the Pull Request is merged:

Update your local repository.

```bash
git checkout main

git pull origin main
```

Switch back to development.

```bash
git checkout develop

git merge main
```

This keeps your local branches synchronized.

---

# Verification

Check the current branch.

```bash
git branch
```

Check repository status.

```bash
git status
```

Check recent commits.

```bash
git log --oneline --decorate --graph -10
```

Confirm:

* Your working tree is clean.
* Your changes are committed.
* Your changes have been pushed to GitHub.

---

# Common Problems

## Forgot to Pull Before Starting

Run:

```bash
git pull origin develop
```

If Git reports conflicts, resolve them before continuing.

---

## Accidentally Committed the Wrong File

Unstage the file.

```bash
git restore --staged filename.php
```

Or amend the last commit if it has not been pushed yet.

---

## Push Rejected

Another developer has pushed new changes.

Update your branch.

```bash
git pull --rebase origin develop
```

Resolve any conflicts.

Continue the rebase.

```bash
git rebase --continue
```

Then push again.

```bash
git push
```

---

## Merge Conflict

Git marks conflicting sections inside the file.

Example:

```text
<<<<<<< HEAD

Your changes

=======

Incoming changes

>>>>>>> develop
```

Edit the file to keep the correct code.

Save the file.

Stage it.

```bash
git add filename.php
```

Continue the merge or rebase.

```bash
git merge --continue
```

or

```bash
git rebase --continue
```

---

# Best Practices

* Work on `develop`, never directly on `main`.
* Pull before starting new work.
* Commit small, focused changes.
* Write clear commit messages.
* Push regularly.
* Review Pull Requests before merging.
* Keep `main` production-ready at all times.

---

# Summary

After completing this guide:

* You understand the project's Git workflow.
* You know how to commit and push changes safely.
* You know how to create Pull Requests.
* You understand how changes reach the production branch.
* You know how to resolve common Git issues.

Next:

➡ **09 - Collaborate with Other Developers**

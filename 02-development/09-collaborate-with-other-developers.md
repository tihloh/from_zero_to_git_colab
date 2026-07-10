# Collaborate with Other Developers

## Quick Setup

Before starting work.

```bash
git checkout develop

git pull origin develop
```

Create a feature branch (recommended).

```bash
git checkout -b feature/login-page
```

Work on the project.

Check your changes.

```bash
git status
```

Commit your work.

```bash
git add .

git commit -m "Add login page"
```

Push your branch.

```bash
git push -u origin feature/login-page
```

Create a Pull Request.

```
feature/login-page
        │
        ▼
develop
```

After the Pull Request is merged:

```bash
git checkout develop

git pull origin develop

git branch -d feature/login-page
```

---

# Complete Guide

When multiple developers work on the same project, everyone should follow the same workflow. This prevents lost work, reduces merge conflicts, and keeps the repository organized.

The recommended workflow is:

```text
feature branch
        │
        ▼
develop
        │
        ▼
main
```

* **Feature branches** are used for individual tasks.
* **develop** is the shared development branch.
* **main** always contains production-ready code.

---

## Step 1 — Start with the Latest Code

Before creating a feature branch, update your local repository.

```bash
git checkout develop

git pull origin develop
```

### Why?

Starting with the latest code reduces merge conflicts and ensures you are building on the newest version of the project.

---

## Step 2 — Create a Feature Branch

Create a new branch from `develop`.

Example:

```bash
git checkout -b feature/login-page
```

Other examples:

```text
feature/dashboard
feature/reports
feature/user-management
bugfix/login
hotfix/session-timeout
```

### Why?

Each feature or bug fix should have its own branch.

This keeps unfinished work separate from the shared development branch.

---

## Step 3 — Develop Your Feature

Modify the project files.

Example:

```text
login.php

sidebar.php

auth.php
```

Check your changes.

```bash
git status
```

Commit regularly.

```bash
git add .

git commit -m "Add login validation"
```

Small, focused commits are easier to review than one large commit.

---

## Step 4 — Push Your Branch

Upload your branch to GitHub.

```bash
git push -u origin feature/login-page
```

The `-u` option links your local branch with the remote branch.

Future pushes only require:

```bash
git push
```

---

## Step 5 — Create a Pull Request

Open GitHub.

Navigate to:

```
Repository
└── Pull Requests
    └── New Pull Request
```

Choose:

```
Base:
develop
```

```
Compare:
feature/login-page
```

Review the changes.

Add a title and description explaining:

* What changed.
* Why it changed.
* Any testing performed.

Submit the Pull Request.

---

## Step 6 — Review the Pull Request

Another developer or project maintainer should review the code.

Typical review items:

* Code quality.
* Coding standards.
* Functionality.
* Security.
* Performance.

If changes are requested:

* Update your branch.
* Commit the changes.
* Push again.

The Pull Request updates automatically.

---

## Step 7 — Merge into Develop

Once approved:

Merge the Pull Request.

GitHub combines the feature branch into:

```text
develop
```

The feature branch can now be deleted.

---

## Step 8 — Update Your Local Repository

Switch back to `develop`.

```bash
git checkout develop
```

Download the merged changes.

```bash
git pull origin develop
```

Delete the local feature branch.

```bash
git branch -d feature/login-page
```

Your repository is now ready for the next task.

---

# Recommended Workflow

```text
Developer A
        │
        ▼
feature/login
        │
        ▼
develop
        │
        ▼
main

Developer B
        │
        ▼
feature/reports
        │
        ▼
develop
        │
        ▼
main
```

Each developer works independently.

The shared `develop` branch collects completed work.

Only reviewed code reaches `main`.

---

# Verification

Check the current branch.

```bash
git branch
```

View all branches.

```bash
git branch -a
```

Check repository status.

```bash
git status
```

Confirm:

* Your feature branch has been pushed.
* The Pull Request has been merged.
* Your local `develop` branch is up to date.

---

# Common Problems

## Another developer modified the same file

Update your branch.

```bash
git checkout develop

git pull origin develop
```

Merge or rebase your feature branch.

Resolve any conflicts before pushing again.

---

## Pull Request has merge conflicts

Update your feature branch with the latest `develop`.

Resolve the conflicts.

Commit the resolved files.

Push the updated branch.

GitHub will automatically update the Pull Request.

---

## Accidentally committed directly to `develop`

If the commit has not been pushed:

```bash
git reset HEAD~1
```

Create a feature branch and recommit.

If the commit has already been pushed, discuss the best recovery approach with the project maintainer before rewriting shared history.

---

## Deleted the wrong branch

If the branch was already merged:

Recover it from the commit history.

```bash
git reflog
```

or

```bash
git log --all
```

Create the branch again from the desired commit.

---

# Best Practices

* Pull before starting new work.
* Create one feature branch per task.
* Commit small, meaningful changes.
* Push your work regularly.
* Use Pull Requests for code reviews.
* Delete feature branches after merging.
* Keep `develop` stable.
* Keep `main` production-ready.

---

# Summary

After completing this guide:

* You know how to work with multiple developers.
* You understand feature branches.
* You can create and review Pull Requests.
* You know how changes flow from a feature branch to `develop`.
* You understand how collaboration keeps the project organized.

Next:

➡ **10 - Deploy to Production**

# Secure the Project

## Quick Setup

Never commit sensitive files.

Verify `.gitignore` contains:

```text
.env
vendor/
node_modules/
*.log
```

Check Git status.

```bash
git status
```

Review staged files.

```bash
git diff --cached
```

Review the commit.

```bash
git show
```

Verify the environment.

```text
APP_ENV=development
```

Before deploying.

* Review the Pull Request.
* Confirm `.env` is not modified.
* Verify secrets are not included.
* Deploy only from `main`.

---

# Complete Guide

Security is not only about preventing attacks.

It also means protecting passwords, API keys, databases, production servers, and source code from accidental exposure.

Every developer is responsible for following secure development practices.

---

## Step 1 — Keep Secrets Out of Git

Sensitive information should never be committed.

Examples:

```text
.env

private.key

id_ed25519

config.local.php
```

Verify `.gitignore`.

```text
.env
vendor/
node_modules/
*.log
```

Check Git.

```bash
git status
```

If a sensitive file appears, stop before committing.

### Why?

Git keeps every committed file forever.

Removing a secret later does not remove it from the repository history.

---

## Step 2 — Use Environment Variables

Store configuration in:

```text
.env
```

Instead of:

```php
$db_password = "password";
```

Use environment variables.

Example:

```php
$db_password = getenv('DB_PASSWORD');
```

Or use your project's environment helper.

### Why?

Each developer can use different credentials.

Production credentials remain on the server.

---

## Step 3 — Protect SSH Keys

Each computer should have its own SSH key.

Example:

```text
~/.ssh/

id_ed25519
id_ed25519.pub
```

Never share:

```text
id_ed25519
```

Only upload:

```text
id_ed25519.pub
```

If a private key is exposed:

1. Remove it from GitHub.
2. Generate a new key.
3. Update GitHub immediately.

---

## Step 4 — Secure the Production Server

Never develop directly on the server.

All code should come from Git.

Deployment flow:

```text
Developer
      │
      ▼
GitHub
      │
      ▼
Production Server
```

Developers should not edit production files using:

* FTP
* File Manager
* Nano
* Vim

The server should only receive reviewed code from the repository.

---

## Step 5 — Review Before Every Commit

Before committing:

```bash
git status
```

Review staged files.

```bash
git diff --cached
```

Verify the commit.

```bash
git show
```

Ask yourself:

* Am I committing only the intended files?
* Did I accidentally include passwords?
* Did I accidentally include backup files?
* Did I accidentally include database dumps?

If anything looks wrong, remove it before pushing.

---

## Step 6 — Secure Dependencies

Install packages only from trusted sources.

Review new packages before adding them.

Example:

```bash
docker compose exec app composer require vendor/package
```

Commit only:

```text
composer.json

composer.lock
```

Never modify files inside:

```text
vendor/
```

---

## Step 7 — Production Environment

The production server should use:

```text
APP_ENV=production
```

Development should use:

```text
APP_ENV=development
```

Never enable debugging on production.

Example:

```text
display_errors = Off
```

Debug information can reveal:

* File paths
* Database names
* SQL queries
* Application structure

---

## Step 8 — Back Up Before Major Changes

Before:

* Deployments
* Database updates
* Major refactoring

Create backups.

Example:

```bash
mysqldump example_project > backup.sql
```

If something goes wrong, restore the backup before troubleshooting further.

---

# Security Checklist

Before every push:

* `.env` is not staged.
* Private keys are not staged.
* Database backups are not staged.
* Debug files are not staged.
* Only intended files are committed.

Before every deployment:

* Pull Request approved.
* Secrets remain on the server.
* Production uses `APP_ENV=production`.
* Deployment is from `main`.

---

# Verification

Review the repository.

```bash
git status
```

Review staged files.

```bash
git diff --cached
```

Verify ignored files.

```bash
git check-ignore .env
```

If `.env` is ignored, Git returns its path.

---

# Common Problems

## Accidentally committed `.env`

Stop pushing.

Remove it from Git.

```bash
git rm --cached .env
```

Commit the removal.

```bash
git commit -m "Remove .env"
```

Rotate any exposed credentials before continuing.

---

## Private SSH key leaked

Immediately:

* Remove the key from GitHub.
* Generate a new SSH key.
* Add the new public key.
* Delete the old private key.

Never continue using a compromised key.

---

## Debug mode enabled in production

Update:

```text
APP_ENV=production
```

Disable PHP error display.

Restart the application if required.

---

## Production server edited manually

Treat the server as a deployment target, not a development environment.

Move the changes into Git, then redeploy so the repository becomes the single source of truth again.

---

# Best Practices

* Never commit secrets.
* Keep `.env` local.
* Protect SSH keys.
* Review every commit before pushing.
* Deploy only reviewed code.
* Keep production and development configurations separate.
* Back up before major changes.

---

# Summary

After completing this guide:

* You know how to protect sensitive project files.
* You understand how secrets should be managed.
* You know how to secure deployments.
* You know how to prevent accidental credential leaks.
* You have a repeatable security checklist for development and deployment.

Next:

➡ **13 - Troubleshoot Common Problems**

# Troubleshoot Common Problems

## Quick Reference

### Git

```bash
git status
git branch
git remote -v
git log --oneline -10
```

### Docker

```bash
docker compose ps
docker compose logs
docker compose restart
```

### Composer

```bash
docker compose exec app composer install
```

### Database

```bash
docker compose ps
```

Check your `.env` database settings.

### PHP

```bash
php -v
```

### SSH

```bash
ssh -T git@github.com

ssh-add -l
```

---

# Complete Guide

This chapter helps diagnose the most common problems encountered during development and deployment.

When troubleshooting:

1. Read the complete error message.
2. Identify which component is failing.
3. Fix one problem at a time.
4. Verify the solution before continuing.

---

# Git Problems

## Permission denied (publickey)

Example:

```text
git@github.com: Permission denied (publickey)
```

### Cause

GitHub cannot authenticate your computer.

### Solution

Check whether your SSH key is loaded.

```bash
ssh-add -l
```

If no key is listed:

```bash
ssh-add ~/.ssh/id_ed25519
```

Test the connection.

```bash
ssh -T git@github.com
```

---

## Repository not found

### Cause

Possible reasons:

* Incorrect repository URL.
* Repository no longer exists.
* You don't have permission.

### Verify

```bash
git remote -v
```

Correct if necessary.

```bash
git remote set-url origin git@github.com:your-username/example-project.git
```

---

## Push rejected

Example:

```text
Updates were rejected because the remote contains work that you do not have locally.
```

### Solution

Download the latest changes.

```bash
git pull --rebase origin develop
```

Resolve any conflicts.

Continue.

```bash
git rebase --continue
```

Push again.

```bash
git push
```

---

## Merge Conflict

Example:

```text
<<<<<<< HEAD
```

### Solution

Edit the file.

Choose which code to keep.

Remove the conflict markers.

Stage the file.

```bash
git add filename.php
```

Continue.

```bash
git rebase --continue
```

or

```bash
git merge --continue
```

---

# Docker Problems

## Containers are not running

Check:

```bash
docker compose ps
```

If stopped:

```bash
docker compose up -d
```

---

## Container keeps restarting

View the logs.

```bash
docker compose logs
```

Or:

```bash
docker compose logs app
```

The logs usually indicate the failing service.

---

## Website does not load

Check:

```bash
docker compose ps
```

Verify:

* Web server is running.
* PHP container is running.
* Database is running.

Then inspect the logs.

```bash
docker compose logs
```

---

# Composer Problems

## vendor/autoload.php not found

### Cause

Dependencies are missing.

### Solution

```bash
docker compose exec app composer install
```

---

## Composer command not found

### Cause

Composer is not installed locally.

### Solution

Run Composer inside Docker.

```bash
docker compose exec app composer install
```

---

# Database Problems

## Access denied

Verify:

```dotenv
DB_HOST
DB_PORT
DB_DATABASE
DB_USERNAME
DB_PASSWORD
```

Restart the application.

```bash
docker compose restart
```

---

## Unknown database

Create the database.

```sql
CREATE DATABASE example_project;
```

Import the schema.

```bash
mysql -u example_user -p example_project < database/schema.sql
```

---

## Table does not exist

Import the latest schema.

```bash
mysql -u example_user -p example_project < database/schema.sql
```

---

# Environment Problems

## .env not found

Create it.

Windows:

```powershell
copy .env.example .env
```

Linux:

```bash
cp .env.example .env
```

Restart Docker.

```bash
docker compose restart
```

---

## Changes to .env are ignored

Restart the application.

```bash
docker compose restart
```

Some frameworks also require clearing their configuration cache.

---

# Deployment Problems

## New code is not visible

Update the server.

```bash
git pull origin main
```

If Docker configuration changed:

```bash
docker compose up -d --build
```

---

## Production server contains local changes

Check:

```bash
git status
```

Production should normally report:

```text
working tree clean
```

Do not edit production files directly.

---

# Debugging Checklist

Before asking for help, collect the following information.

### Git

```bash
git status
git branch
git remote -v
```

### Docker

```bash
docker compose ps
docker compose logs
```

### Composer

```bash
docker compose exec app composer install
```

### Environment

Verify:

```text
.env
```

exists and contains the correct values.

### Database

Verify:

* Database exists.
* Tables exist.
* Credentials are correct.

---

# Getting Help

When reporting a problem, include:

* The complete error message.
* The command you executed.
* The output of `git status`.
* The output of `docker compose ps`.
* Relevant log entries.
* The steps that caused the problem.

Avoid screenshots of terminal output when possible. Copy and paste the text instead, as it is easier to search, quote, and analyze.

---

# Best Practices

* Read the full error message.
* Solve one issue at a time.
* Verify each fix before trying another.
* Do not ignore warnings.
* Keep your local repository updated.
* Keep Docker running.
* Keep backups of important data.

---

# Summary

After completing this handbook, you should be able to:

* Set up a development environment.
* Configure Git and GitHub.
* Use Docker for development.
* Manage Composer dependencies.
* Work with multiple developers.
* Deploy to production safely.
* Manage project databases.
* Follow secure development practices.
* Troubleshoot common issues independently.

Congratulations! Your development environment is now ready, and you have the knowledge to contribute to the project confidently.

# Deploy to Production

## Quick Setup

Switch to the production branch.

```bash
git checkout main
```

Download the latest changes.

```bash
git pull origin main
```

Connect to the production server.

```bash
ssh user@your-server
```

Go to the project directory.

```bash
cd /var/www/example-project
```

Download the latest source code.

```bash
git pull origin main
```

Rebuild the containers if necessary.

```bash
docker compose up -d --build
```

Install Composer packages.

```bash
docker compose exec app composer install --no-dev --optimize-autoloader
```

Verify the application.

```bash
docker compose ps
```

Open the production website and confirm everything works.

---

# Complete Guide

Production deployment publishes the latest approved version of the application to the production server.

Only code that has been reviewed and merged into the `main` branch should be deployed.

The deployment flow is:

```text
Developer
      │
      ▼
Feature Branch
      │
      ▼
Develop
      │
      ▼
Pull Request
      │
      ▼
Main
      │
      ▼
Production Server
```

---

## Step 1 — Verify the Main Branch

Before deploying, confirm that the latest changes have already been merged into `main`.

Update your local repository.

```bash
git checkout main

git pull origin main
```

Review the latest commits.

```bash
git log --oneline -10
```

Verify that the commit you want to deploy is present.

---

## Step 2 — Connect to the Production Server

Connect using SSH.

```bash
ssh user@your-server
```

Example:

```text
ssh ubuntu@example-server
```

After logging in, navigate to the project.

```bash
cd /var/www/example-project
```

---

## Step 3 — Update the Source Code

Download the latest production code.

```bash
git pull origin main
```

### What this does

Git downloads only the changes that were merged into the `main` branch.

No development or feature branches are deployed.

---

## Step 4 — Install PHP Dependencies

If `composer.json` or `composer.lock` changed, install the updated packages.

```bash
docker compose exec app composer install --no-dev --optimize-autoloader
```

### Why?

* Removes development-only packages.
* Optimizes the autoloader.
* Keeps the production environment smaller and faster.

If no Composer changes were made, this step is usually optional.

---

## Step 5 — Rebuild the Containers

If you changed any of the following:

* Dockerfile
* docker-compose.yml
* PHP extensions
* System packages

Rebuild the containers.

```bash
docker compose up -d --build
```

If you only changed PHP, HTML, CSS, or JavaScript source files that are mounted into the container, a rebuild may not be necessary.

---

## Step 6 — Verify the Deployment

Check the container status.

```bash
docker compose ps
```

Example:

```text
NAME      STATUS

app       Up

db        Up

nginx     Up
```

Open the production website in your browser.

Verify:

* Home page loads.
* Login works.
* Database connection succeeds.
* New features are available.
* No errors appear in the browser.

---

## Step 7 — Check the Logs

If something isn't working, inspect the logs.

View all logs.

```bash
docker compose logs
```

View application logs.

```bash
docker compose logs app
```

View web server logs.

```bash
docker compose logs nginx
```

Press **Ctrl + C** to stop following the logs if you use the `-f` option.

---

## Deployment Checklist

Before deploying:

* All changes merged into `main`.
* Pull Request approved.
* Local testing completed.
* `.env` is correct on the server.
* Database backup completed (if required).

After deploying:

* Website loads.
* Login works.
* Database works.
* Containers are running.
* Logs show no unexpected errors.

---

# Verification

Check Git.

```bash
git status
```

Expected:

```text
working tree clean
```

Check Docker.

```bash
docker compose ps
```

Check Composer.

```bash
docker compose exec app composer --version
```

Open the production website and confirm the new version is live.

---

# Common Problems

## Local changes exist on the server

Running:

```bash
git pull
```

may fail if files were edited directly on the server.

Production servers should not be used for development.

All code changes should come from Git.

---

## Composer packages missing

Run:

```bash
docker compose exec app composer install --no-dev --optimize-autoloader
```

---

## Website still shows old code

If your application uses caching, clear the cache according to your framework's documentation.

If Docker images changed:

```bash
docker compose up -d --build
```

---

## Container failed to start

Inspect the logs.

```bash
docker compose logs
```

The logs usually identify the failing service.

---

# Best Practices

* Never edit production files directly.
* Deploy only from the `main` branch.
* Keep `.env` on the server.
* Never commit production secrets.
* Test on `develop` before merging to `main`.
* Verify the deployment immediately after publishing.

---

# Summary

After completing this guide:

* You can deploy the application safely.
* You understand the production deployment workflow.
* You know when to rebuild Docker containers.
* You know how to verify a successful deployment.
* You know how to troubleshoot common deployment issues.

Next:

➡ **11 - Manage the Database**

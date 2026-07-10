# Install Composer Dependencies

## Quick Setup

Install the project dependencies.

**If Composer is installed on your computer**

```bash
composer install
```

**If Composer runs inside Docker**

```bash
docker compose exec app composer install
```

Verify Composer.

```bash
composer --version
```

Verify the `vendor` directory was created.

```text
example-project/

vendor/
composer.json
composer.lock
```

If `composer.json` changes:

```bash
composer install
```

If you add a new package:

```bash
composer require vendor/package
```

Commit the changes.

```bash
git add composer.json composer.lock

git commit -m "Add vendor/package"

git push
```

Do **not** commit:

```text
vendor/
```

---

# Complete Guide

Composer is PHP's dependency manager.

Instead of manually downloading PHP libraries, Composer installs and updates them automatically based on the project's `composer.json` file.

---

## Step 1 — Understand the Composer Files

A typical PHP project contains:

```text
example-project/

composer.json
composer.lock
vendor/
```

### File Purpose

| File            | Purpose                                                 |
| --------------- | ------------------------------------------------------- |
| `composer.json` | Lists the PHP packages required by the project.         |
| `composer.lock` | Records the exact package versions that were installed. |
| `vendor/`       | Contains the installed packages.                        |

Only `vendor/` is generated automatically.

---

## Step 2 — Install the Dependencies

If Composer is installed on your computer, run:

```bash
composer install
```

If Composer runs inside Docker, use:

```bash
docker compose exec app composer install
```

### What this command does

Composer reads:

```text
composer.lock
```

If the lock file exists, Composer installs the exact package versions recorded in it.

If the lock file is missing, Composer installs the latest versions allowed by `composer.json`.

### Verify

After installation:

```text
vendor/

autoload.php
```

should exist.

---

## Step 3 — Verify the Installation

Check Composer.

```bash
composer --version
```

Check the installed packages.

```bash
composer show
```

If using Docker:

```bash
docker compose exec app composer show
```

The project should now have a populated `vendor/` directory.

---

## Step 4 — Add a New Package

Sometimes the project needs a new PHP package.

Example:

```bash
composer require monolog/monolog
```

If using Docker:

```bash
docker compose exec app composer require monolog/monolog
```

Composer automatically updates:

```text
composer.json

composer.lock
```

It also downloads the package into:

```text
vendor/
```

---

## Step 5 — Commit Dependency Changes

Whenever you add or remove packages, commit:

```text
composer.json

composer.lock
```

Example:

```bash
git add composer.json composer.lock

git commit -m "Add monolog"

git push
```

Do **not** commit:

```text
vendor/
```

Every developer should generate their own `vendor` directory by running:

```bash
composer install
```

---

## Step 6 — Update Packages (Optional)

Update all packages.

```bash
composer update
```

Or update a specific package.

```bash
composer update monolog/monolog
```

### Important

Use `composer update` only when you intentionally want newer package versions.

Most developers should use:

```bash
composer install
```

because it installs the versions already approved by the project.

---

# Verification

Verify Composer.

```bash
composer --version
```

Verify packages.

```bash
composer show
```

Verify the `vendor` directory exists.

```text
vendor/

autoload.php
```

Open the application.

If it loads without:

```text
vendor/autoload.php not found
```

then Composer has been configured correctly.

---

# Common Problems

## `vendor/autoload.php` not found

The dependencies have not been installed.

Run:

```bash
composer install
```

or

```bash
docker compose exec app composer install
```

---

## Composer command not found

Composer is not installed on your computer.

Either install Composer locally or run it through Docker.

---

## Package was added but another developer gets an error

Make sure you committed:

```text
composer.json

composer.lock
```

Do **not** commit:

```text
vendor/
```

Other developers should run:

```bash
composer install
```

---

## Accidentally committed `vendor`

Remove it from Git.

```bash
git rm -r --cached vendor
```

Add it to `.gitignore`.

```text
vendor/
```

Commit the change.

```bash
git commit -m "Remove vendor directory"

git push
```

---

# Best Practices

* Commit `composer.json`.
* Commit `composer.lock`.
* Ignore `vendor/`.
* Use `composer install` for normal development.
* Use `composer update` only when intentionally updating dependencies.

---

# Summary

After completing this guide:

* Composer dependencies are installed.
* The `vendor` directory has been generated.
* You know which Composer files belong in Git.
* You understand when to use `install`, `require`, and `update`.

Next:

➡ **08 - Work with Git**

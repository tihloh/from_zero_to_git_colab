# Configure Environment Variables

## Quick Setup

Copy the example environment file.

**Windows**

```powershell
copy .env.example .env
```

**Linux**

```bash
cp .env.example .env
```

Open `.env`.

Update the required values.

Example:

```dotenv
APP_ENV=development

DB_HOST=db
DB_PORT=3306

DB_DATABASE=example_project
DB_USERNAME=example_user
DB_PASSWORD=example_password
```

Save the file.

Restart Docker.

```bash
docker compose restart
```

If new PHP packages were added:

```bash
docker compose exec app composer install
```

Verify the application.

```text
http://localhost
```

---

# Complete Guide

The `.env` file stores configuration values used by the application.

Instead of editing the source code, you change the values in `.env`. This allows every developer to use different settings while keeping the same source code.

---

## Step 1 — Create the Environment File

The repository should include an example configuration.

```text
.env.example
```

Create your own environment file.

### Windows

```powershell
copy .env.example .env
```

### Linux

```bash
cp .env.example .env
```

After copying, your project should contain:

```text
example-project/

.env.example
.env
```

### Why?

`.env.example` is safe to commit to Git.

`.env` contains your personal settings and should never be committed.

---

## Step 2 — Configure the Application

Open `.env` using your preferred editor.

Example:

```dotenv
APP_ENV=development

DB_HOST=db
DB_PORT=3306

DB_DATABASE=example_project

DB_USERNAME=example_user

DB_PASSWORD=example_password
```

Update the values for your local environment.

Typical settings include:

| Variable      | Description               |
| ------------- | ------------------------- |
| `APP_ENV`     | Application mode.         |
| `DB_HOST`     | Database server hostname. |
| `DB_PORT`     | Database port.            |
| `DB_DATABASE` | Database name.            |
| `DB_USERNAME` | Database username.        |
| `DB_PASSWORD` | Database password.        |

Do not remove variables unless you know they are no longer used by the application.

---

## Step 3 — Restart the Application

Some applications automatically detect changes to `.env`.

Others require a restart.

Restart the containers.

```bash
docker compose restart
```

If the application uses PHP-FPM, restarting ensures the new environment values are loaded.

---

## Step 4 — Verify the Configuration

Open the application.

```text
http://localhost
```

Verify that:

* The application loads.
* The database connects successfully.
* No configuration errors are displayed.

If your project includes a health check or status page, verify that it also reports the application as healthy.

---

## Step 5 — Ignore the Environment File

Open `.gitignore`.

Verify it contains:

```text
.env
```

### Why?

Every developer uses different credentials.

Keeping `.env` out of Git prevents accidental exposure of passwords, API keys, and other sensitive information.

Instead, update `.env.example` whenever a new configuration variable is required.

Example:

```dotenv
# .env.example

APP_ENV=development

DB_HOST=db
DB_PORT=3306

DB_DATABASE=example_project

DB_USERNAME=example_user

DB_PASSWORD=example_password
```

Developers can then copy the updated template into their own `.env`.

---

## Step 6 — Updating Environment Variables

When a new configuration option is added:

1. Update your own `.env`.
2. Update `.env.example`.
3. Commit **only** `.env.example`.

Example:

```bash
git add .env.example

git commit -m "Add MAIL_HOST environment variable"

git push
```

Never commit:

```text
.env
```

---

# Verification

Check that `.env` exists.

```bash
ls -a
```

or on Windows:

```powershell
dir -Force
```

Verify Git ignores the file.

```bash
git status
```

The `.env` file should not appear in the list of tracked files.

Restart the application.

```bash
docker compose restart
```

Open:

```text
http://localhost
```

The application should load without configuration errors.

---

# Common Problems

## `.env` was committed to Git

If the file has already been committed:

Remove it from Git while keeping it on your computer.

```bash
git rm --cached .env
```

Commit the change.

```bash
git commit -m "Remove .env from repository"

git push
```

Also make sure `.gitignore` contains:

```text
.env
```

---

## Database connection failed

Verify:

* `DB_HOST`
* `DB_PORT`
* `DB_DATABASE`
* `DB_USERNAME`
* `DB_PASSWORD`

Then restart the containers.

```bash
docker compose restart
```

---

## Application still uses old values

Restart Docker.

```bash
docker compose restart
```

Some PHP applications may also require clearing their configuration cache. Refer to your framework's documentation if changes are not reflected after restarting.

---

## `.env.example` is missing new variables

Whenever you add a new environment variable:

* Update your own `.env`
* Update `.env.example`
* Commit only `.env.example`

This ensures new developers can set up the project without guessing which variables are required.

---

# Summary

After completing this guide:

* You created your own `.env` file.
* You configured the application for your local environment.
* You know which files should and should not be committed.
* You understand how to safely share configuration changes with other developers.

Next:

➡ **07 - Install Composer Dependencies**

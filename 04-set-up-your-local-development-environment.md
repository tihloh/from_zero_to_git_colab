# Set Up Your Local Development Environment

## Quick Setup

Clone the repository.

```bash
git clone git@github.com:your-username/example-project.git

cd example-project
```

Copy the environment file.

**Windows**

```powershell
copy .env.example .env
```

**Linux**

```bash
cp .env.example .env
```

Edit `.env` with your local configuration.

Start Docker.

```bash
docker compose up -d --build
```

Install Composer packages.

```bash
composer install
```

Verify everything is running.

```bash
docker compose ps
```

Open the website.

```text
http://localhost
```

---

# Complete Guide

This guide prepares your computer for local development. After completing these steps, you'll have a fully working copy of the project that is isolated from the production server.

---

## Step 1 — Clone the Repository

Copy the SSH URL from GitHub.

Example:

```text
git@github.com:your-username/example-project.git
```

Clone the project.

```bash
git clone git@github.com:your-username/example-project.git
```

Move into the project folder.

```bash
cd example-project
```

### What this does

* Downloads the latest source code.
* Creates a local Git repository.
* Connects your local project to GitHub.

### Verify

Run:

```bash
git remote -v
```

Expected:

```text
origin  git@github.com:your-username/example-project.git
```

---

## Step 2 — Create Your Environment File

Most projects include a template called:

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

Example:

```text
example-project/

.env.example
.env
docker-compose.yml
composer.json
```

### What this does

Each developer has their own `.env` file.

This allows different settings without modifying the project's source code.

Example:

```text
Developer A
APP_ENV=development
DB_HOST=localhost
```

```text
Developer B
APP_ENV=development
DB_HOST=192.168.1.50
```

The `.env` file should never be committed to Git.

---

## Step 3 — Configure Your Environment

Open the `.env` file.

Example:

```dotenv
APP_ENV=development

DB_HOST=db
DB_PORT=3306

DB_DATABASE=example_project

DB_USERNAME=example_user

DB_PASSWORD=example_password
```

Update the values for your local environment if necessary.

### What this does

The application reads these settings at runtime.

Changing `.env` does not modify the application's source code.

---

## Step 4 — Build the Docker Environment

Start the development containers.

```bash
docker compose up -d --build
```

### What this command does

* Builds Docker images if needed.
* Creates containers.
* Starts the services.
* Runs them in the background.

The first build may take several minutes.

### Verify

Check running containers.

```bash
docker compose ps
```

Example:

```text
NAME             STATUS

web              Up

mysql            Up
```

---

## Step 5 — Install Composer Dependencies

Install the PHP packages required by the project.

```bash
composer install
```

If Composer is running inside Docker:

```bash
docker compose exec app composer install
```

### What this does

Composer reads:

```text
composer.json
```

Downloads the required packages and creates:

```text
vendor/
```

Do not manually edit files inside the `vendor` directory.

---

## Step 6 — Open the Application

Open your browser.

Example:

```text
http://localhost
```

or

```text
http://localhost:8080
```

depending on your Docker configuration.

If the application loads successfully, your local development environment is ready.

---

## Verification

Check Git.

```bash
git status
```

Check Docker.

```bash
docker compose ps
```

Check Composer.

```bash
composer --version
```

Confirm:

* Repository cloned successfully.
* `.env` exists.
* Docker containers are running.
* Composer packages are installed.
* Website loads successfully.

---

## Common Problems

### `.env` file not found

Create it from the template.

```bash
cp .env.example .env
```

---

### `vendor/autoload.php` not found

Composer packages have not been installed.

Run:

```bash
composer install
```

or

```bash
docker compose exec app composer install
```

---

### Cannot connect to the database

Check the database settings in `.env`.

Verify that the database container is running.

```bash
docker compose ps
```

---

### Docker containers keep restarting

View the logs.

```bash
docker compose logs
```

The logs usually identify the service causing the problem.

---

# Summary

After completing this guide:

* The project has been cloned.
* Your personal `.env` file has been created.
* Docker containers are running.
* Composer dependencies have been installed.
* The application is running locally.

Next:

➡ **05 - Build the Docker Environment**

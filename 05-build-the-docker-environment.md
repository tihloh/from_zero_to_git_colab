# Build the Docker Environment

## Quick Setup

Build and start the containers.

```bash
docker compose up -d --build
```

View running containers.

```bash
docker compose ps
```

View container logs.

```bash
docker compose logs
```

View logs for a specific service.

```bash
docker compose logs app

docker compose logs db
```

Stop the containers.

```bash
docker compose down
```

Restart the containers.

```bash
docker compose restart
```

Rebuild after changing the Dockerfile.

```bash
docker compose up -d --build
```

Run a command inside the PHP container.

```bash
docker compose exec app bash
```

Run Composer.

```bash
docker compose exec app composer install
```

---

# Complete Guide

Docker allows every developer to use the same development environment regardless of their operating system. Instead of installing PHP, MySQL, Composer, and other dependencies directly on your computer, they run inside containers.

---

## Step 1 — Understand the Project Structure

A typical Docker project looks like this.

```text
example-project/

docker-compose.yml
Dockerfile
.env
```

### File Purpose

| File                 | Purpose                            |
| -------------------- | ---------------------------------- |
| `docker-compose.yml` | Defines all project services.      |
| `Dockerfile`         | Builds the PHP application image.  |
| `.env`               | Stores local configuration values. |

---

## Step 2 — Build the Environment

Build and start every service.

```bash
docker compose up -d --build
```

### What this command does

* Builds Docker images.
* Creates containers.
* Creates networks.
* Creates volumes.
* Starts every service.

The `-d` option runs the containers in the background.

The `--build` option rebuilds the image if necessary.

### Verify

```bash
docker compose ps
```

Example:

```text
NAME           STATUS

app            Up

db             Up

nginx          Up
```

All services should have a status of **Up**.

---

## Step 3 — View Running Containers

Display all project containers.

```bash
docker compose ps
```

Example:

```text
NAME      IMAGE      STATUS

app       php        Up

db        mysql      Up

nginx     nginx      Up
```

### Why?

This confirms that Docker successfully started the project.

---

## Step 4 — View Logs

If something isn't working, check the logs.

All services:

```bash
docker compose logs
```

Specific service:

```bash
docker compose logs app
```

```bash
docker compose logs db
```

To continuously watch new log entries:

```bash
docker compose logs -f app
```

Press **Ctrl + C** to stop watching.

---

## Step 5 — Access a Container

Sometimes you need to work inside a container.

Open a shell.

```bash
docker compose exec app bash
```

Example:

```text
root@container:/var/www/html#
```

You can now run commands inside the container.

Examples:

```bash
php artisan
```

```bash
composer install
```

```bash
php -v
```

Exit the container.

```bash
exit
```

---

## Step 6 — Restart the Environment

Restart all services.

```bash
docker compose restart
```

Restart only one service.

```bash
docker compose restart app
```

Restarting is useful after changing configuration files.

---

## Step 7 — Stop the Environment

Stop every container.

```bash
docker compose down
```

Containers are removed, but volumes remain unless explicitly deleted.

Start them again.

```bash
docker compose up -d
```

---

## Step 8 — Rebuild the Environment

If you modify the Dockerfile or install new system packages, rebuild the image.

```bash
docker compose up -d --build
```

Docker rebuilds the image and recreates the containers.

---

## Step 9 — Remove Everything (Optional)

Remove containers, networks, and volumes.

```bash
docker compose down -v
```

### Warning

This deletes Docker volumes.

If your database is stored in a Docker volume, the data will be lost unless it is backed up.

Use this command only when you intentionally want a clean environment.

---

# Docker Compose Commands

| Command                        | Description                        |
| ------------------------------ | ---------------------------------- |
| `docker compose up -d`         | Start the project.                 |
| `docker compose up -d --build` | Rebuild and start.                 |
| `docker compose ps`            | Show running containers.           |
| `docker compose logs`          | View all logs.                     |
| `docker compose logs app`      | View app logs.                     |
| `docker compose exec app bash` | Open a shell in the app container. |
| `docker compose restart`       | Restart all services.              |
| `docker compose down`          | Stop the project.                  |
| `docker compose down -v`       | Stop and remove volumes.           |

---

# Verification

Run:

```bash
docker compose ps
```

Confirm:

* The PHP container is running.
* The database container is running.
* The web server container is running.

Open the application.

```
http://localhost
```

The application should load without errors.

---

# Common Problems

## Docker is not running

Start Docker Desktop.

Wait until Docker reports:

```
Engine running
```

---

## Port already in use

Example:

```
Bind for 0.0.0.0:80 failed
```

Another application is already using the port.

Stop the conflicting application or change the port mapping in `docker-compose.yml`.

---

## Changes are not appearing

If you changed the Dockerfile:

```bash
docker compose up -d --build
```

If you only changed the application source code, rebuilding is usually **not** required because the project directory is mounted into the container.

---

## Cannot access the website

Check that the containers are running.

```bash
docker compose ps
```

Then check the logs.

```bash
docker compose logs
```

The logs usually identify the failing service.

---

# Summary

After completing this guide:

* You understand the Docker project structure.
* You can start and stop the environment.
* You can rebuild containers.
* You can access containers.
* You know how to troubleshoot common Docker issues.

Next:

➡ **06 - Configure Environment Variables**

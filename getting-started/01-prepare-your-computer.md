# Prerequisites

## Quick Setup

Before starting, make sure you have:

* A GitHub account.
* Git installed.
* Docker Desktop installed.
* Visual Studio Code installed.
* An SSH client (OpenSSH).
* Internet access.
* Basic knowledge of the command line.

Verify the required software.

```bash
git --version

docker --version

docker compose version

ssh -V
```

If all commands display a version number, you're ready to continue.

---

# Complete Guide

Before setting up the project, install and verify the required software.

Following the prerequisites ensures that every developer uses a similar development environment, making collaboration and troubleshooting much easier.

---

## Step 1 — Create a GitHub Account

Create a GitHub account if you don't already have one.

GitHub will be used to:

* Store the source code.
* Share changes with other developers.
* Review code through Pull Requests.
* Deploy approved code to production.

---

## Step 2 — Install Git

Install Git for your operating system.

Verify the installation.

```bash
git --version
```

Expected output:

```text
git version 2.x.x
```

Git is used to track changes and collaborate with other developers.

---

## Step 3 — Install Docker Desktop

Install Docker Desktop.

Verify Docker.

```bash
docker --version
```

Verify Docker Compose.

```bash
docker compose version
```

Docker provides a consistent development environment for every developer.

---

## Step 4 — Install Visual Studio Code

Install Visual Studio Code or another code editor of your choice.

Recommended extensions:

* Docker
* GitHub Pull Requests
* PHP Intelephense
* EditorConfig

These extensions improve development but are optional.

---

## Step 5 — Verify SSH

Verify that OpenSSH is available.

```bash
ssh -V
```

SSH will later be used to authenticate with GitHub and connect to production servers.

---

## Step 6 — Verify Internet Access

Ensure you can access:

* GitHub
* Docker Hub

These services are required to clone repositories and download Docker images.

---

## Step 7 — Learn the Project Workflow

The project follows this workflow:

```text
Create Repository
        │
        ▼
Configure SSH
        │
        ▼
Clone Repository
        │
        ▼
Configure Docker
        │
        ▼
Configure .env
        │
        ▼
Install Composer
        │
        ▼
Develop on develop
        │
        ▼
Create Pull Request
        │
        ▼
Merge into main
        │
        ▼
Deploy to Production
```

Each chapter in this handbook follows this workflow.

Complete one chapter before moving to the next.

---

# Verification

Verify all required tools.

```bash
git --version

docker --version

docker compose version

ssh -V
```

Confirm:

* Git is installed.
* Docker is installed.
* Docker Compose is installed.
* SSH is available.

---

# Common Problems

## Git command not found

Git is not installed or is not included in your system's PATH.

Reinstall Git and restart your terminal.

---

## Docker command not found

Docker Desktop is not installed or is not running.

Start Docker Desktop and verify it is running before continuing.

---

## Docker Compose command not found

Update Docker Desktop to a version that includes Docker Compose v2.

Verify again.

```bash
docker compose version
```

---

## SSH command not found

Install OpenSSH or enable the built-in OpenSSH client provided by your operating system.

Verify the installation.

```bash
ssh -V
```

---

# Summary

After completing this guide:

* Your computer is ready for development.
* The required software is installed.
* You have verified that each tool works correctly.
* You understand the order of the remaining chapters.

Next:

➡ **02 - GitHub Setup**

# Developer Playbook

Everything you need to set up, develop, collaborate, deploy, and maintain the project.

Follow the chapters in order when setting up the project for the first time. Afterward, use this handbook as a reference whenever you need a reminder or encounter a problem.

---

# Handbook Structure

## Getting Started

For new developers setting up the project.

1. [01 - Prerequisites](getting-started/01-prerequisites.md)
2. [02 - Create a GitHub Repository](getting-started/02-create-a-github-repository.md)
3. [03 - Configure SSH Authentication](getting-started/03-configure-ssh-authentication.md)
4. [04 - Set Up Local Development](getting-started/04-set-up-local-development.md)
5. [05 - Build the Docker Environment](getting-started/05-build-the-docker-environment.md)
6. [06 - Configure Environment Variables](getting-started/06-configure-environment-variables.md)
7. [07 - Install Composer Dependencies](getting-started/07-install-composer-dependencies.md)

---

## Development

Daily development workflow.

8. [08 - Work with Git](development/08-work-with-git.md)

9. [09 - Collaborate with Other Developers](development/09-collaborate-with-other-developers.md)

---

## Deployment

Preparing and publishing production releases.

10. [10 - Deploy to Production](deployment/10-deploy-to-production.md)

11. [11 - Manage the Database](deployment/11-manage-the-database.md)

---

## Maintenance

Maintaining and supporting the project.

12. [12 - Secure the Project](maintenance/12-secure-the-project.md)

13. [13 - Troubleshoot Common Problems](maintenance/13-troubleshoot-common-problems.md)

---

# Development Workflow

```text
Prepare Computer
        │
        ▼
GitHub Setup
        │
        ▼
SSH Authentication
        │
        ▼
Clone Repository
        │
        ▼
Docker Setup
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

---

# Quick Reference

## First-Time Setup

1. Complete all chapters under **Getting Started**.
2. Clone the repository.
3. Configure `.env`.
4. Start Docker.
5. Install Composer dependencies.
6. Verify the application.

---

## Daily Development

1. Pull the latest changes.
2. Create or switch to your working branch.
3. Make your changes.
4. Commit and push.
5. Open a Pull Request.

---

## Deployment

1. Merge approved changes into `main`.
2. Pull the latest code on the production server.
3. Install Composer dependencies if required.
4. Rebuild Docker containers if required.
5. Verify the deployment.

---

# Contributing

* Follow the documented Git workflow.
* Commit small, meaningful changes.
* Write clear commit messages.
* Never commit secrets or sensitive files.
* Keep `main` production-ready.

---

# Need Help?

If you encounter a problem, start with:

**Maintenance → 13 - Troubleshoot Common Problems**

Most common setup, Git, Docker, Composer, database, and deployment issues are covered there.

# Create a GitHub Repository

## Quick Setup

Create a **Private** repository.

Do **not** initialize with:
- README
- .gitignore
- License

Generate SSH:

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

Show public key:

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

```bash
cat ~/.ssh/id_ed25519.pub
```

Test:

```bash
ssh -T git@github.com
```

Clone:

```bash
git clone git@github.com:your-username/example-project.git
cd example-project
```

Create branches:

```bash
git branch -M main
git checkout -b develop
git push -u origin main
git push -u origin develop
```

Invite contributors (**Write** permission).

---

# Complete Guide

## Step 1 - Create the Repository

Create a private repository and leave it empty.

## Step 2 - Configure SSH

Generate a key pair, upload the **public** key to GitHub (**Settings → SSH and GPG Keys**) and test the connection.

## Step 3 - Clone the Repository

Clone using the SSH URL so future pushes don't require passwords.

## Step 4 - Create Main Branches

Use `main` for production and `develop` for ongoing development.

## Step 5 - Invite Contributors

Give contributors **Write** permission. Keep **Admin** access for project owners only.

Next: Configure SSH Authentication.

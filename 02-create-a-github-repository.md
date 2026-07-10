# GitHub Setup

## Quick Setup

Create a **Private** GitHub repository.

Do **not** initialize it with:

- README
- .gitignore
- License

Generate an SSH key.

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

Display the public key.

Windows

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

Linux

```bash
cat ~/.ssh/id_ed25519.pub
```

Upload the public key to:

```
Settings
└── SSH and GPG Keys
```

Test SSH.

```bash
ssh -T git@github.com
```

Clone the repository.

```bash
git clone git@github.com:your-username/example-project.git

cd example-project
```

Create the project branches.

```bash
git branch -M main

git checkout -b develop

git push -u origin main

git push -u origin develop
```

Invite contributors with **Write** permission.

(Optional) Protect the `main` branch.

---

# Complete Guide

This section explains each step in detail.

---

## Step 1 — Create the Repository

Log in to GitHub and click **New repository**.

Enter a repository name.

Example:

```
example-project
```

Choose:

```
Visibility:
Private
```

Leave these options **unchecked**:

- Add a README
- Add a `.gitignore`
- Choose a license

Click **Create repository**.

### Why leave the repository empty?

Your project already exists on your computer.

An empty repository lets you upload your existing source code without creating unnecessary merge commits or conflicts during the initial push.

---

## Step 2 — Generate an SSH Key

Every development computer should have its own SSH key.

Open PowerShell or Terminal and run:

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

When prompted:

```
Enter file in which to save the key:
```

Press **Enter** to use the default location.

When prompted for a passphrase, either enter one for additional security or press **Enter** to skip it.

After the command completes, two files are created.

```
~/.ssh/

id_ed25519
id_ed25519.pub
```

| File | Description |
|------|-------------|
| `id_ed25519` | Your private key. Never share this file. |
| `id_ed25519.pub` | Your public key. Upload this file to GitHub. |

### Why is SSH used?

SSH allows GitHub to verify your computer without requiring your username and password every time you push code.

Only the public key is uploaded to GitHub.

The private key never leaves your computer.

---

## Step 3 — Add the Public Key to GitHub

Display your public key.

Windows:

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

Linux:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output.

In GitHub, open:

```
Profile
└── Settings
    └── SSH and GPG Keys
        └── New SSH Key
```

Enter a descriptive title.

Examples:

```
Home PC

Office PC

Laptop
```

Paste the copied key and click **Add SSH Key**.

### Verify

Run:

```bash
ssh -T git@github.com
```

Expected output:

```
Hi your-username!

You've successfully authenticated...
```

If you see this message, SSH has been configured successfully.

---

## Step 4 — Clone the Repository

Copy the SSH URL from GitHub.

Example:

```
git@github.com:your-username/example-project.git
```

Clone the repository.

```bash
git clone git@github.com:your-username/example-project.git
```

Move into the project directory.

```bash
cd example-project
```

### Verify

Run:

```bash
git remote -v
```

Expected:

```
origin git@github.com:your-username/example-project.git
```

---

## Step 5 — Create the Main Branches

Rename the default branch.

```bash
git branch -M main
```

Create the development branch.

```bash
git checkout -b develop
```

Push both branches.

```bash
git push -u origin main

git push -u origin develop
```

### Branch Purpose

```
main
│
└── Production-ready code


develop
│
└── Development and testing
```

---

## Step 6 — Invite Contributors

Open:

```
Repository
└── Settings
    └── Collaborators
```

Invite each developer using their GitHub username.

Assign the following permission:

```
Write
```

Do not give contributors **Admin** permission unless they are responsible for managing the repository.

---

## Step 7 — Protect the Main Branch (Optional)

If your GitHub plan supports branch protection:

Open:

```
Repository
└── Settings
    └── Branches
```

Create a rule for:

```
main
```

Recommended settings:

- Require Pull Requests before merging
- Block force pushes
- Prevent branch deletion

This helps protect your production branch from accidental changes.

---

# Verification

Run:

```bash
git branch -a

git remote -v

ssh -T git@github.com
```

Confirm that:

- SSH authentication succeeds.
- The remote uses the SSH URL.
- `main` exists.
- `develop` exists.

---

# Common Problems

...# GitHub Setup

## Quick Setup

### 1. Create a Private Repository

Repository Settings

```
Visibility: Private
Initialize with README: No
Initialize with .gitignore: No
Add License: No
```

### 2. Generate an SSH Key

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

### 3. Upload the Public Key

Windows

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

Linux

```bash
cat ~/.ssh/id_ed25519.pub
```

GitHub

```
Settings
└── SSH and GPG Keys
    └── New SSH Key
```

### 4. Test SSH

```bash
ssh -T git@github.com
```

### 5. Clone the Repository

```bash
git clone git@github.com:your-username/example-project.git

cd example-project
```

### 6. Create the Main Branches

```bash
git branch -M main

git checkout -b develop

git push -u origin main

git push -u origin develop
```

### 7. Add Contributors

```
Repository
└── Settings
    └── Collaborators
```

Permission

```
Write
```

### 8. Protect `main` (Optional)

```
Repository
└── Settings
    └── Branches
```

Enable

- Require Pull Request
- Prevent force pushes
- Prevent deletion

---

# Complete Guide

The following sections explain each step in detail.

---

## Step 1 — Create a Private Repository

Open GitHub and create a new repository.

Repository name example:

```
example-project
```

Choose:

```
Private
```

Leave these options unchecked:

- README
- .gitignore
- License

Click **Create Repository**.

### Why this matters

The repository remains empty so you can upload your existing project without unnecessary merge commits.

---

## Step 2 — Generate an SSH Key

Every computer should have its own SSH key.

Run:

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

Press **Enter** to accept the default location.

This creates:

```
~/.ssh/

id_ed25519
id_ed25519.pub
```

| File | Purpose |
|------|---------|
| `id_ed25519` | Private key. Never share it. |
| `id_ed25519.pub` | Public key. Upload to GitHub. |

...

(continue with the remaining steps)

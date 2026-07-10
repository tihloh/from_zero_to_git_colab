# GitHub Setup

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

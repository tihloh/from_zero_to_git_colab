# Configure SSH Authentication

## Quick Setup

Generate an SSH key.

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

Start the SSH agent.

**Windows (PowerShell)**

```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic

Start-Service ssh-agent
```

**Linux**

```bash
eval "$(ssh-agent -s)"
```

Add the private key.

**Windows**

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

**Linux**

```bash
ssh-add ~/.ssh/id_ed25519
```

Verify the key is loaded.

```bash
ssh-add -l
```

Test GitHub authentication.

```bash
ssh -T git@github.com
```

---

# Complete Guide

This guide configures SSH so Git can securely authenticate with GitHub without asking for your username and password every time you push or pull changes.

---

## Step 1 — Generate an SSH Key

Each development computer should have its own SSH key.

Open a terminal or PowerShell and run:

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

### What this command does

* Creates a new SSH key pair.
* Uses the recommended **Ed25519** encryption algorithm.
* Adds a comment to help identify the key.

Press **Enter** when asked where to save the key.

Example:

```
Enter file in which to save the key:

C:\Users\John\.ssh\id_ed25519
```

You may also enter a passphrase for additional security, or press **Enter** to leave it empty.

After the command finishes, two files are created.

```
id_ed25519
id_ed25519.pub
```

| File             | Purpose                                  |
| ---------------- | ---------------------------------------- |
| `id_ed25519`     | Your private key. Keep this file secret. |
| `id_ed25519.pub` | Your public key. Upload this to GitHub.  |

> Never share your private key.

---

## Step 2 — Start the SSH Agent

The SSH agent keeps your private key in memory so you don't have to enter the passphrase every time Git connects to GitHub.

### Windows

Enable the service.

```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic
```

Start the service.

```powershell
Start-Service ssh-agent
```

### Linux

Start the SSH agent.

```bash
eval "$(ssh-agent -s)"
```

### Verify

You should see something similar to:

```
Agent pid 12345
```

---

## Step 3 — Add Your Private Key

Load your private key into the SSH agent.

### Windows

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

### Linux

```bash
ssh-add ~/.ssh/id_ed25519
```

### Verify

Display all loaded keys.

```bash
ssh-add -l
```

Example output:

```
256 SHA256:xxxxxxxxxxxxxxxx developer@example.com (ED25519)
```

If you see your key listed, it has been loaded successfully.

---

## Step 4 — Verify the Public Key Exists

Before uploading the key to GitHub, make sure the public key exists.

### Windows

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

### Linux

```bash
cat ~/.ssh/id_ed25519.pub
```

You should see a long line beginning with:

```
ssh-ed25519
```

Copy the entire line.

---

## Step 5 — Upload the Public Key to GitHub

Open GitHub.

Navigate to:

```
Profile
└── Settings
    └── SSH and GPG Keys
        └── New SSH Key
```

Fill in the form.

Example:

```
Title

Office PC
```

```
Key Type

Authentication Key
```

Paste the copied public key into the **Key** field.

Click **Add SSH Key**.

Repeat this process for every computer you use.

Example:

```
Home PC

Office PC

Laptop
```

Each device should have its own SSH key.

---

## Step 6 — Test the Connection

Run:

```bash
ssh -T git@github.com
```

The first time you connect, you may see:

```
The authenticity of host 'github.com' can't be established.
```

Type:

```
yes
```

GitHub's fingerprint will be saved to your `known_hosts` file.

Expected output:

```
Hi your-username!

You've successfully authenticated...
```

Your computer is now authorized to access your GitHub repositories.

---

## Verification

Verify the SSH agent has your key.

```bash
ssh-add -l
```

Verify authentication.

```bash
ssh -T git@github.com
```

Confirm that:

* The SSH agent is running.
* Your private key is loaded.
* GitHub authentication succeeds.

---

## Common Problems

### Permission denied (publickey)

Your private key may not be loaded.

Check:

```bash
ssh-add -l
```

If no keys are listed, add it again.

```bash
ssh-add ~/.ssh/id_ed25519
```

---

### The SSH agent is not running

Start the SSH agent again.

Windows:

```powershell
Start-Service ssh-agent
```

Linux:

```bash
eval "$(ssh-agent -s)"
```

---

### Wrong GitHub Account

If you have multiple GitHub accounts, make sure the correct public key is uploaded to the account that owns or has access to the repository.

---

# Summary

After completing this guide:

* SSH keys have been created.
* The SSH agent is running.
* Your private key is loaded.
* Your public key has been added to GitHub.
* GitHub can authenticate your computer securely.

Next:

➡ **04 - Set Up Your Local Development Environment**

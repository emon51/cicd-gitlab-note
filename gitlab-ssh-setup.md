# GitLab SSH Setup Guide

## Problem
```
Permission denied (publickey)
```

## Cause
SSH key not configured with GitLab.

---

## Step 1: Generate SSH Key
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- ssh-keygen → tool to create keys
- -t → type of key
- ed25519 → algorithm used to generate the key
  
Press Enter for default settings.


---

## Step 2: Check Key
```
ls ~/.ssh
```
Expected:
- id_ed25519
- id_ed25519.pub

---

## Step 3: Copy Public Key
```
cat ~/.ssh/id_ed25519.pub
```

---

## Step 4: Add to GitLab
1. Go to GitLab
2. Profile → Preferences → Access → SSH Keys
3. Paste key
4. Click "Add key"

---

## Step 5: Start SSH Agent
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

## Step 6: Test Connection
```
ssh -T git@gitlab.com
```
For local setup using Docker
```
ssh -T -p 2222 git@localhost
```

Expected:
```
Welcome to GitLab, @username!
```

---

## Step 7: Push Code
```
git push -u origin main
```

---

## Important Notes
- Share only: id_ed25519.pub (public key)
- Never share: id_ed25519 (private key)

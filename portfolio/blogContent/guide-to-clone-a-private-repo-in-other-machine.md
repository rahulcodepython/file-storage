---
title: How to clone a private repo in other machine (like VPS)
description: This is a guide helps us to clone a private repo to any machine
date: 03/18/2024
---

To clone a private repository in your VPS, follow these steps:

### 1. **Use SSH Key Authentication (Recommended)**

#### **Step 1: Generate SSH Key (If Not Already Generated)**

Run this command on your VPS:

```sh
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Press **Enter** to save it in the default location (`~/.ssh/id_ed25519`).

#### **Step 2: Copy the SSH Public Key**

```sh
cat ~/.ssh/id_ed25519.pub
```

Copy the output.

#### **Step 3: Add the SSH Key to GitHub**

1. Go to **GitHub** → **Settings** → **SSH and GPG keys**.
2. Click **New SSH key**.
3. Paste the copied key and save it.

#### **Step 4: Test the Connection**

```sh
ssh -T git@github.com
```

It should return:

```
Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.
```

#### **Step 5: Clone the Repository**

Now, clone the private repo using SSH:

```sh
git clone git@github.com:your-username/your-private-repo.git
```

---

### 2. **Use Personal Access Token (Alternative)**

If SSH is not an option, use a **GitHub personal access token** (PAT).

#### **Step 1: Generate a Personal Access Token**

1. Go to **GitHub** → **Settings** → **Developer settings** → **Personal access tokens**.
2. Click **Generate new token (classic)**.
3. Select scopes like `repo` (for private repo access).
4. Copy the generated token.

#### **Step 2: Clone Using HTTPS**

Run:

```sh
git clone https://<your-github-username>:<your-personal-access-token>@github.com/your-username/your-private-repo.git
```

🔹 **Tip:** Instead of putting the token in the command, configure it securely:

```sh
git config --global credential.helper store
git clone https://github.com/your-username/your-private-repo.git
```

Then, enter the **username** as your GitHub username and **password** as your token.

---

For security, **SSH authentication is the best choice**. Let me know if you need help setting it up! 🚀

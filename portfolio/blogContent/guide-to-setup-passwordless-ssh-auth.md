---
title: How to setup passwordless SSH authentication
description: This is a post for setting up a ssh passwordless authentication
date: 08/03/2025
---

To set up **passwordless SSH login** from your **Windows machine (rd211)** to your **Ubuntu server (rahul)**, follow these steps:

---

## **Step 1: Generate an SSH Key on Windows**

On your **Windows laptop**, open **PowerShell** or **Command Prompt** and run:

```powershell
ssh-keygen -t rsa -b 4096
```

-   When prompted for a file location, press **Enter** to save it in the default location:  
     `C:\Users\rd211\.ssh\id_rsa`
-   If prompted for a passphrase, you can leave it empty.

---

## **Step 2: Copy the Public Key to the Ubuntu Server**

Now, transfer your public key to the Ubuntu server.

### **Method 1: Using `ssh-copy-id` (Recommended)**

If your Ubuntu server allows SSH password login, run from **PowerShell**:

```powershell
ssh-copy-id rahul@<server-ip>
```

It will ask for Rahul’s password once, then set up key-based login.

### **Method 2: Manually Copying the Key**

If `ssh-copy-id` is not available, do the following:

1. Open **PowerShell** and display the public key:

    ```powershell
    Get-Content $HOME\.ssh\id_rsa.pub
    ```

2. Copy the output.
3. Log in to your Ubuntu server manually:

    ```bash
    ssh rahul@<server-ip>
    ```

4. On the Ubuntu server, create the `.ssh` directory and authorized keys file:

    ```bash
    mkdir -p ~/.ssh && chmod 700 ~/.ssh
    echo "<PASTE_YOUR_PUBLIC_KEY_HERE>" >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    ```

5. Exit from the Ubuntu server:

    ```bash
    exit
    ```

---

## **Step 3: Verify SSH Key Login**

Now, try logging in without a password:

```powershell
ssh rahul@<server-ip>
```

If everything is set up correctly, you should be logged in without being prompted for a password.

---

## **Step 4: Disable Password Authentication (Optional, for Security)**

To **force SSH key-based authentication only**, do the following on the Ubuntu server:

1. Open the SSH configuration file:

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

2. Find and update these lines:

    ```plaintext
    PasswordAuthentication no
    PubkeyAuthentication yes
    ```

3. Restart SSH service:

    ```bash
    sudo systemctl restart ssh
    ```

Now, only SSH keys will work for authentication.

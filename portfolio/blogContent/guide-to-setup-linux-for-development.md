---
title: How to setup linux for development
description: This is a guide book for setting up a newly linux distro for development purpose
date: 08/03/2025
---

1. Install latest version of python

```bash
# Update the package list
sudo apt update

# Add the Deadsnakes PPA to your system
sudo add-apt-repository ppa:deadsnakes/ppa

# Update the package list
sudo apt update

# Install Python 3.13
sudo apt install -y python3.13 python3.13-venv python3.13-dev

# Update alternatives to set Python 3.13 as the default
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.13 1
sudo update-alternatives --config python3

# Verify the default Python version
python3 --version

# Install pip for Python 3.13
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python3.13 get-pip.py

# Verify pip installation
pip --version
```

To configure the `python` command to invoke Python 3, you have several options:

**1. Using an Alias (User-Specific):**

Add the following line to your `~/.bashrc` or `~/.bash_aliases` file:

```bash
alias python='python3'
```

After saving the file, apply the changes by running:

```bash
source ~/.bashrc
```

**2. Using `update-alternatives` (System-Wide):**

This method is suitable for Debian-based systems. First, add Python 3 as an alternative:

```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
```

Then, select Python 3 as the default:

```bash
sudo update-alternatives --config python
```

**3. Creating a Symbolic Link (System-Wide):**

Create a symbolic link pointing `python` to `python3`:

```bash
sudo ln -s /usr/bin/python3 /usr/bin/python
```

**Caution:** Altering the default `python` command may affect system scripts that rely on Python 2. Ensure that such changes do not disrupt system operations.

2. To install Git on Ubuntu, you can use the following commands:

```bash
sudo apt update
sudo apt install git
```

After installation, verify the installed Git version:

```bash
git --version
```

3. To install both Docker Engine (daemon) and Docker Desktop on Ubuntu, follow these steps:

**1. Install Docker Engine:**

Docker Engine is the core component that runs Docker containers.

-   **Update the package index:**

```bash
   sudo apt update
```

-   **Install prerequisite packages:**

    ```bash
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
    ```

-   **Add Docker's official GPG key:**

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

-   **Add the Docker APT repository:**

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

-   **Update the package index again:**

    ```bash
    sudo apt update
    ```

-   **Install Docker Engine:**

    ```bash
    sudo apt install docker-ce
    ```

-   **Verify Docker installation:**

    ```bash
    docker --version
    ```

**2. Install Docker Desktop:**

Docker Desktop provides a user-friendly interface for managing Docker containers and integrates additional tools.

-   **Ensure your system meets the prerequisites:**

-   Ubuntu 22.04, 24.04, or the latest non-LTS version.

    -   For non-Gnome Desktop environments, install `gnome-terminal`:

        ```bash
        sudo apt install gnome-terminal
        ```

-   **Set up Docker's package repository:**

    If not already done during Docker Engine installation, add Docker's GPG key and repository:

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

-   **Download the latest Docker Desktop DEB package:**

    Visit the [Docker Desktop release page](https://docs.docker.com/desktop/release-notes/) to find the latest version. Replace `<version>` with the appropriate version number:

    ```bash
    curl -LO https://desktop.docker.com/linux/main/amd64/docker-desktop-<version>-amd64.deb
    ```

-   **Install Docker Desktop:**

    ```bash
    sudo apt install ./docker-desktop-<version>-amd64.deb
    ```

-   **Launch Docker Desktop:**

After installation, you can start Docker Desktop from your application launcher or by running:

```bash
systemctl --user start docker-desktop
```

4. To install the latest version of Node.js using NVM (Node Version Manager) on Ubuntu, run the following commands:

### **1. Install NVM**

```bash
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
```

_(Check [NVM GitHub](https://github.com/nvm-sh/nvm) for the latest version if needed.)_

### **2. Reload Shell Configuration**

```bash
source ~/.bashrc  # Use ~/.zshrc if you're using Zsh
```

### **3. Verify NVM Installation**

```bash
command -v nvm
```

### **4. Install the Latest Node.js Version**

```bash
nvm install node
```

### **5. Set the Installed Version as Default**

```bash
nvm use node
nvm alias default node
```

### **6. Verify Installation**

```bash
node -v
npm -v
```

5. To install VS Code using `snapd` on Ubuntu, run the following commands:

### **1. Ensure `snapd` is installed**

```bash
sudo apt update
sudo apt install snapd
```

### **2. Install Visual Studio Code**

```bash
sudo snap install code --classic
```

### **3. Verify Installation**

```bash
code --version
```

Now, you can launch VS Code using:

```bash
code
```

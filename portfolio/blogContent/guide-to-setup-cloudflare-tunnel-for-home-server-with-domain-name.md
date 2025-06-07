---
title: How to setup Cloudflare tunnel for home server with domain name
description: This is a guide to setup Cloudflare tunnel for home server with domain name
date: 08/03/2025
---

You can use **Cloudflare Tunnel** to expose your home server without opening router ports. Here's how you can do it:

---

### **Step 1: Install Cloudflare Tunnel (cloudflared)**

SSH into your Ubuntu server and run:

```sh
sudo apt update
```

```sh
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
```

```sh
sudo dpkg -i cloudflared-linux-amd64.deb
```

Check if it's installed correctly:

```sh
cloudflared --version
```

---

### **Step 2: Authenticate Cloudflare Tunnel**

Run the command to log in:

```sh
cloudflared tunnel login
```

-   This will open a browser and ask you to select your domain (`rahulcodepython.tech`).
-   Approve the request and get back to the terminal.

##### **Authenticate Cloudflare Tunnel | Alternative Way**

Since you're using **Ubuntu Server OS** without a browser, you can still authenticate **Cloudflare Tunnel** using a different device (like your personal laptop or phone). Here's how:

---

###### **Step 1: Start Cloudflare Tunnel Authentication**

On your Ubuntu Server, run:

```sh
cloudflared tunnel login
```

This will output a URL like:

```
Please open the following URL and log in with your Cloudflare account:
https://dash.cloudflare.com/argotunnel?some-auth-link
```

---

###### **Step 2: Authenticate Using Another Device**

1. Copy the URL from the terminal.
2. Open the URL on your **personal computer, phone, or another device** with a browser.
3. Log in to Cloudflare and approve the authentication.
4. Once approved, **Cloudflare will generate a certificate** and download it automatically on your server.

---

###### **Step 3: Verify Authentication**

Once the authentication is done, your terminal should confirm success.

To check if the credentials were saved correctly, run:

```sh
ls ~/.cloudflared/
```

You should see a **`.json` credentials file** inside.

Now, you can continue setting up the tunnel as per the previous steps. 🚀

---

### **Step 3: Create a Cloudflare Tunnel**

Create a named tunnel:

```sh
cloudflared tunnel create my-home-server
```

This will generate a **UUID** (a unique ID for your tunnel).

---

### **Step 4: Configure Cloudflare Tunnel**

Navigate to the `.cloudflared` directory:

```sh
cd /etc/cloudflared
```

Edit or create a config file:

```sh
nano config.yml
```

Add the following content:

```yaml
tunnel: YOUR_UUID_HERE # Replace with the UUID from Step 3
credentials-file: ~/.cloudflared/YOUR_UUID_HERE.json # Path to credentials file

ingress:
    - hostname: rahulcodepython.tech
      service: http://localhost:80 # Change this if your web server runs on a different port
    - service: http_status:404 # Catch-all rule
```

You have to change:

-   Tunnel UUID
-   Credentials file path
-   Port Number

Save the file and exit.

---

### **Step 5: Start Cloudflare Tunnel**

Now start your tunnel:

```sh
nohup cloudflared tunnel run my-home-server > /dev/null 2>&1 &
```

---

### **🛑 Stop A Connector**

1️⃣ First, list running `cloudflared` processes:

```sh
ps aux | grep cloudflared
```

-   This will show the **Process IDs (PIDs)** of running instances.

2️⃣ Kill the extra process using its PID (replace `<PID>` with the actual number):

```sh
sudo kill <PID>
```

OR, if multiple processes exist:

```sh
sudo killall cloudflared # Kill all cloudflared connector
cloudflared tunnel run my-home-server # Restart a new tunnel connector
```

---

### **Step 6: Set Up a Simple Web Server**

Create a simple HTML file:

```sh
mkdir -p /var/www/html
nano /var/www/html/index.html
```

Add this content:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Welcome to Rahul's Server</title>
    </head>
    <body>
        <h1>Hello, Cloudflare Tunnel is working!</h1>
    </body>
</html>
```

Save the file.

Now install a lightweight web server:

```sh
sudo apt update
sudo apt install nginx -y
```

Make sure the server is running:

```sh
sudo systemctl start nginx
sudo systemctl enable nginx
```

Check if it's working locally:

```sh
curl http://localhost
```

---

### **Step 7: Connect Cloudflare Tunnel to Your Domain**

###### **Delete Existing A Records**

In the Cloudflare **DNS Records Settings**:

1. Find the following records and **delete them all**:
    - `A * → 75.2.103.23`
    - `A rahulcodepython.tech → 75.2.103.23`
    - `A www → 75.2.103.23`

📌 **Why delete them?**  
Cloudflare Tunnel does not rely on an **A record (IP address)** but instead uses a **CNAME record** pointing to the Cloudflare network.

###### **Find Your Tunnel UUID**

When you created the tunnel earlier, you received a **Tunnel UUID** (a long alphanumeric string). If you forgot it, you can list your tunnels using:

```sh
cloudflared tunnel list
```

This will output something like:

```
ID                                   NAME             CREATED       CONNECTIONS
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx my-home-server  2024-03-02    2x yyz -> MIA
```

The **ID (UUID)** is important, and we’ll use it in the next step.

###### **Connect tunnel with domain name**

1. **Go to Cloudflare Dashboard** → **Your Domain (`rahulcodepython.tech`)**
2. **DNS Settings** → Add a `CNAME` record:
    - **Name:** `@`
    - **Target:** `YOUR_TUNNEL_ID.cfargotunnel.com`
    - **Proxy Status:** ✅ (Keep it proxied)

---

### **Step 8: Run Cloudflare Tunnel as a Service**

If you want the tunnel to **automatically start on reboot**, create a systemd service:

```sh
sudo nano /etc/systemd/system/cloudflared.service
```

Paste the following:

```ini
[Unit]
Description=Cloudflare Tunnel
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/cloudflared tunnel run my-home-server
Restart=always
User=root

[Install]
WantedBy=multi-user.target
```

Save and exit.

Create a folder and move the config.yml file to there:

```sh
sudo mkdir -p /root/.cloudflared # Creating the directory
sudo cp /etc/cloudflared/config.yml /root/.cloudflared/config.yml # Moving the file to there
```

Then, enable and start the service:

```sh
sudo systemctl restart cloudflared # Restart the service
sudo systemctl status cloudflared # Check the status of the service
sudo systemctl enable cloudflared # Enable it for start automatically after boot
sudo systemctl start cloudflared # Start the service (not required if it is already active, check before use it)
```

---

### **Step 9: Verify Your Website**

Now open your domain in a browser:

```
https://rahulcodepython.tech
```

You should see your HTML page!

---

### **Steps to add new services**

#### - Step 1: Add the `hostname` and `servie` to the `confi.yml` file.

Open the `config.yml`

```sh
sudo nano /root/.cloudflared/config.yml
```

Add new services

```
    - hostname: rahulcodepython.tech
      service: http://localhost:80  # Change this if your web server runs on a different port
```

#### - Step 2: Restart the cloudflared service.

```sh
sudo systemctl restart cloudflared
```

---

### **Here are some useful `cloudflared` commands:**

###### **🚀 Basic Commands**

```sh
cloudflared --version       # Check installed version
cloudflared tunnel login    # Authenticate with Cloudflare
cloudflared tunnel create my-home-server  # Create a new tunnel
cloudflared tunnel list     # List all created tunnels
cloudflared tunnel delete my-home-server  # Delete a tunnel
```

---

###### **🚀 Running the Tunnel**

```sh
cloudflared tunnel run my-home-server  # Start a specific tunnel with logs
nohup cloudflared tunnel run my-home-server > /dev/null 2>&1 & # Start a specific tunnel without logs and run in background (recomended)
cloudflared tunnel ingress validate       # Validate the config file
```

---

###### **🚀 Configuration & Management**

```sh
cloudflared tunnel route ip add 192.168.1.100/32 my-home-server  # Route traffic
cloudflared tunnel route ip show  # Show configured routes
cloudflared tunnel cleanup         # Remove old tunnels
```

---

##### **🚀Check Tunnel Status (Highlighted)**

```sh
cloudflared tunnel info my-home-server  # Show status and info of a tunnel
```

---

# **🚀 Hurrah! Tunnel setup is done.**

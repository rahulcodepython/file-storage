---
title: Nginx Commands
description: This is a post for describing few nginx commands
date: 08/03/2025
---

Here are some common **Nginx** commands for managing the server:

### **1. Start, Stop, and Restart Nginx**

```sh
sudo systemctl start nginx    # Start Nginx
sudo systemctl stop nginx     # Stop Nginx
sudo systemctl restart nginx  # Restart Nginx (hard restart)
sudo systemctl reload nginx   # Reload without dropping connections
```

### **2. Check Nginx Status**

```sh
sudo systemctl status nginx  # Check if Nginx is running
```

### **3. Test Nginx Configuration**

```sh
sudo nginx -t   # Test for syntax errors
```

### **4. Enable/Disable Nginx on Boot**

```sh
sudo systemctl enable nginx   # Enable auto-start on boot
sudo systemctl disable nginx  # Disable auto-start on boot
```

### **5. View Nginx Logs**

```sh
sudo tail -f /var/log/nginx/access.log  # View access logs
sudo tail -f /var/log/nginx/error.log   # View error logs
```

### **6. Reload Configuration without Restarting**

```sh
sudo systemctl reload nginx
```

### **7. Check Running Nginx Processes**

```sh
ps aux | grep nginx
```

### **8. Stop All Nginx Processes**

```sh
sudo pkill nginx
```

### **9. Find Active Nginx Configuration Files**

```sh
nginx -T   # Show all active configuration files
```

Let me know if you need any specific Nginx command details! 🚀

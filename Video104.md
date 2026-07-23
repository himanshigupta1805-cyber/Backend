# Hosting an Express App on Ubuntu VPS using Hostinger
### Sigma Web Development Course - Tutorial #104

---

# Overview

In this tutorial, an **Express.js application** is deployed on an **Ubuntu VPS (Virtual Private Server)** purchased from **Hostinger**.

Unlike shared hosting, a VPS gives you complete control over the server, allowing you to install software like Node.js, Nginx, PM2, MongoDB, MySQL, etc.

---

# Prerequisites

- Node.js installed
- Express.js application ready
- Git installed
- GitHub repository (recommended)
- Domain name (optional)
- VPS with Ubuntu installed
- SSH client (Terminal / PowerShell / Git Bash / PuTTY)

---

# What is a VPS?

**VPS (Virtual Private Server)** is a virtual machine that behaves like a dedicated server.

Instead of sharing resources with many users (Shared Hosting), each VPS gets dedicated resources.

### Advantages

- Full root access
- Better performance
- Custom software installation
- Better security
- Suitable for production applications

---

# Buying a VPS

Popular VPS providers:

- Hostinger
- DigitalOcean
- AWS EC2
- Azure
- Google Cloud
- Linode
- Vultr

For learning purposes, Hostinger provides an affordable Ubuntu VPS.

---

# Connecting to the VPS

Use SSH to connect.

```bash
ssh root@YOUR_SERVER_IP
```

Example

```bash
ssh root@145.xxx.xxx.xxx
```

If asked:

```text
Are you sure you want to continue connecting?
```

Type

```text
yes
```

Then enter the VPS password.

---

# Updating Ubuntu

Always update the package lists after logging in.

```bash
sudo apt update
```

Upgrade installed packages.

```bash
sudo apt upgrade -y
```

---

# Installing Git

```bash
sudo apt install git
```

Verify installation

```bash
git --version
```

---

# Installing Node.js

Install Node.js using NodeSource (recommended for latest LTS).

Example:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```

Install Node.js

```bash
sudo apt install nodejs
```

Check versions

```bash
node -v
npm -v
```

---

# Cloning the Project

Clone the Express application.

```bash
git clone <repository-url>
```

Example

```bash
git clone https://github.com/user/project.git
```

Move inside the project.

```bash
cd project
```

---

# Installing Dependencies

Install all required npm packages.

```bash
npm install
```

This reads the **package.json** file and installs every dependency.

---

# Environment Variables

Create a `.env` file if required.

Example

```env
PORT=3000
DB_URL=...
JWT_SECRET=...
```

Never upload sensitive `.env` files to GitHub.

---

# Running the Express Server

Development mode

```bash
node server.js
```

or

```bash
npm start
```

If successful,

```text
Server running on port 3000
```

---

# Problem with Running Node Directly

If you close the terminal,

```text
Node Server Stops
```

This is not suitable for production.

---

# PM2

PM2 is a **Node.js Process Manager**.

It keeps your application running continuously.

### Features

- Auto restart
- Background execution
- Crash recovery
- Startup on reboot
- Monitoring
- Logging

---

# Installing PM2

```bash
sudo npm install -g pm2
```

Verify

```bash
pm2 -v
```

---

# Starting the Application with PM2

```bash
pm2 start server.js
```

or

```bash
pm2 start app.js
```

Name the process

```bash
pm2 start server.js --name campuscare
```

---

# PM2 Commands

Show running applications

```bash
pm2 list
```

View logs

```bash
pm2 logs
```

Restart app

```bash
pm2 restart campuscare
```

Stop app

```bash
pm2 stop campuscare
```

Delete process

```bash
pm2 delete campuscare
```

Monitor processes

```bash
pm2 monit
```

---

# Saving PM2 Processes

Save running processes

```bash
pm2 save
```

Enable auto-start on server reboot

```bash
pm2 startup
```

Run the generated command.

---

# Why Use Nginx?

Instead of exposing your Node.js app directly, use **Nginx** as a **Reverse Proxy**.

Benefits:

- Better security
- HTTPS support
- Faster static file serving
- Load balancing
- Hides application port
- Handles multiple domains

---

# Installing Nginx

```bash
sudo apt install nginx
```

Check status

```bash
sudo systemctl status nginx
```

Start Nginx

```bash
sudo systemctl start nginx
```

Enable on boot

```bash
sudo systemctl enable nginx
```

---

# Nginx Reverse Proxy

Example configuration

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

Meaning:

- Listen on port **80**
- Accept requests for your domain
- Forward requests to Express running on **localhost:3000**

---

# Restarting Nginx

After changing configuration,

```bash
sudo systemctl restart nginx
```

or

```bash
sudo service nginx restart
```

---

# Firewall (UFW)

Allow HTTP traffic.

```bash
sudo ufw allow 'Nginx Full'
```

Check firewall status.

```bash
sudo ufw status
```

---

# Accessing the Application

Open browser

```text
http://YOUR_SERVER_IP
```

or

```text
http://yourdomain.com
```

If Nginx is configured correctly, your Express app should be accessible.

---

# Updating the Application

Whenever code changes,

Pull latest code.

```bash
git pull
```

Install new packages (if any)

```bash
npm install
```

Restart PM2

```bash
pm2 restart campuscare
```

---

# Deployment Workflow

```text
Develop Locally
        │
        ▼
Push Code to GitHub
        │
        ▼
SSH into VPS
        │
        ▼
Clone / Pull Repository
        │
        ▼
npm install
        │
        ▼
Configure .env
        │
        ▼
Run using PM2
        │
        ▼
Configure Nginx
        │
        ▼
Open Server IP / Domain
```

---

# Common Commands Cheat Sheet

### SSH

```bash
ssh root@SERVER_IP
```

### Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

### Clone Repository

```bash
git clone <repo-url>
```

### Install Dependencies

```bash
npm install
```

### Start App

```bash
pm2 start server.js --name app
```

### PM2

```bash
pm2 list
pm2 logs
pm2 restart app
pm2 stop app
pm2 delete app
pm2 save
pm2 startup
```

### Nginx

```bash
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl status nginx
```

---

# Key Interview Points

- **VPS** provides dedicated virtual resources with full root access.
- **SSH** is used to remotely access the VPS.
- **PM2** keeps Node.js applications running in production.
- **Nginx** acts as a reverse proxy between users and the Express app.
- **Reverse Proxy** hides backend ports and forwards requests to the application.
- **Git** is used to deploy code from GitHub to the server.
- **Environment variables (.env)** store sensitive configuration securely.
- **Production deployment** typically follows:
  - GitHub → VPS → npm install → PM2 → Nginx
- **PM2 + Nginx** is a standard deployment setup for Express.js applications.

---

# Revision Summary

- Buy an Ubuntu VPS.
- Connect using SSH.
- Update the server.
- Install Git and Node.js.
- Clone the Express project.
- Install dependencies with `npm install`.
- Configure the `.env` file.
- Run the application using **PM2**.
- Install and configure **Nginx** as a reverse proxy.
- Restart Nginx and access the application through the server IP or domain.
- Update the application later using `git pull` and `pm2 restart`.

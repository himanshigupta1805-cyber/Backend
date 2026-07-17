# What is Hosting? Where to Host? Which Hosting?
## Sigma Web Development Course - Tutorial #103
### Revision Notes

---

# What is Hosting?

Hosting is the process of making your website or web application available on the internet so that anyone can access it using a URL.

Without hosting:

```
Your Computer
      ↓
Only you can access the website
```

With hosting:

```
Your Computer
      ↓
Hosting Server
      ↓
Internet
      ↓
Users Worldwide
```

A hosting provider stores your project on its servers and serves it to users over the internet.

---

# Why Do We Need Hosting?

- To make a website publicly accessible.
- To keep the website online 24×7.
- To provide a permanent URL/domain.
- To store application files and databases.
- To handle user requests.

---

# Types of Hosting

## 1. Static Hosting

Used for websites containing only:

- HTML
- CSS
- JavaScript
- Images

No backend or database is required.

### Examples

- Portfolio
- Landing Page
- Documentation
- Resume Website

### Advantages

- Fast
- Free on many platforms
- Easy deployment
- Secure

---

## 2. Dynamic Hosting

Used when the project has:

- Backend
- Database
- Authentication
- APIs

Examples:

- Express.js
- Django
- Flask
- Spring Boot
- Laravel

### Examples of Dynamic Websites

- E-commerce websites
- Social media
- Blog websites
- Chat applications
- College Management Systems

---

# Static vs Dynamic Hosting

| Static Hosting | Dynamic Hosting |
|---------------|-----------------|
| HTML/CSS/JS only | Backend supported |
| No database | Database supported |
| Very fast | Slightly slower |
| Easy deployment | More configuration |
| Mostly free | Free + Paid options |

---

# Components of a Full Stack Project

```
Frontend
    ↓
Backend
    ↓
Database
```

Each component may be hosted separately.

---

# Where Can We Host?

## Frontend Hosting

Popular platforms:

- Vercel
- Netlify
- GitHub Pages
- Firebase Hosting
- Cloudflare Pages

Best for:

- React
- Angular
- Vue
- Static Websites

---

## Backend Hosting

Popular platforms:

- Render
- Railway
- Fly.io
- Heroku (limited free usage)
- AWS EC2
- DigitalOcean

Suitable for:

- Node.js
- Express.js
- Flask
- Django
- Spring Boot

---

## Database Hosting

Popular databases:

### MongoDB Atlas

- Cloud-hosted MongoDB
- Free tier available
- Easy integration

### MySQL

Hosted on:

- Railway
- PlanetScale
- Aiven
- AWS RDS

### PostgreSQL

Hosted on:

- Supabase
- Railway
- Neon
- AWS RDS

---

# Complete Hosting Architecture

```
User
      ↓
Frontend (Vercel)

      ↓

Backend API (Render)

      ↓

Database (MongoDB Atlas)
```

---

# Which Hosting Platform Should You Choose?

## For Beginners

Frontend

- Vercel
- Netlify

Backend

- Render
- Railway

Database

- MongoDB Atlas

This combination is free and beginner-friendly.

---

# Hosting Flow

```
Write Code
      ↓
Push to GitHub
      ↓
Connect GitHub Repository
      ↓
Hosting Platform Builds Project
      ↓
Website Goes Live
```

---

# Why GitHub is Important?

Most hosting platforms directly integrate with GitHub.

Workflow:

```
Local Project
      ↓
Git Commit
      ↓
Git Push
      ↓
GitHub
      ↓
Hosting Platform
```

Whenever you push new code:

```
GitHub
      ↓
Hosting Platform
      ↓
Automatic Deployment
```

This process is called **Continuous Deployment (CD)**.

---

# Deployment

Deployment means uploading your application to a hosting server so users can access it online.

Example:

Before deployment

```
http://localhost:3000
```

After deployment

```
https://your-app-name.vercel.app
```

---

# Localhost vs Hosted Website

| Localhost | Hosted Website |
|-----------|----------------|
| Runs on your computer | Runs on cloud server |
| Only you can access | Anyone with the URL can access |
| Stops when your PC is off | Available 24×7 |
| Used for development | Used for production |

---

# Domain Name

A domain is the human-readable address of your website.

Examples:

- google.com
- github.com
- openai.com

Without a domain, websites are accessed using IP addresses.

---

# Hosting vs Domain

Hosting

- Stores website files.
- Runs the application.

Domain

- Provides a memorable name for the website.

Example:

```
Domain
example.com

↓

Hosting Server

↓

Website Files
```

---

# Free Hosting Platforms

### Frontend

- Vercel
- Netlify
- GitHub Pages
- Cloudflare Pages

### Backend

- Render
- Railway
- Fly.io

### Database

- MongoDB Atlas
- Supabase
- Neon

---

# Paid Hosting Platforms

- AWS
- Microsoft Azure
- Google Cloud Platform (GCP)
- DigitalOcean
- Linode

Used for production-scale applications.

---

# Advantages of Cloud Hosting

- High availability
- Automatic backups
- Scalability
- Global accessibility
- Better performance
- Easy deployment

---

# Typical Deployment for MERN Stack

```
React
     ↓
Vercel

Express + Node
     ↓
Render

MongoDB
     ↓
MongoDB Atlas
```

---

# Common Beginner Mistakes

- Forgetting to push code to GitHub.
- Not adding environment variables.
- Using localhost database in production.
- Forgetting to build frontend.
- Wrong API URLs after deployment.
- Exposing secret keys in GitHub.

---

# Best Practices

- Use GitHub for version control.
- Store secrets in environment variables.
- Never upload `.env` files.
- Keep frontend, backend, and database separate.
- Test locally before deployment.
- Use free hosting while learning.

---

# Key Terms

### Hosting

Making a website available on the internet.

### Deployment

Uploading a project to a hosting server.

### Domain

The web address used to access a website.

### Server

A computer that serves web pages and APIs to users.

### Cloud Hosting

Hosting applications on cloud infrastructure instead of a personal computer.

---

# Interview Questions

### What is hosting?

Hosting is the service of storing and serving a website or web application over the internet.

---

### Difference between localhost and hosting?

| Localhost | Hosting |
|-----------|----------|
| Local machine | Remote server |
| Development | Production |
| Private | Public |

---

### What is deployment?

Deployment is the process of publishing an application to a hosting platform.

---

### Which platforms are commonly used for frontend hosting?

- Vercel
- Netlify
- GitHub Pages
- Cloudflare Pages

---

### Which platforms are commonly used for backend hosting?

- Render
- Railway
- Fly.io
- AWS EC2

---

### Which platform is commonly used for MongoDB hosting?

MongoDB Atlas.

---

# Quick Revision

- Hosting makes a website accessible over the internet.
- Static hosting is for HTML, CSS, and JavaScript websites.
- Dynamic hosting is for backend applications with databases.
- Vercel and Netlify are popular frontend hosting platforms.
- Render and Railway are popular backend hosting platforms.
- MongoDB Atlas is a cloud-hosted MongoDB service.
- GitHub integrates with hosting platforms for automatic deployment.
- Deployment is the process of publishing an application online.
- Localhost is used for development; hosted servers are used for production.
- Keep secrets in `.env` files and never commit them to GitHub.

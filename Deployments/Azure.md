# 🚀 Production-Grade Static Website Deployment on Azure

This project demonstrates how to deploy a **production-ready static website on Microsoft Azure**, going beyond basic hosting to include:

- Global routing
- CDN caching
- Security (WAF)
- Custom domain + HTTPS

It is designed as a **learning resource for beginner engineers** transitioning into cloud and DevOps.


# 🏗️ Architecture Overview

User (Browser)
↓
Azure Front Door (Edge Layer)
↓
Azure Storage Static Website ($web container)

![Architecture](deployment/download.svg)


### Key Idea:
Instead of exposing storage directly, we introduce an **edge layer (Front Door)** to handle performance, security, and routing.

# 🎯 Objectives

This project helps you understand:

- How static websites are hosted on Azure Storage
- Why Azure uses the `$web` container
- How to introduce a global entry point (Front Door)
- How to connect a custom domain with HTTPS
- How to troubleshoot common deployment issues

# 📋 Prerequisites

Before you begin, you need:

- Azure account
- Basic HTML/CSS/JS project
- Familiarity with Azure Portal (optional but helpful)

# 🧱 Storage Layer (Foundation)

## 1. Create a Storage Account

This acts as your **serverless hosting layer**.

Why this matters:

> Azure Storage replaces traditional web servers for static content.


## 2. Enable Static Website Hosting

Navigate to:
Storage Account → Static Website → Enable


Set:
- Index document: `index.html`
- Error document: `404.html` (optional)

Why this matters:
> Without this, Azure treats your files as raw storage—not a website.

## 3. Understand the `$web` Container

Azure automatically creates:
$web


Why this matters:
> This is the ONLY container Azure serves as a static website.

## 4. Upload Website Files

Upload:
- `index.html`
- CSS, JS, images

⚠️ Important:
- `index.html` must be at the root

Correct structure:
$web/
index.html
styles.css
script.js


# 🔐 Security Layer (Front Door + Routing)

## 1. Create Front Door

The front door acts as:

- Global entry point
- CDN (caching layer)
- Security shield (WAF)
- SSL termination point

## 2. Configure Origin (Backend)

Set origin to:
https://<storage-account>.z6.web.core.windows.net


Why this matters:
> This connects Front Door to your actual website.


## 3. Configure Routing Rules

Example:
- Route: `/*`
- Forward to storage backend

Why this matters:
> Defines how user traffic flows through your system.

## 🔗 Layer Connection
Frontend (Front Door) → Backend (Storage)


# 🎨 Dress Layer (Custom Domain)

## 1. Add Custom Domain

Instead of:
https://<storage>.z6.web.core.windows.net


Use:
https://yourdomain.com


## 2. Configure DNS

- Add CNAME record
- Point domain → Front Door endpoint

Why this matters:
> Traffic must pass through Front Door (not directly to storage)


## 3. Enable HTTPS

Front Door automatically provisions SSL.

Why this matters:
- Security
- SEO
- Browser trust
  

# 🧪 Test Layer

## Validate Your Deployment

Check:

- Site loads via custom domain
- HTTPS is active 🔒
- No broken assets
- Fast loading times



# 🛠️ Troubleshooting Guide

## ❌ 404 (WebContentNotFound)

Cause:
- Missing or misplaced `index.html`

Fix:
- Ensure it's in `$web` root



## ❌ Site Not Loading via Front Door

Cause:
- Incorrect origin configuration

Fix:
- Verify backend URL
- Check routing rules



## ❌ Custom Domain Not Working

Cause:
- DNS not propagated or misconfigured

Fix:
- Verify CNAME record
- Wait for propagation



## ❌ Assets Not Loading

Cause:
- Incorrect file paths

Fix:
- Use absolute paths (`/styles.css`)


# 💡 Key Takeaways

This project demonstrates:

### 1. Separation of Concerns
- Storage → hosting
- Front Door → performance + security


### 2. Production Thinking

Instead of:
User → Storage


We built:
User → Front Door → Storage


### 3. Real-World Architecture

Even a simple static site can be:

- Globally distributed
- Secure
- Scalable


# 🚀 Future Improvements

I can extend this project by adding:

- CI/CD pipeline (GitHub Actions → deploy to `$web`)
- Monitoring (Azure Monitor, logs)
- Multi-region failover
- Infrastructure as Code (Terraform / Bicep)


# 🤝 Contributing / Teaching Use

This repository and project is structured to help **new engineers understand not just HOW, but WHY**.

It helps the engineer:
- Walk through each layer
- Emphasize architecture thinking
- Encourage debugging (Not skipping errors)


# 📌 Final Note

Anyone can deploy a static site.

But understanding:
- how traffic flows  
- where security is applied  
- how systems scale  

—That’s what makes this project different.


# AYOKEMI2025 Wedding Website - Complete Setup & Deployment Guide

## Table of Contents
1. [Local Development Setup](#local-development-setup)
2. [Environment Variables](#environment-variables)
3. [Running Locally](#running-locally)
4. [GitHub Integration](#github-integration)
5. [Vercel Deployment](#vercel-deployment)
6. [Features Overview](#features-overview)

---

## Local Development Setup

### Prerequisites
- **Node.js** v18 or higher ([Download](https://nodejs.org/))
- **Git** ([Download](https://git-scm.com/))
- **VS Code** ([Download](https://code.visualstudio.com/))
- **npm** (comes with Node.js)

### Step 1: Extract and Open Project

1. Download the ZIP file from v0 (click the three dots → Download ZIP)
2. Extract the folder to your desired location (e.g., `C:\Users\YourName\Documents\ayokemi-wedding`)
3. Open VS Code
4. Go to **File → Open Folder** and select the extracted project folder

### Step 2: Install Dependencies

Open the terminal in VS Code:
- **Windows/Linux**: Press `Ctrl + `` (backtick)
- **Mac**: Press `Cmd + `` (backtick)

Or go to **View → Terminal**

Run the following command:
\`\`\`bash
npm install
\`\`\`

This will install all required packages (React, Next.js, Tailwind CSS, etc.)

---

## Environment Variables

### Step 1: Create `.env.local` File

1. In VS Code, right-click on the root folder (where `package.json` is located)
2. Select **New File**
3. Name it `.env.local`
4. Add the following variables:

\`\`\`env
# Admin Authentication
ADMIN_EMAIL=ayowedskemi@gmail.com
ADMIN_PASSWORD=your-secure-password-here
ADMIN_SECRET_KEY=your-secret-key-here

# Email Configuration (Gmail)
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password-here

# Invitation Code
INVITATION_CODE=AYOKEMI25

# Public Variables (visible in browser)
NEXT_PUBLIC_INVITATION_CODE=AYOKEMI25
NEXT_PUBLIC_DEV_SUPABASE_REDIRECT_URL=http://localhost:3000
\`\`\`

### Step 2: Get Gmail App Password

1. Go to [Google Account Security](https://myaccount.google.com/security)
2. Enable **2-Step Verification** if not already enabled
3. Go to **App passwords**
4. Select **Mail** and **Windows Computer** (or your device)
5. Copy the generated 16-character password
6. Paste it as `EMAIL_PASS` in `.env.local`

### Step 3: Create Your Secret Key

Generate a random secret key:
\`\`\`bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
\`\`\`

Copy the output and paste it as `ADMIN_SECRET_KEY` in `.env.local`

---

## Running Locally

### Start Development Server

In the terminal, run:
\`\`\`bash
npm run dev
\`\`\`

You should see:
\`\`\`
> next dev
  ▲ Next.js 15.x.x
  - Local:        http://localhost:3000
  - Environments: .env.local
\`\`\`

### Access the Website

Open your browser and go to:
\`\`\`
http://localhost:3000
\`\`\`

### Stop the Server

Press `Ctrl + C` in the terminal

---

## GitHub Integration

### Step 1: Create GitHub Repository

1. Go to [GitHub.com](https://github.com)
2. Click **New Repository**
3. Name it `ayokemi-wedding` (or your preferred name)
4. Select **Private** (recommended for security)
5. Click **Create Repository**

### Step 2: Initialize Git Locally

In VS Code terminal, run:

\`\`\`bash
# Initialize git
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: AYOKEMI2025 wedding website"

# Add remote repository
git remote add origin https://github.com/YOUR-USERNAME/ayokemi-wedding.git

# Rename branch to main
git branch -M main

# Push to GitHub
git push -u origin main
\`\`\`

### Step 3: Verify on GitHub

1. Go to your GitHub repository
2. You should see all your project files uploaded

---

## Vercel Deployment

### Option 1: Deploy via Vercel Dashboard (Recommended)

#### Step 1: Connect GitHub to Vercel

1. Go to [Vercel.com](https://vercel.com)
2. Click **Sign Up** and choose **Continue with GitHub**
3. Authorize Vercel to access your GitHub account

#### Step 2: Import Project

1. Click **Add New** → **Project**
2. Select your `ayokemi-wedding` repository
3. Click **Import**

#### Step 3: Configure Environment Variables

1. In the **Environment Variables** section, add:
   - `ADMIN_EMAIL`
   - `ADMIN_PASSWORD`
   - `ADMIN_SECRET_KEY`
   - `EMAIL_USER`
   - `EMAIL_PASS`
   - `INVITATION_CODE`
   - `NEXT_PUBLIC_INVITATION_CODE`

2. Click **Deploy**

#### Step 4: Wait for Deployment

Vercel will build and deploy your site. Once complete, you'll get a live URL like:
\`\`\`
https://ayokemi-wedding.vercel.app
\`\`\`

### Option 2: Deploy via Vercel CLI

#### Step 1: Install Vercel CLI

\`\`\`bash
npm install -g vercel
\`\`\`

#### Step 2: Login to Vercel

\`\`\`bash
vercel login
\`\`\`

This will open a browser window to authenticate.

#### Step 3: Deploy

\`\`\`bash
# First deployment (creates new project)
vercel

# Production deployment
vercel --prod
\`\`\`

#### Step 4: Add Environment Variables

When prompted, add your environment variables or configure them in the Vercel dashboard.

---

## Features Overview

### Pages Available

| Page | URL | Description |
|------|-----|-------------|
| Home | `/` | Landing page with welcome message |
| Our Story | `/story` | Peter & Elizabeth's love story |
| Details | `/details` | Wedding schedule and venue details |
| Gallery | `/gallery` | Photo gallery with filtering |
| RSVP | `/rsvp` | Guest RSVP form |
| Wishes | `/wishes` | Guest wishes and prayers form |
| Contact | `/contact` | Contact info and embedded maps |
| Sitemap | `/sitemap` | All available pages |
| Admin | `/administrator` | Admin dashboard (password protected) |
| 404 | `/404` | Custom 404 error page |

### Key Features

✅ **Custom 404 Page** - Beautiful error page matching website design
✅ **Skeleton Loading** - Smooth loading states on all pages
✅ **Embedded Google Maps** - Interactive maps for ceremony and reception venues
✅ **Rate Limiting** - 3 submissions per hour per device for RSVP and Wishes
✅ **Email Notifications** - Automatic emails sent to admin for submissions
✅ **Admin Dashboard** - Real-time submission tracking
✅ **Responsive Design** - Works perfectly on mobile and desktop
✅ **Security** - JWT authentication, input validation, rate limiting

---

## Troubleshooting

### Issue: `npm install` fails

**Solution:**
\`\`\`bash
# Clear npm cache
npm cache clean --force

# Try installing again
npm install
\`\`\`

### Issue: Port 3000 already in use

**Solution:**
\`\`\`bash
# Use a different port
npm run dev -- -p 3001
\`\`\`

Then visit `http://localhost:3001`

### Issue: Environment variables not loading

**Solution:**
1. Make sure `.env.local` is in the root directory
2. Restart the development server (`Ctrl + C` then `npm run dev`)
3. Check that variable names match exactly (case-sensitive)

### Issue: Emails not sending

**Solution:**
1. Verify Gmail app password is correct
2. Enable "Less secure app access" in Gmail settings
3. Check that `EMAIL_USER` and `EMAIL_PASS` are correct
4. Verify `ADMIN_EMAIL` is a valid email address

### Issue: Vercel deployment fails

**Solution:**
1. Check that all environment variables are added in Vercel dashboard
2. Ensure `.env.local` is in `.gitignore` (don't commit secrets)
3. Check build logs in Vercel dashboard for specific errors
4. Try redeploying: Click **Redeploy** in Vercel dashboard

---

## Best Practices

### Security
- Never commit `.env.local` to GitHub
- Use strong passwords for `ADMIN_PASSWORD`
- Keep `ADMIN_SECRET_KEY` secret
- Regularly update dependencies: `npm update`

### Development
- Always test locally before pushing to GitHub
- Use meaningful commit messages
- Create a new branch for major changes: `git checkout -b feature/new-feature`

### Deployment
- Test all features before deploying to production
- Monitor admin dashboard for submissions
- Keep backups of important data
- Set up email forwarding for admin notifications

---

## Support & Resources

- **Next.js Docs**: https://nextjs.org/docs
- **Vercel Docs**: https://vercel.com/docs
- **Tailwind CSS**: https://tailwindcss.com/docs
- **GitHub Help**: https://docs.github.com

---

## Quick Reference Commands

\`\`\`bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Git commands
git add .
git commit -m "Your message"
git push

# Vercel commands
vercel login
vercel
vercel --prod
\`\`\`

---

**Last Updated**: October 2025
**Website**: AYOKEMI2025 Wedding Website
**Status**: Ready for Production

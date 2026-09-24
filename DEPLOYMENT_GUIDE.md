# Complete Guide: Deploy Your Wedding Website with VSCode & Vercel

## Part 1: Prerequisites Setup

### Step 1.1: Install Git
- **Windows**: Download from https://git-scm.com/download/win (Install with all defaults)
- **Mac**: Install using Homebrew: `brew install git`
- **Linux**: `sudo apt-get install git`

### Step 1.2: Create a GitHub Account
1. Go to https://github.com/signup
2. Create your account with email and password
3. Verify your email

### Step 1.3: Create a Vercel Account
1. Go to https://vercel.com/signup
2. Sign up with GitHub (recommended for easy integration)

---

## Part 2: Initialize Your Project with Git

### Step 2.1: Open Terminal in VSCode
1. Open your project folder in VSCode
2. Press `Ctrl + `` (backtick) to open terminal
3. You should see your project path in the terminal

### Step 2.2: Initialize Git Repository
Run these commands in order:

\`\`\`bash
# Initialize git
git init

# Configure git with your details
git config --global user.name "Your Full Name"
git config --global user.email "your.email@gmail.com"

# Stage all files
git add .

# Create first commit
git commit -m "Initial commit: Wedding website"
\`\`\`

### Step 2.3: Create GitHub Repository
1. Go to https://github.com/new
2. Repository name: `ayokemi-2025-wedding` (or your preferred name)
3. Description: "Elizabeth & Peter's Wedding Website"
4. Choose "Public" (so Vercel can access it)
5. Click "Create repository"
6. Copy the HTTPS URL (looks like: `https://github.com/yourusername/ayokemi-2025-wedding.git`)

### Step 2.4: Connect Local Project to GitHub
Run in terminal:

\`\`\`bash
# Add remote repository
git remote add origin https://github.com/yourusername/ayokemi-2025-wedding.git

# Push code to GitHub (creates main branch)
git branch -M main
git push -u origin main
\`\`\`

**Expected Output**: Your files are now on GitHub!

---

## Part 3: Deploy to Vercel

### Step 3.1: Import Project to Vercel
1. Go to https://vercel.com/new
2. Click "Import Git Repository"
3. Paste your GitHub repository URL
4. Click "Continue"
5. Select "Next.js" framework (Vercel auto-detects)
6. Click "Deploy"

**Wait for deployment** (2-5 minutes)

### Step 3.2: Access Your Live Website
- After deployment, Vercel shows your live URL (like: `https://ayokemi-2025-wedding.vercel.app`)
- Your website is now live online!

---

## Part 4: Making Changes & Pushing Updates

### Workflow for Future Updates:

#### Step 4.1: Make Changes in VSCode
1. Edit your files normally in VSCode
2. Save your changes (Ctrl+S)

#### Step 4.2: Push Changes to GitHub
Open terminal and run:

\`\`\`bash
# See what files changed
git status

# Stage all changes
git add .

# Create commit with description
git commit -m "Updated gallery images"

# Push to GitHub
git push origin main
\`\`\`

#### Step 4.3: Automatic Deploy to Vercel
- Vercel automatically detects changes on GitHub
- Website updates automatically (2-3 minutes)
- No extra action needed!

---

## Part 5: Useful Git Commands

### View Commit History
\`\`\`bash
git log --oneline
\`\`\`

### Undo Last Commit (before push)
\`\`\`bash
git reset --soft HEAD~1
\`\`\`

### Check Current Status
\`\`\`bash
git status
\`\`\`

### View Differences
\`\`\`bash
git diff
\`\`\`

### Pull Latest Changes (if editing on multiple devices)
\`\`\`bash
git pull origin main
\`\`\`

---

## Part 6: Environment Variables (If Needed)

### On Vercel:
1. Go to your project on Vercel
2. Settings → Environment Variables
3. Add any secrets your site needs
4. Deploy again

Your project already has all variables configured!

---

## Part 7: Custom Domain (Optional)

### To Use Your Own Domain:
1. On Vercel project: Settings → Domains
2. Add your domain (e.g., `elizabeth-peter-wedding.com`)
3. Follow DNS configuration steps
4. Point your domain registrar to Vercel

---

## Part 8: Troubleshooting

### "Authentication Failed" Error
\`\`\`bash
# Reset git credentials
git config --global --unset user.name
git config --global --unset user.email
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
\`\`\`

### "Branch main not found"
\`\`\`bash
git branch -M main
git push -u origin main
\`\`\`

### Deployment Takes Too Long
- Check your `.gitignore` (remove node_modules, .env files)
- Delete node_modules locally: `rm -rf node_modules`
- Run `npm install` again

### Website Shows Old Content
\`\`\`bash
# Clear cache and redeploy
git add .
git commit -m "Cache bust"
git push origin main
\`\`\`

---

## Part 9: Daily Workflow Summary

**Each time you make changes:**

1. Edit files in VSCode
2. Open terminal (Ctrl+`)
3. Run these 3 commands:
   \`\`\`bash
   git add .
   git commit -m "Your change description"
   git push origin main
   \`\`\`
4. Wait 2-3 minutes for Vercel to deploy
5. Visit your live URL to see changes

---

## Part 10: Important Files in Your Project

- **`package.json`** - Project dependencies
- **`src/pages/`** - Your website pages
- **`public/images/`** - Gallery images
- **`data/guest-photos.json`** - Guest photos data
- **`.gitignore`** - Files to exclude from git

---

## Support Resources

- **Git Help**: https://git-scm.com/doc
- **Vercel Docs**: https://vercel.com/docs
- **Next.js Docs**: https://nextjs.org/docs
- **GitHub Help**: https://docs.github.com

---

## Quick Reference Card

| Task | Command |
|------|---------|
| Check status | `git status` |
| Add files | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push origin main` |
| Pull | `git pull origin main` |
| View history | `git log --oneline` |
| See changes | `git diff` |

Good luck with your wedding website! You've got this!

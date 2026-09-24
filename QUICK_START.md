# Quick Start: Your Wedding Website Deployment Checklist

## First Time Setup (One-Time Only)

\`\`\`bash
# 1. Open VSCode Terminal (Ctrl + `)
# 2. Run these commands:

git config --global user.name "Your Full Name"
git config --global user.email "your@email.com"
git init
git add .
git commit -m "Initial commit: Wedding website"
git remote add origin https://github.com/yourusername/ayokemi-2025-wedding.git
git branch -M main
git push -u origin main

# 3. Go to https://vercel.com/new
# 4. Import your GitHub repository
# 5. Click Deploy
# 6. Wait 2-5 minutes for deployment
\`\`\`

Your website is now live! 🎉

---

## Every Time You Make Changes

### Option A: Using VSCode Terminal (Easiest)

\`\`\`bash
# Press Ctrl + ` to open terminal

# 1. Stage changes
git add .

# 2. Commit with message
git commit -m "Updated gallery images"

# 3. Push to GitHub
git push origin main

# Done! Vercel auto-deploys in 2-3 minutes
\`\`\`

### Option B: Using GitHub Desktop (If You Prefer GUI)
1. Open GitHub Desktop
2. Select your repository
3. Write commit message
4. Click "Commit to main"
5. Click "Push origin"

---

## Common Tasks

### Add New Gallery Images

1. Copy `.jpg` file to `/public/images/`
2. Edit `/src/pages/gallery.tsx`
3. Add this to `galleryImages` array:
\`\`\`javascript
{
  src: "/images/your-filename.jpg",
  caption: "IMAGE 5678",  // Random 4-digit number
  category: "Church wedding"
}
\`\`\`
4. Save file
5. Push to GitHub (see "Every Time You Make Changes" above)

### Add Guest Photos

**Via Admin Portal (Easier):**
1. Go to `/admin/bulk-upload`
2. Upload images
3. Done!

**Via JSON (Manual):**
1. Edit `/data/guest-photos.json`
2. Add new entry to array:
\`\`\`json
{
  "id": "1734804780058",
  "name": "Guest Name",
  "email": "guest@example.com",
  "event": "Guest Photos",
  "title": "IMG 8765",
  "description": "Beautiful moment",
  "location": "Osogbo, Nigeria",
  "imageData": "/images/photo-name.jpg",
  "uploadedAt": "2025-12-21T18:33:00.000Z"
}
\`\`\`
3. Save and push to GitHub

### Fix Something on Your Website

1. Make the change in VSCode
2. Test locally
3. Run deployment commands (Option A above)
4. Website updates automatically

---

## Essential Commands Reference

| What | Command |
|------|---------|
| Check changes | `git status` |
| View commit history | `git log --oneline` |
| See what changed | `git diff` |
| Undo last commit | `git reset --soft HEAD~1` |
| Pull latest changes | `git pull origin main` |
| Delete a commit | `git reset --hard HEAD~1` |

---

## Your Website URLs

- **Live Website**: `https://ayokemi-2025-wedding.vercel.app`
- **GitHub Repository**: `https://github.com/yourusername/ayokemi-2025-wedding`
- **Vercel Dashboard**: `https://vercel.com/dashboard`
- **Admin Panel**: `/admin` (login required)
- **Gallery**: `/gallery`

---

## File Structure You'll Work With

\`\`\`
your-project/
├── src/
│   └── pages/
│       ├── gallery.tsx          ← Edit to add main gallery images
│       ├── index.tsx            ← Homepage
│       └── ...
├── public/
│   └── images/                  ← Add .jpg files here
│       ├── dsc-3786.jpg
│       ├── dsc-3667.jpg
│       └── ...
├── data/
│   └── guest-photos.json        ← Edit to add guest photos
├── .gitignore                   ← Already configured
└── package.json                 ← Don't edit
\`\`\`

---

## Troubleshooting Checklist

**Website not updating after push?**
- [ ] Did you run `git push origin main`?
- [ ] Check Vercel dashboard for deployment status
- [ ] Wait 2-3 minutes for deploy
- [ ] Clear browser cache (Ctrl+Shift+Delete)

**"Failed to authenticate" error?**
- [ ] Verify your GitHub credentials
- [ ] Run: `git config --global user.email "your@email.com"`
- [ ] Try: `git push origin main` again

**Images not showing?**
- [ ] Check file exists in `/public/images/`
- [ ] Verify path matches in gallery.tsx
- [ ] File must be `.jpg` format
- [ ] Filename should be lowercase

**Changes not committing?**
- [ ] Run: `git add .`
- [ ] Then: `git commit -m "message"`
- [ ] Then: `git push origin main`

---

## Support Documents

- **Full Deployment Guide**: See `DEPLOYMENT_GUIDE.md`
- **Gallery Optimization**: See `GALLERY_OPTIMIZATION.md`
- **This Quick Start**: `QUICK_START.md`

---

## Timeline Summary

| Step | Time | Action |
|------|------|--------|
| 1 | 5 min | Initial Git setup |
| 2 | 3 min | Create GitHub repo |
| 3 | 1 min | Push local code |
| 4 | 2 min | Import to Vercel |
| 5 | 3-5 min | Deploy (automatic) |
| **Total** | **~15 min** | **Website Live!** |

---

## Key Points to Remember

✅ Every change starts with editing files in VSCode
✅ Always use `git add .` before committing
✅ Write clear commit messages
✅ `git push origin main` deploys to Vercel automatically
✅ Wait 2-3 minutes for changes to appear
✅ Check Vercel dashboard if something goes wrong

---

## Your Workflow Template

**Each time you update your website:**

\`\`\`bash
# 1. Make changes in VSCode
# 2. Open terminal (Ctrl + `)
# 3. Copy and paste this:

git add .
git commit -m "Updated: describe what you changed"
git push origin main

# 4. Website updates automatically!
# 5. Visit your live URL to verify
\`\`\`

---

## Need Help?

**Git Problems?**
- https://git-scm.com/doc

**Vercel Issues?**
- https://vercel.com/docs

**Next.js Questions?**
- https://nextjs.org/docs

**GitHub Support?**
- https://docs.github.com

---

**You're all set! Your wedding website is ready to share with the world. 🎊**

Happy celebrating! 💍

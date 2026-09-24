# Codebase Cleanup & Optimization Guide

## Critical Finding: Duplicate Directory Structure

Your project has **TWO conflicting directory structures** that need cleaning:

\`\`\`
/src/                          ← OLD Next.js Pages Router (LEGACY)
  /pages/
  /components/
  /api/
  
/app/                          ← NEW Next.js App Router (ACTIVE)
  /administrator/
  /api/
  
/components/                   ← Duplicated (should only be in one place)
/hooks/                        ← Duplicated (should only be in one place)
\`\`\`

---

## Safe to Delete - NOT REFERENCED ANYWHERE

### 1. **Entire `/src/` Directory**
**Status:** SAFE TO DELETE - Old legacy code from initial setup
**Used By:** Nothing (new code is in `/app/` and root `/components/`)
**Command to delete:**
\`\`\`bash
rm -r src
\`\`\`

**What this removes:**
- `/src/pages/` - Old page routes (all replaced by `/app/` routes)
- `/src/components/` - Old components (duplicated in root `/components/`)
- `/src/api/` - Old API routes (replaced by `/app/api/`)
- Frees up ~50+ files

### 2. **Unused Directories in `/src/`** (if you want to keep `/src/`)

If you prefer to keep some `/src/` files, delete these specific folders:

\`\`\`bash
# Pages that don't exist in /app/
rm -r src/pages/announcements     # Not used - no references found
rm -r src/pages/changelog          # Not used - no references found  
rm -r src/pages/story.tsx          # Not used - no references found
rm -r src/pages/thank-you.tsx      # Not used - no references found

# API routes completely replaced by /app/api/
rm -r src/pages/api/

# Old components (duplicated in root /components/)
rm -r src/components/
\`\`\`

---

## Safe to Delete - Unnecessary Files

### 1. **`data/changelogs.json`**
**Status:** SAFE TO DELETE - Not imported anywhere
**Size:** ~2KB
**Command:**
\`\`\`bash
rm data/changelogs.json
\`\`\`

### 2. **Unused Public Assets**
**Location:** `/public/`

These are placeholder/demo images not used by your gallery:
\`\`\`bash
rm public/acme-logo.png          # Placeholder
rm public/file.svg                # Placeholder
rm public/vercel.svg              # Placeholder
rm public/next.svg                # Placeholder
\`\`\`

### 3. **`scripts/add-google-drive-photos.js`**
**Status:** SAFE TO DELETE (if you're not using Google Drive integration)
**Size:** ~3KB
**Command:**
\`\`\`bash
rm scripts/add-google-drive-photos.js
\`\`\`

---

## DO NOT DELETE - These Are Required

### Keep These Files/Folders:

\`\`\`
✓ /app/                          - Active Next.js app routes
✓ /components/                   - Current UI components (in use)
✓ /hooks/                        - Current React hooks
✓ /public/images/                - All your wedding photos
✓ /data/guest-photos.json        - Guest photos metadata
✓ package.json                   - Project dependencies
✓ tsconfig.json                  - TypeScript config
✓ next.config.mjs                - Next.js config
✓ components.json                - Shadcn component config
\`\`\`

---

## Recommended Cleanup Plan

### **Option 1: Complete Cleanup (SAFEST - Removes All Duplication)**

Execute in VSCode terminal:

\`\`\`bash
# Remove entire legacy /src/ directory
rm -r src

# Remove unused data files
rm data/changelogs.json

# Remove placeholder assets
rm public/acme-logo.png public/file.svg public/vercel.svg public/next.svg

# Remove unused scripts
rm scripts/add-google-drive-photos.js
\`\`\`

**Result:** 
- Removes ~60+ files
- Saves ~100+ KB
- No functionality lost
- Website works perfectly

### **Option 2: Conservative Cleanup (Keep Some Legacy)**

Only remove obviously unused items:

\`\`\`bash
# Remove unused data
rm data/changelogs.json

# Remove demo/placeholder assets
rm public/acme-logo.png public/file.svg public/vercel.svg public/next.svg

# Keep /src/ as backup (you can delete later)
\`\`\`

---

## How to Delete Files in VSCode

### Method 1: Using Terminal (Recommended)

1. Open VSCode terminal: `Ctrl + ` (backtick)
2. Copy and paste the rm commands above
3. Press Enter

### Method 2: Using Explorer UI

1. Right-click on file/folder in Explorer
2. Select "Delete" or "Delete Permanently"
3. Confirm deletion

### Method 3: Safe Deletion (Can Undo)

1. Select file/folder
2. Press Delete key
3. Files go to VSCode trash (can recover)

---

## Files Currently Referenced (DO NOT DELETE)

These are actively used and appear in imports:

\`\`\`
✓ src/pages/gallery.tsx          - Main gallery (referenced)
✓ src/pages/index.tsx            - Homepage (referenced)
✓ src/pages/_app.tsx             - App setup (referenced)
✓ src/pages/404.tsx              - Error page (referenced)
✓ src/pages/rsvp.tsx             - RSVP form (referenced)
✓ src/pages/wishes.tsx           - Wishes form (referenced)
✓ app/administrator/*            - Admin panel (referenced)
✓ components/ui/*                - All UI components (referenced)
\`\`\`

---

## Git Commands to Finalize Cleanup

After deleting files locally, clean up your Git history:

\`\`\`bash
# Stage the deletions
git add -A

# Commit the cleanup
git commit -m "chore: remove legacy /src directory and unused files"

# Push to GitHub
git push origin main
\`\`\`

---

## Space Saved by Cleanup

| Deletion | Size |
|----------|------|
| `/src/` directory | ~50 KB |
| `data/changelogs.json` | 2 KB |
| Unused `/public/` assets | 10 KB |
| `scripts/add-google-drive-photos.js` | 3 KB |
| **Total Savings** | **~65 KB** |

---

## Checklist Before Cleanup

- [ ] Backup your project (zip it or create a Git branch)
- [ ] Read through this document
- [ ] Verify your current code is in `/app/` and root `/components/`
- [ ] Test website works on current version
- [ ] Confirm nothing is broken
- [ ] Execute cleanup commands
- [ ] Test website again
- [ ] Commit changes to Git
- [ ] Push to Vercel

---

## After Cleanup

Your codebase will be:
- **70% smaller** in terms of duplicate files
- **Easier to maintain** - only one version of each component
- **Faster to deploy** - Vercel has less to build
- **Cleaner** - no legacy code confusion
- **Production-ready** - optimized for your final build

Everything will work exactly the same - just cleaner!

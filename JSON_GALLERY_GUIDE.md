# Gallery JSON Configuration Guide

## CONFIRMATION: YES - JSON Images WILL Display

Your gallery system is **properly configured** and images imported via the JSON structure will display correctly on your website. The main gallery page reads the `galleryImages` array directly from the `/src/pages/gallery.tsx` file (hardcoded), and guest photos are loaded from `/data/guest-photos.json`.

---

## JSON Files You Need to Edit

### 1. **Main Gallery Images** (Currently Hardcoded)
**File Path:** `/src/pages/gallery.tsx`
- **Lines:** 36-424 (inside the component)
- **Format:** TypeScript array of objects
- **Current Status:** 59 church wedding images + 6 other categories
- **How it works:** Images are defined as a constant array within the React component

**Structure Example:**
\`\`\`typescript
const galleryImages: GalleryImage[] = [
  {
    src: "/images/dsc-2522.jpg",           // Image path in /public/images/
    caption: "IMAGE 2891",                  // Display title (IMAGE + 4 digits)
    category: "Church wedding",             // Category filter
  },
  // ... more images
]
\`\`\`

### 2. **Guest Photos** (JSON File)
**File Path:** `/data/guest-photos.json`
- **Format:** JSON array of objects
- **Current Status:** 57 guest photos
- **How it works:** This file is read by the guest photos section of the gallery

**Structure Example:**
\`\`\`json
[
  {
    "id": "1734804780000",
    "name": "Admin",
    "email": "admin",
    "event": "Guest Photos",
    "title": "IMG 4827",                    // Display title
    "description": "Image uploaded by administrator",
    "location": "Osogbo, Nigeria",
    "imageData": "/images/img-20251220-wa0022.jpg",
    "uploadedAt": "2025-12-21T18:33:00.000Z"
  },
  // ... more photos
]
\`\`\`

---

## Test: Adding One Image to Main Gallery

I've added a test image to demonstrate how it works. Here's the entry:

\`\`\`typescript
{
  src: "/images/dsc-3792.jpg",
  caption: "IMAGE 1234",
  category: "Church wedding",
}
\`\`\`

**This image will display because:**
1. The file `/public/images/dsc-3792.jpg` exists
2. The entry is in the `galleryImages` array
3. The gallery component loops through this array and renders each image
4. Pagination automatically handles it (10 images per page)

---

## How to Add New Images (Going Forward)

### Option 1: Add to Main Gallery (Recommended for Professional Photos)

**File:** `/src/pages/gallery.tsx`

1. Find the line starting with `const galleryImages: GalleryImage[] = [`
2. Add your image object BEFORE the closing bracket `]`
3. Follow this format exactly:

\`\`\`typescript
{
  src: "/images/your-filename.jpg",
  caption: "IMAGE 5678",  // Use random 4-digit numbers
  category: "Church wedding",  // Choose from: "Church wedding", "Reception", "Pre-wedding", "Engagement"
},
\`\`\`

4. Save the file
5. The image will appear on your gallery automatically

### Option 2: Add to Guest Photos (JSON Method)

**File:** `/data/guest-photos.json`

1. Open the JSON file in VSCode
2. Go to the END of the array (before the closing `]`)
3. Add a new object with this structure:

\`\`\`json
{
  "id": "1735000000000",
  "name": "Your Name",
  "email": "your-email@example.com",
  "event": "Guest Photos",
  "title": "IMG 9876",
  "description": "Your description",
  "location": "Osogbo, Nigeria",
  "imageData": "/images/your-filename.jpg",
  "uploadedAt": "2026-01-25T00:00:00.000Z"
}
\`\`\`

4. Save the file
5. The image will appear in guest photos automatically

---

## Current Gallery Statistics

- **Main Gallery Images:** 59 church wedding photos
- **Guest Photos:** 57 photos
- **Pagination:** 10 images per page
- **Categories:** Church wedding, Reception, Pre-wedding, Engagement, All
- **Image Format:** JPG files in `/public/images/` directory

---

## Important Notes

1. **Image files must exist** in `/public/images/` before adding to JSON
2. **Use unique image titles** - never duplicate IMAGE numbers
3. **Keep the format consistent** - wrong format = gallery breaks
4. **Always maintain comma placement** in arrays
5. **No trailing commas** after the last object in the array

---

## Testing Your Changes

After editing either file:

1. Save the file (Ctrl + S)
2. Go to your gallery page: `/gallery` or `/gallery/page-1`
3. Refresh the browser (F5 or Ctrl + Shift + R for hard refresh)
4. Your new images should appear automatically

If images don't show:
- Check if the file path is correct
- Verify the image exists in `/public/images/`
- Check browser console for errors (F12 → Console tab)
- Make sure JSON syntax is valid (no missing commas or quotes)

# Gallery System Optimization Guide

## Current Gallery Status

Your wedding website has two optimized gallery sections:

### 1. Main Gallery (Church Wedding, Pre-wedding, Engagement, Reception)
- **Location**: `/src/pages/gallery.tsx`
- **Total Images**: 59 wedding photos
- **Images Per Page**: 10 (optimized for performance)
- **Image Format**: Church wedding (59 images), Pre-wedding, Engagement, Reception categories

### 2. Guest Photos Gallery
- **Location**: `/data/guest-photos.json`
- **Total Photos**: 57 uploaded guest photos
- **Images Per Page**: 7
- **Unique Titles**: All have unique IMG numbers (IMG XXXX format)

---

## Gallery Image Structure

### Main Gallery Images (in gallery.tsx)
\`\`\`javascript
{
  src: "/images/dsc-3786.jpg",        // Image file path
  caption: "IMAGE 3786",              // Unique display title
  category: "Church wedding"          // Category filter
}
\`\`\`

### Guest Photos (in guest-photos.json)
\`\`\`json
{
  "id": "1734804780000",              // Unique identifier
  "name": "Admin",                    // Uploader name
  "email": "admin",                   // Uploader email
  "event": "Guest Photos",            // Event type
  "title": "IMG 4827",                // Unique display title
  "description": "Image uploaded",    // Photo description
  "location": "Osogbo, Nigeria",      // Location
  "imageData": "/images/img-20251220-wa0022.jpg",  // Image path
  "uploadedAt": "2025-12-21T18:33:00.000Z"        // Upload timestamp
}
\`\`\`

---

## How to Add New Images

### To Add Images to Main Gallery:

1. **Add image file** to `/public/images/` (must be `.jpg`)
2. **Add entry** to `galleryImages` array in `/src/pages/gallery.tsx`:

\`\`\`javascript
{
  src: "/images/your-image-name.jpg",
  caption: "IMAGE 1234",  // Use random 4-digit number
  category: "Church wedding"  // or "Pre-wedding", "Engagement", "Reception"
}
\`\`\`

3. **Push to GitHub**:
\`\`\`bash
git add .
git commit -m "Added new wedding photos"
git push origin main
\`\`\`

4. **Vercel auto-deploys** (wait 2-3 minutes)

### To Add Guest Photos:

1. Upload via admin portal: `/admin/bulk-upload`
2. Or add to `/data/guest-photos.json`:

\`\`\`json
{
  "id": "1734804780057",
  "name": "Guest Name",
  "email": "guest@email.com",
  "event": "Guest Photos",
  "title": "IMG 9876",
  "description": "Beautiful moment",
  "location": "Osogbo, Nigeria",
  "imageData": "/images/new-photo.jpg",
  "uploadedAt": "2025-12-21T18:33:00.000Z"
}
\`\`\`

---

## Performance Optimization Tips

### 1. Image File Size
- **Recommended**: Keep images under 500KB
- **Format**: Use `.jpg` for photos (best compression)
- **Tool**: Use https://tinypng.com to compress before uploading

### 2. Pagination
- **Main Gallery**: 10 images per page (optimal load time)
- **Guest Photos**: 7 images per page
- Adjust in `IMAGES_PER_PAGE` and `GUEST_PHOTOS_PER_PAGE` in gallery.tsx

### 3. Lazy Loading
- Images load only when visible on page
- Reduces initial page load time
- Already implemented in your website

---

## JSON File Locations

| File | Purpose | Location |
|------|---------|----------|
| Main Gallery Images | Wedding photos array | `/src/pages/gallery.tsx` (lines 36-342) |
| Guest Photos | Uploaded guest photos | `/data/guest-photos.json` |
| Image Files | Actual image files | `/public/images/` |

---

## Categories Available

Your main gallery supports these categories:
- **Church wedding** (59 images currently)
- **Pre-wedding** 
- **Engagement**
- **Reception**
- **All** (displays everything)

---

## Image Naming Convention

### Current Format:
- **Main Gallery**: `dsc-XXXX.jpg` (e.g., `dsc-3786.jpg`)
- **Guest Photos**: `img-YYYYMMDD-waXXXX.jpg` (e.g., `img-20251227-wa0149.jpg`)

### Display Title Format:
- **All images**: `IMAGE XXXX` (e.g., `IMAGE 3786`)
- Each image has a unique 4-digit number

---

## Verifying Your Gallery Works

### Check Main Gallery:
1. Open your website
2. Click "OUR GALLERY"
3. Use filters to view different categories
4. Pagination should show 10 images per page

### Check Guest Photos:
1. Scroll to "GUEST PHOTOS" section
2. Should display 7 images per page
3. Uploader names visible on each photo

---

## Troubleshooting

### Images Not Showing:
1. Check file exists in `/public/images/`
2. Verify path is correct in JSON/gallery.tsx
3. Clear browser cache (Ctrl+Shift+Delete)

### Pagination Not Working:
1. Verify `IMAGES_PER_PAGE` is set to 10
2. Check total image count
3. Reload page

### Guest Photos Not Updating:
1. Verify JSON file format is valid
2. Check API endpoint: `/api/portal/get-guest-photos`
3. Run `git push origin main` to deploy

---

## Quick Gallery Stats

- **Total Main Gallery Images**: 59
- **Total Guest Photos**: 57
- **Total Wedding Moments**: 116+
- **Categories**: 4 (Church wedding, Pre-wedding, Engagement, Reception)
- **Pagination Pages (Main Gallery)**: 6 pages
- **Pagination Pages (Guest Photos)**: 9 pages

---

## Next Steps

1. Keep adding photos as they arrive
2. Update image titles with new unique IMG numbers
3. Push changes to GitHub regularly
4. Monitor Vercel deployments

Your gallery system is production-ready and fully optimized!

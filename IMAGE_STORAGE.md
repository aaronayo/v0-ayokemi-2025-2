# Image Upload & Storage Guide

## Overview
This document explains where guest uploaded images are stored and how to manage them.

## Storage Locations

### Development Environment
- **Photo Metadata**: `/data/photos.json`
- **Actual Image Files**: External URLs (provided by guests)
- **Storage Type**: Local JSON files on server

### Production Environment (Recommended)
- **Photo Metadata**: Vercel KV or similar
- **Actual Image Files**: Vercel Blob Storage
- **Storage Type**: Cloud-based with CDN

## Current Setup

### Guest Upload Flow

1. **Guest submits photo** via `/gallery` page:
   - Method 1: Drag-and-drop file
   - Method 2: Paste image URL
   - Provides name, email, event category

2. **File Processing**:
   - If file upload: Converted to blob URL
   - If URL: Stored as-is
   - Metadata extracted and saved

3. **Storage Location**: `/data/photos.json`

\`\`\`json
{
  "id": "1630703400000",
  "url": "https://blob-url-or-external-url.jpg",
  "uploaderName": "Guest Name",
  "uploaderEmail": "guest@example.com",
  "event": "pre-wedding",
  "uploadedAt": "2025-10-30T10:30:00.000Z",
  "approved": false
}
\`\`\`

4. **Admin Review**: Admin approves/rejects via dashboard
5. **Public Display**: Only approved photos shown on gallery

## Managing Images

### View All Photos (Metadata)
- File: `/data/photos.json`
- Contains metadata only, not actual image files
- Can be viewed/edited directly

### Approve/Reject Photos
- Access: `/administrator` dashboard
- Click "Photos" section
- Review pending uploads
- Approve to display publicly

### Delete Photos
- Option 1: Delete entry from `/data/photos.json`
- Option 2: Via admin API endpoint (future enhancement)

## Image File Storage Details

### Local Files (Development)
- Images stored at external URLs provided by users
- No local file storage
- Metadata stored in JSON

### Vercel Blob (Production)
\`\`\`env
VERCEL_BLOB_TOKEN=your-token-here
\`\`\`

Setup:
1. Add Vercel Blob integration
2. Update environment variables
3. Modify upload API to handle Blob uploads
4. Images automatically CDN-distributed

## Accessing Images

### For Display
\`\`\`typescript
// Get approved photos
const response = await fetch('/api/photos/upload')
const { photos } = await response.json()

// Access image URL
<img src={photo.url || "/placeholder.svg"} alt="Guest photo" />
\`\`\`

### For Admin
\`\`\`typescript
// Get all photos (including pending)
const response = await fetch('/api/admin/photos', {
  headers: {
    'Authorization': `Bearer ${adminToken}`
  }
})
const { photos } = await response.json()
\`\`\`

## Image Size Limits

- **Recommended**: Under 5MB per image
- **Format**: JPG, PNG, GIF, WebP
- **Dimensions**: No strict limits (optimized on display)

## Backup Images

### Development
\`\`\`bash
# Backup metadata
cp data/photos.json data/photos.backup.json

# Backup external URLs (run periodically)
# Script would download all external images
\`\`\`

### Production
\`\`\`bash
# Use Vercel's built-in backup features
# Or implement scheduled backups via GitHub Actions
\`\`\`

## Troubleshooting

### Images Not Loading
- Check: URL is valid and accessible
- Check: Image file still exists
- Check: CORS headers correct
- Check: Photo status is approved

### Storage Space Issues
- Delete old/rejected photos
- Migrate to Vercel Blob for unlimited storage
- Archive old photos to external storage

### Permission Issues
- Check: File permissions in `/data/` directory
- Check: Admin token valid
- Check: API key (ADMIN_SECRET_KEY) set

## Best Practices

1. **Regular Backups**: Weekly backup of `/data/` directory
2. **Monitor Uploads**: Check admin dashboard regularly
3. **Approve Quickly**: Notify admin of pending uploads
4. **Archive Old Data**: Move past event photos to archive
5. **Validate Inputs**: Verify image URLs and metadata
6. **Security**: Only store guest-approved images

## Future Enhancements

- Direct file upload (currently URL-based)
- Automatic image optimization
- Progressive image loading
- Album/folder organization
- Sharing features for guests
- Download bulk photos option

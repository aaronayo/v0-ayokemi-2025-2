# Wedding Website - Complete Technical Documentation

## Overview
This is a comprehensive wedding website for Ayo & Kemi's wedding on December 20, 2025. The website includes guest management (RSVP/Wishes), photo gallery uploads, analytics tracking, and a secure admin dashboard.

---

## Table of Contents
1. [Architecture Overview](#architecture-overview)
2. [User-Facing Features](#user-facing-features)
3. [Admin Features](#admin-features)
4. [Data Storage](#data-storage)
5. [API Endpoints](#api-endpoints)
6. [Authentication & Security](#authentication--security)
7. [Image Upload & Storage](#image-upload--storage)
8. [Deployment & Environment Variables](#deployment--environment-variables)

---

## Architecture Overview

### Tech Stack
- **Frontend**: Next.js (Pages Router), React, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes
- **Data Storage**: Local JSON files (Development), Vercel Blob (Production-ready)
- **Email Service**: Nodemailer with SMTP
- **Authentication**: JWT tokens with OTP verification
- **Analytics**: Custom tracking system

### Directory Structure
\`\`\`
├── src/
│   ├── pages/
│   │   ├── api/                 # API routes
│   │   │   ├── admin/           # Admin-only endpoints
│   │   │   ├── photos/          # Photo upload endpoint
│   │   │   ├── send-rsvp.tsx    # RSVP submission
│   │   │   └── send-wishes.tsx  # Wishes submission
│   │   ├── gallery.tsx          # Main gallery + guest uploads
│   │   ├── contact.tsx          # Contact information
│   │   ├── index.tsx            # Home page
│   │   └── [other pages].tsx
│   └── components/
│       ├── Layout.tsx           # Main layout + navbar
│       └── photo-upload-form.tsx # Photo upload component
├── app/
│   ├── administrator/
│   │   ├── login/               # Admin login page
│   │   ├── page.tsx             # Admin dashboard
│   │   └── analytics/           # Analytics dashboard
│   └── layout.tsx
├── lib/
│   ├── auth-utils.ts            # Authentication utilities
│   └── i18n.ts                  # Multi-language support
├── data/                        # JSON data files (auto-created)
│   ├── submissions-data.json    # RSVP & Wishes data
│   └── photos.json              # Guest photo metadata
└── public/                      # Static assets
\`\`\`

---

## User-Facing Features

### 1. Home Page (`/`)
- Introduction to the couple (Ayo & Kemi)
- Key wedding details (date, time, location)
- Countdown to December 20, 2025
- Quick links to RSVP and Gallery
- Bank details for gifts
- Dress code information

### 2. Gallery Page (`/gallery`)
- **Official Gallery**: Pre-wedding photos displayed by category
  - Pre-wedding (6 official photos)
  - Engagement (placeholder)
  - Church Wedding (placeholder)
  - Reception (placeholder)
- **Guest Upload Section**: 
  - Drag-and-drop file upload
  - Image URL input
  - Form submission with guest name, email, and event category
  - Admin approval workflow before displaying

### 3. Story Page (`/story`)
- Peter's biography and photo
- Elizabeth's biography and photo
- Engagement story and photos
- Timeline of relationship

### 4. Details Page (`/details`)
- Dress codes with color swatches
- Bank account information
- Contact details
- RSVP and Wishes forms
- Map/Location information

### 5. Contact Page (`/contact`)
- Peter's phone: 08167788117
- Elizabeth's phone: 09151553758
- Email: ayopet4real@gmail.com
- Contact form
- Social media links (if applicable)

### 6. RSVP Page (`/rsvp`)
- Guest information form
- Attendance confirmation
- Guest count selection
- Optional message field
- Email confirmation sent to admin
- Data stored in `submissions-data.json`

### 7. Wishes Page (`/wishes`)
- Prayer/wishes submission form
- Guest name and message
- Public display on website
- Email sent to admin
- Data stored in `submissions-data.json`

### 8. Privacy Page (`/privacy`)
- Data collection policies
- Photo usage rights
- Security practices
- Contact for privacy concerns

### 9. Terms Page (`/terms`)
- Terms of service
- Photo submission terms
- Liability disclaimers
- Modifications clause

---

## Admin Features

### Admin Login (`/administrator/login`)
- Email-based authentication
- OTP verification via email
- Forgot password functionality
- Session management (60-minute timeout)
- **Credentials**: Use ADMIN_EMAIL and ADMIN_PASSWORD environment variables

### Admin Dashboard (`/administrator`)
- **Real-time Metrics**:
  - Total RSVPs received
  - Attendance breakdown (Yes/No/Undecided)
  - Total confirmed guests
  - Total wishes received
  - RSVP progress towards 250 guests

- **Recent Submissions**:
  - Latest RSVP entries with guest details
  - Latest wishes and prayers
  - Submission timestamps
  - Guest contact information

- **System Status**:
  - Live/Auto-refresh indicator
  - Manual refresh button
  - Pause/Resume auto-refresh
  - Session management
  - Last refresh timestamp

### Analytics Dashboard (`/administrator/analytics`)
- Page view tracking
- Visitor statistics
- RSVP statistics and trends
- Photo upload metrics
- Engagement tracking
- Charts and graphs (Recharts integration)

### Photo Management (`/api/admin/photos`)
- View all submitted photos (approved and pending)
- Approve guest uploads
- Reject inappropriate uploads
- Bulk operations support
- Admin-only access via auth token

---

## Data Storage

### Development Storage (JSON Files)
Photos, RSVPs, and wishes are stored locally in the `data/` directory:

\`\`\`
data/
├── photos.json          # Guest-uploaded photo metadata
├── submissions-data.json # RSVP and wishes submissions
└── [auto-created]
\`\`\`

### Production Storage (Recommended)
For production, use **Vercel Blob** for image files:
- Images uploaded by users are stored with blob URLs
- Metadata is stored in Vercel KV or database
- See [Deployment](#deployment--environment-variables) section

### Data Structure

**photos.json** (Photo Metadata):
\`\`\`json
[
  {
    "id": "1630703400000",
    "url": "https://example-blob-url.jpg",
    "uploaderName": "John Doe",
    "uploaderEmail": "john@example.com",
    "event": "pre-wedding",
    "uploadedAt": "2025-10-30T10:30:00.000Z",
    "approved": false
  }
]
\`\`\`

**submissions-data.json** (RSVPs & Wishes):
\`\`\`json
{
  "rsvps": [
    {
      "id": "1630703400000",
      "type": "rsvp",
      "name": "Guest Name",
      "email": "guest@example.com",
      "guests": 2,
      "attending": "yes",
      "message": "Looking forward to it!",
      "timestamp": "2025-10-30T10:30:00.000Z"
    }
  ],
  "wishes": [
    {
      "id": "1630703400001",
      "type": "wish",
      "name": "Well-wisher",
      "message": "Wishing you a beautiful life together!",
      "timestamp": "2025-10-30T10:35:00.000Z"
    }
  ],
  "stats": {
    "totalRSVPs": 45,
    "attendingYes": 38,
    "attendingNo": 7,
    "totalGuests": 92,
    "totalWishes": 23
  }
}
\`\`\`

---

## API Endpoints

### Public Endpoints

#### `POST /api/send-rsvp`
Submit an RSVP response
\`\`\`
Body: {
  "name": "Guest Name",
  "email": "guest@example.com",
  "guests": 2,
  "attending": "yes" | "no",
  "message": "Optional message"
}
Response: { success: true, message: "..." }
\`\`\`

#### `POST /api/send-wishes`
Submit a wish/prayer
\`\`\`
Body: {
  "name": "Well-wisher",
  "message": "Wish message"
}
Response: { success: true, message: "..." }
\`\`\`

#### `POST /api/photos/upload`
Upload a guest photo (URL only)
\`\`\`
Body: {
  "url": "https://image-url.jpg",
  "uploaderName": "Guest Name",
  "uploaderEmail": "guest@example.com",
  "event": "pre-wedding" | "engagement" | "church-wedding" | "reception"
}
Response: { success: true, photo: {...}, message: "Photo uploaded successfully and is pending approval" }
\`\`\`

#### `GET /api/photos/upload`
Retrieve approved photos
\`\`\`
Query: None
Response: { photos: [...] }
\`\`\`

### Admin Endpoints (Requires Authentication)

#### `GET /api/admin/submissions`
Fetch all RSVPs and wishes
\`\`\`
Header: Authorization: Bearer {ADMIN_SECRET_KEY}
Response: {
  rsvps: [...],
  wishes: [...],
  stats: {...}
}
\`\`\`

#### `GET /api/admin/photos`
Fetch all photos (approved and pending)
\`\`\`
Header: Authorization: Bearer {ADMIN_SECRET_KEY}
Response: { photos: [...] }
\`\`\`

#### `PUT /api/admin/photos/:id`
Approve or reject a photo
\`\`\`
Header: Authorization: Bearer {ADMIN_SECRET_KEY}
Body: { "approved": true | false }
Response: { success: true, message: "..." }
\`\`\`

#### `POST /api/admin/login`
Request OTP for admin login
\`\`\`
Body: { "email": "admin@example.com" }
Response: { success: true, message: "OTP sent to email" }
\`\`\`

#### `POST /api/admin/verify-otp`
Verify OTP and get JWT token
\`\`\`
Body: { "email": "admin@example.com", "otp": "123456" }
Response: { 
  success: true, 
  token: "jwt-token", 
  message: "Login successful" 
}
\`\`\`

---

## Authentication & Security

### Admin Authentication Flow
1. Admin enters email on login page → `/administrator/login`
2. System sends OTP via email
3. Admin enters OTP → API verifies via `/api/admin/verify-otp`
4. JWT token issued (valid for 1 hour)
5. Token stored in `sessionStorage`
6. Token included in all admin API requests via `Authorization: Bearer {token}` header

### Token Verification
- JWT verified using `JWT_SECRET` environment variable
- OTP valid for 10 minutes
- Admin session timeout: 60 minutes (configurable)
- SessionManager component handles automatic logout

### Security Best Practices
- All admin endpoints require JWT token verification
- Passwords hashed and stored as environment variables (not in database)
- OTP sent via email for verification
- CORS headers configured
- Input validation on all forms
- SQL injection prevention (no database used)

---

## Image Upload & Storage

### Guest Photo Upload Flow
1. **Frontend** (`/gallery` - photo-upload-form component):
   - User enters name, email, selects event category
   - Two upload methods:
     - **Drag-and-drop**: Files dropped trigger file input
     - **Image URL**: Direct URL paste in input field
   
2. **File Processing**:
   - For drag-drop: File converted to blob, uploaded to Vercel Blob
   - For URL: URL validated and stored directly
   - Metadata extracted (filename, uploader info, timestamp)

3. **Backend Processing** (`POST /api/photos/upload`):
   - Receives file or URL + metadata
   - Stores blob URL or external URL
   - Creates metadata entry in `photos.json`
   - Sets `approved: false` (pending admin review)
   - Sends confirmation email to uploader

4. **Admin Approval** (`/administrator`):
   - Admin views pending photos in dashboard
   - Can approve or reject via `/api/admin/photos` endpoint
   - Only approved photos visible to guests

5. **Public Display** (`/gallery`):
   - Guest upload section shows only approved photos
   - Photos fetched via `GET /api/photos/upload`
   - Displayed in responsive grid

### Storage Locations

**Development**:
- Photo metadata: `/data/photos.json`
- Actual image files: Stored with blob URLs (external)

**Production (Vercel Blob)**:
- Create Vercel Blob integration in project settings
- Images uploaded directly to Vercel Blob storage
- URLs returned and stored in metadata
- Automatic CDN distribution

### Environment Variables for Image Upload
\`\`\`
NEXT_PUBLIC_BASE_URL=http://localhost:3000  # or production URL
VERCEL_BLOB_TOKEN=your-blob-token           # For production
\`\`\`

---

## Deployment & Environment Variables

### Required Environment Variables

\`\`\`env
# Admin Authentication
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=secure-password
ADMIN_SECRET_KEY=your-secret-key-for-api
JWT_SECRET=your-jwt-secret-key

# Email Configuration (SMTP)
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
NEXTAUTH_SECRET=your-nextauth-secret

# Base URL
NEXT_PUBLIC_BASE_URL=https://your-domain.com  # Production URL
NEXT_PUBLIC_INVITATION_CODE=optional-code
INVITATION_CODE=same-as-above

# Optional: Multi-language
NEXT_PUBLIC_DEFAULT_LANGUAGE=en
\`\`\`

### Setup Steps

1. **Clone Repository**
   \`\`\`bash
   git clone your-repo-url
   cd wedding-website
   \`\`\`

2. **Install Dependencies**
   \`\`\`bash
   npm install
   \`\`\`

3. **Configure Environment Variables**
   - Copy `.env.example` to `.env.local`
   - Fill in all required variables
   - For Vercel deployment, add via project settings

4. **Run Development Server**
   \`\`\`bash
   npm run dev
   \`\`\`
   Visit `http://localhost:3000`

5. **Deploy to Vercel**
   \`\`\`bash
   npm run build
   git push  # Automatic deployment via GitHub integration
   \`\`\`
   Or use Vercel CLI:
   \`\`\`bash
   vercel deploy
   \`\`\`

### Data Backup
- Regular backups of `data/` directory recommended
- Or use Vercel KV for production persistence
- Set up automated backups in deployment pipeline

---

## Frontend Features

### Multi-language Support
- Supported languages: English, Spanish, French, Yoruba
- Language switcher in header
- Preference saved to localStorage
- Automatic translation of UI elements

### Responsive Design
- Mobile-first approach
- Breakpoints: sm (640px), md (768px), lg (1024px)
- Tailwind CSS for styling
- Accessible UI components

### Performance Optimizations
- Image optimization with Next.js Image component
- CSS minification
- Code splitting
- Automatic static generation where applicable
- CDN for assets

---

## Troubleshooting

### Common Issues

**Photos not uploading**
- Check: File size < 5MB
- Check: Valid image format (JPG, PNG, GIF)
- Check: User entered all required fields
- Check: Admin approved the photo

**Admin login not working**
- Check: Email matches ADMIN_EMAIL environment variable
- Check: OTP was received in email
- Check: OTP not expired (10 minutes)
- Check: JWT_SECRET is set in environment

**RSVP/Wishes not saving**
- Check: Email service configured correctly
- Check: ADMIN_SECRET_KEY is set
- Check: Network connection active
- Check: `submissions-data.json` has write permissions

**Images not displaying**
- Check: Blob URLs are still active
- Check: CORS headers configured
- Check: Image format supported by browser
- Check: Metadata has `approved: true`

---

## Summary

This comprehensive system provides a complete wedding website with:
- Public guest pages (Gallery, Story, Details, Contact)
- Guest submission system (RSVP, Wishes, Photos)
- Secure admin dashboard (Authentication, Analytics, Moderation)
- Real-time data tracking and updates
- Multi-language support
- Responsive mobile design

All data is securely stored and admin functions are protected by authentication tokens.
\`\`\`

Now I'll create the admin infrastructure setup file:

# Email Setup Guide for Wedding Website

## Environment Variables Required

Add these environment variables to your Vercel project or `.env.local` file:

\`\`\`env
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
\`\`\`

## Gmail Setup Instructions

1. **Enable 2-Factor Authentication** on your Gmail account
2. **Generate App Password**:
   - Go to Google Account settings
   - Security → 2-Step Verification → App passwords
   - Generate a new app password for "Mail"
   - Use this app password (not your regular password) for `EMAIL_PASS`

## Alternative Email Services

If not using Gmail, update the service in the API routes:

\`\`\`typescript
const transporter = nodemailer.createTransporter({
  service: 'outlook', // or 'yahoo', 'hotmail', etc.
  auth: {
    user: process.env.EMAIL_USER,
    pass: process.env.EMAIL_PASS,
  },
})
\`\`\`

## Testing

1. Add the environment variables
2. Submit a test RSVP or wish
3. Check your email for the formatted submission

## Email Format

- **RSVP emails** include: name, email, guest count, attendance status, and optional message
- **Wishes emails** include: sender name and their message/prayer
- Both emails are formatted with clean HTML styling matching your website design

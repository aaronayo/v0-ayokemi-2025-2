# Security Improvements Summary

This document outlines all the security enhancements implemented in the AYOKEMI2025 wedding website.

## Overview

The following security measures have been implemented to protect the application from common vulnerabilities and abuse:

1. **JWT-based Authentication** - Secure token-based authentication for admin access
2. **Rate Limiting** - Protection against spam and abuse on form submissions
3. **Input Validation** - Comprehensive validation and sanitization of user inputs
4. **Session Management** - Automatic session timeout and token verification

---

## 1. JWT Authentication

### Implementation

**Files Modified:**
- `lib/auth-utils.ts` - JWT token generation and verification utilities
- `app/administrator/login/page.tsx` - Updated to store JWT tokens
- `src/pages/api/admin/verify-otp.tsx` - Returns JWT token instead of secret key
- `src/pages/api/admin/submissions.tsx` - Verifies JWT tokens for API access
- `app/administrator/page.tsx` - Uses JWT token for authenticated requests

### How It Works

1. **Login Flow:**
   - User enters credentials → OTP sent to email
   - User enters OTP → Server verifies and generates JWT token
   - JWT token stored in `sessionStorage` as `adminAuthToken`

2. **Token Structure:**
   - Algorithm: HS256
   - Expiration: 1 hour
   - Payload: `{ email: string }`
   - Secret: `ADMIN_SECRET_KEY` environment variable

3. **Token Verification:**
   - All admin API requests require `Authorization: Bearer <token>` header
   - Server verifies token signature and expiration
   - Invalid/expired tokens return 401 Unauthorized

### Security Benefits

- **No Secret Key Exposure:** Admin secret key never sent to client
- **Time-Limited Access:** Tokens expire after 1 hour
- **Tamper-Proof:** JWT signature prevents token modification
- **Stateless:** No server-side session storage required

---

## 2. Rate Limiting

### Implementation

**Files Created/Modified:**
- `lib/rate-limit-utils.ts` - Rate limiting logic (server & client)
- `components/rate-limit-modal.tsx` - User-friendly rate limit notification
- `src/pages/rsvp.tsx` - Added rate limiting to RSVP form
- `src/pages/wishes.tsx` - Added rate limiting to wishes form
- `src/pages/api/send-rsvp.tsx` - Server-side rate limit enforcement
- `src/pages/api/send-wishes.tsx` - Server-side rate limit enforcement

### Rate Limit Configuration

| Endpoint | Limit | Window | Identifier |
|----------|-------|--------|------------|
| RSVP Submissions | 3 | 24 hours | IP + Email |
| Wish Submissions | 3 | 24 hours | IP + Name |
| Admin Login | 5 attempts | 15 minutes | Email |
| Admin OTP Verify | 10 attempts | 15 minutes | Email |

### How It Works

1. **Client-Side Check (First Line of Defense):**
   - Uses `localStorage` to track submission count
   - Prevents unnecessary API calls
   - Shows user-friendly modal with countdown

2. **Server-Side Enforcement (Final Authority):**
   - Uses in-memory Map to track submissions
   - Identifier: `${clientIP}-${email/name}`
   - Returns 429 status code when limit exceeded

3. **User Experience:**
   - Clear error message explaining the limit
   - Countdown timer showing when they can submit again
   - Prevents accidental spam submissions

### Security Benefits

- **Spam Prevention:** Limits automated bot submissions
- **Resource Protection:** Prevents email service abuse
- **Fair Usage:** Ensures legitimate users can access the service
- **DDoS Mitigation:** Reduces impact of malicious traffic

---

## 3. Input Validation & Sanitization

### Implementation

**All API Routes Include:**

1. **Email Validation:**
   \`\`\`typescript
   const validateEmail = (email: string): boolean => {
     const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
     return emailRegex.test(email) && email.length <= 254
   }
   \`\`\`

2. **Input Length Validation:**
   \`\`\`typescript
   const validateInput = (input: string, maxLength: number): boolean => {
     return typeof input === "string" && 
            input.trim().length > 0 && 
            input.length <= maxLength
   }
   \`\`\`

3. **HTML Sanitization:**
   \`\`\`typescript
   const sanitizeInput = (input: string): string => {
     return input.replace(/[<>]/g, "").trim()
   }
   \`\`\`

4. **OTP Validation:**
   \`\`\`typescript
   const validateOTP = (otp: string): boolean => {
     return /^\d{6}$/.test(otp)
   }
   \`\`\`

### Protected Fields

| Field | Max Length | Validation |
|-------|-----------|------------|
| Name | 100 chars | Non-empty, sanitized |
| Email | 254 chars | Valid email format |
| Password | 100 chars | Non-empty |
| Message | 1000 chars | Sanitized |
| OTP | 6 chars | Numeric only |
| Invitation Code | 20 chars | Exact match |

### Security Benefits

- **XSS Prevention:** Removes HTML tags from user input
- **SQL Injection Prevention:** Validates data types and formats
- **Buffer Overflow Prevention:** Enforces maximum lengths
- **Data Integrity:** Ensures only valid data is processed

---

## 4. Session Management

### Implementation

**Files:**
- `components/session-manager.tsx` - Automatic session timeout component
- `app/administrator/page.tsx` - Integrated session management

### Features

1. **Automatic Timeout:**
   - Default: 60 minutes of inactivity
   - Tracks user activity (mouse, keyboard, touch)
   - Warns user before timeout
   - Automatically logs out on timeout

2. **Token Verification:**
   - Checks for valid JWT token on page load
   - Redirects to login if token missing/invalid
   - Clears session data on logout

3. **Session Storage:**
   - `adminAuthenticated` - Boolean flag
   - `adminEmail` - User email
   - `adminLoginTime` - Login timestamp
   - `adminToken` - Random session identifier
   - `adminAuthToken` - JWT token

### Security Benefits

- **Prevents Unauthorized Access:** Expired sessions can't access admin panel
- **Reduces Attack Window:** Limited time for session hijacking
- **Activity Tracking:** Monitors user engagement
- **Clean Logout:** Properly clears all session data

---

## 5. Additional Security Measures

### Environment Variables

All sensitive data stored in environment variables:
- `ADMIN_EMAIL` - Admin email address
- `ADMIN_PASSWORD` - Admin password
- `ADMIN_SECRET_KEY` - JWT signing secret
- `EMAIL_USER` - Email service username
- `EMAIL_PASS` - Email service password
- `INVITATION_CODE` - Guest invitation code

### HTTPS Enforcement

- All production traffic should use HTTPS
- Prevents man-in-the-middle attacks
- Protects JWT tokens in transit

### CORS Protection

- API routes only accept requests from same origin
- Prevents cross-site request forgery

### Error Handling

- Generic error messages to users
- Detailed errors logged server-side only
- Prevents information leakage

---

## Testing Checklist

### Authentication
- [ ] Login with correct credentials works
- [ ] Login with incorrect credentials fails
- [ ] OTP expires after 5 minutes
- [ ] JWT token expires after 1 hour
- [ ] Invalid JWT token returns 401
- [ ] Session timeout works after 60 minutes

### Rate Limiting
- [ ] RSVP form blocks after 3 submissions
- [ ] Wishes form blocks after 3 submissions
- [ ] Rate limit resets after 24 hours
- [ ] Client-side check prevents API calls
- [ ] Server-side check enforces limit

### Input Validation
- [ ] Invalid email addresses rejected
- [ ] Overly long inputs truncated
- [ ] HTML tags removed from inputs
- [ ] Invalid OTP format rejected
- [ ] Wrong invitation code rejected

### Session Management
- [ ] Inactive session times out
- [ ] User activity resets timeout
- [ ] Logout clears all session data
- [ ] Expired token redirects to login

---

## Deployment Notes

### Required Environment Variables

Ensure these are set in production:

\`\`\`bash
ADMIN_EMAIL=your-admin@email.com
ADMIN_PASSWORD=your-secure-password
ADMIN_SECRET_KEY=your-jwt-secret-key-min-32-chars
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-specific-password
INVITATION_CODE=AYOKEMI25
NEXT_PUBLIC_INVITATION_CODE=AYOKEMI25
\`\`\`

### Security Best Practices

1. **Use Strong Secrets:**
   - `ADMIN_SECRET_KEY` should be at least 32 characters
   - Use random, cryptographically secure strings
   - Never commit secrets to version control

2. **Enable HTTPS:**
   - Use SSL/TLS certificates
   - Redirect HTTP to HTTPS
   - Enable HSTS headers

3. **Monitor Logs:**
   - Watch for failed login attempts
   - Track rate limit violations
   - Alert on suspicious activity

4. **Regular Updates:**
   - Keep dependencies updated
   - Apply security patches promptly
   - Review security advisories

---

## Future Enhancements

### Recommended Improvements

1. **Two-Factor Authentication:**
   - Add TOTP-based 2FA
   - Backup codes for recovery

2. **Advanced Rate Limiting:**
   - Redis-based distributed rate limiting
   - IP reputation scoring
   - CAPTCHA for suspicious activity

3. **Audit Logging:**
   - Log all admin actions
   - Track data access patterns
   - Generate security reports

4. **Database Encryption:**
   - Encrypt sensitive data at rest
   - Use encrypted connections
   - Implement field-level encryption

5. **Content Security Policy:**
   - Add CSP headers
   - Prevent XSS attacks
   - Restrict resource loading

---

## Support

For security concerns or questions, contact the development team.

**Last Updated:** January 2025
**Version:** 1.0.0

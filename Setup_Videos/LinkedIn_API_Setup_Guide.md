# LinkedIn Official API — Complete Setup Guide

**Date:** 2026-03-20
**Author:** Shahzain Ali + Claude Opus 4.6
**Status:** FULLY WORKING — Post, Comment, Like on LinkedIn via Official API

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Token Type — Quick Summary](#2-token-type--quick-summary)
3. [LinkedIn Page Create Karna](#3-linkedin-page-create-karna)
4. [Developer App Create Karna](#4-developer-app-create-karna)
5. [App Permissions (Products) Enable Karna](#5-app-permissions-products-enable-karna)
6. [Client Credentials + Redirect URLs](#6-client-credentials--redirect-urls)
7. [Access Token Generate Karna (OAuth 2.0)](#7-access-token-generate-karna-oauth-20)
8. [Person URN Find Karna](#8-person-urn-find-karna)
9. [Organization URN Find Karna](#9-organization-urn-find-karna)
10. [LinkedIn Pe Post Karna (API Test)](#10-linkedin-pe-post-karna-api-test)
11. [Token Renewal — Kab Aur Kaise](#11-token-renewal--kab-aur-kaise)
12. [.env Configuration](#12-env-configuration)
13. [What You Can Post — Content Types](#13-what-you-can-post--content-types)
14. [API Endpoints Quick Reference](#14-api-endpoints-quick-reference)
15. [Troubleshooting](#15-troubleshooting)
16. [Checklist — Setup Complete?](#16-checklist--setup-complete)

---

## 1. Prerequisites

Ye sab **pehle se ready** hona chahiye:

| # | Requirement | Notes |
|---|------------|-------|
| 1 | LinkedIn personal account | Login ke liye (already hoga) |
| 2 | Desktop browser | Chrome/Edge recommended |

> **LinkedIn Company Page** zaroori hai Developer App banane ke liye — lekin **pehle se banana zaroori nahi.** App creation form mein **"+ Create a new LinkedIn Page"** ka option hota hai, wahi pe bana sakte ho (Step 4 mein dikhayenge).
>
> **Posting ke liye Page zaroori nahi** — `w_member_social` scope se aap **personal profile** pe post kar sakte ho. Page sirf app creation ke liye chahiye.

**Is guide mein hum ye karenge:**

| Item | Guide Mein Step |
|------|----------------|
| Developer App | Step 4 |
| Permissions enable | Step 5 |
| Client Credentials + Redirect URLs | Step 6 |
| Access Token (60 days) | Step 7 |
| Person URN find karna | Step 8 |
| Organization URN find karna (optional) | Step 9 |
| LinkedIn pe post karna | Step 10 |

**Cost:** Sab kuch **100% free** hai. Koi payment nahi lagti.

---

## 2. Token Type — Quick Summary

| Token Type | Expiry | Kab Use Hota Hai |
|------------|--------|------------------|
| **Access Token** | **60 days** | LinkedIn pe post, comment, like |

**Key Points:**
- LinkedIn mein sirf **ek token type** hai — Access Token (60 days)
- Never-expiring token ka option **nahi** hai LinkedIn mein
- Har 50 din mein renew karna padta hai (10 din pehle)
- Token generate karna easy hai — 2 minute ka kaam hai

---

## 3. LinkedIn Page Create Karna

> **Agar sirf personal profile pe post karna hai toh Page banana zaroori nahi — Step 4 pe jao.**
> Business ke liye Page recommended hai.

**Time:** 5 minutes

1. Browser mein jao: **https://www.linkedin.com/company/setup/new**
   - Ya LinkedIn open karo → Top bar mein **"For Business"** (ya **"+"** icon) → **"Create a Company Page"**
2. Page type select karo:

| Type | Best For |
|------|----------|
| **Small business** | Startup ya chhoti company |
| Medium to large business | Badi company |
| Showcase page | Sub-brand |
| Educational institution | School/university |

3. Page details fill karo:

| Field | Example | Notes |
|-------|---------|-------|
| **Name** | My Tech Company | Company ka naam |
| **LinkedIn public URL** | my-tech-company | Auto-generate, customize kar sakte ho |
| **Website** | https://mytechcompany.com | Optional |
| **Industry** | Technology, Information and Internet | Dropdown se select karo |
| **Organization size** | 2-10 employees | Ya "0-1" agar solo ho |
| **Organization type** | Sole Proprietorship | Solo founder ke liye |
| **Tagline** | AI-Powered Automation Solutions | Short description |

4. Checkbox tick karo: "I verify that I am an authorized representative..."
5. **"Create page"** click karo

**Result:** LinkedIn Page ban gaya ✅

---

## 4. Developer App Create Karna

**Time:** 5 minutes

1. LinkedIn Developer Portal kholein: **developer.linkedin.com**
2. **"Create app"** button pe click karo (top right)
3. App details fill karo:

| Field | Value | Notes |
|-------|-------|-------|
| **App name** | My Tech Company App | Descriptive naam |
| **LinkedIn Page** | My Tech Company | Dropdown se select karo — agar page nahi hai toh **"+ Create a new LinkedIn Page"** pe click karke wahi bana lo |
| **Privacy policy URL** | https://mytechcompany.com/privacy | Optional for development |
| **App logo** | Upload logo | Required — 100x100 minimum |

4. **"Create app"** click karo

**Result:** Developer App ban gayi ✅

---

## 5. App Permissions (Products) Enable Karna

1. App settings mein **"Products"** tab pe jao
2. In products ko **Request access** karo:

| Product | Purpose | Approval |
|---------|---------|----------|
| **Share on LinkedIn** | Posts create karna | Instant approval |
| **Sign In with LinkedIn using OpenID Connect** | Profile info access | Instant approval |
| Community Management API | Comments, likes | May need review |

3. Har product ke Terms accept karo aur **"Request access"** click karo
4. Wait karo — kuch instantly approve, kuch mein 1-2 din lag sakte hain

### Verify Permissions:

**"Auth"** tab mein check karo ke ye scopes available hain:

| Scope | Purpose | Required? |
|-------|---------|-----------|
| `openid` | Sign in with LinkedIn | ✅ Yes |
| `profile` | Basic profile info | ✅ Yes |
| `email` | Email address | Optional |
| `w_member_social` | **Create posts on personal profile** | ✅ MANDATORY |

> ⚠️ **`w_member_social`** sabse important hai — iske bina post nahi hoga!

---

## 6. Client Credentials + Redirect URLs

### Credentials Note Karo:

**"Auth"** tab mein:

| Credential | Where to Find |
|------------|--------------|
| **Client ID** | Auth tab → Client ID |
| **Client Secret** | Auth tab → Click eye icon |

> ⚠️ **Client Secret kabhi public mat karo!**

### Redirect URLs Configure Karo:

**"Auth"** tab → **"Authorized redirect URLs for your app"** mein add karo:

```
http://localhost:8080/callback
https://www.linkedin.com/developers/tools/oauth/redirect
```

> **"Update"** ya **"Save"** button click karna mat bhoolo — warna redirect URLs save nahi honge!

---

## 7. Access Token Generate Karna (OAuth 2.0)

### Method A: LinkedIn Developer Tools (Easiest — Recommended)

**Time:** 2 minutes

1. Jao: **https://www.linkedin.com/developers/tools/oauth**
2. Apni app select karo
3. **Scopes** mein select karo:
   - ✅ `openid`
   - ✅ `profile`
   - ✅ `email`
   - ✅ `w_member_social`
4. **"Request access token"** click karo
5. LinkedIn login karo aur **"Allow"** click karo
6. **Access Token** copy karo

> ⚠️ **Token 60 days mein expire hota hai!** Calendar mein reminder lagao.

### Method B: Manual OAuth Flow (For Production)

**Step 1: Authorization Code Get Karo**

Browser mein ye URL open karo (apni values replace karo):

```
https://www.linkedin.com/oauth/v2/authorization?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=http://localhost:8080/callback&scope=openid%20profile%20email%20w_member_social
```

Allow karne ke baad redirect hoga:
```
http://localhost:8080/callback?code=AUTHORIZATION_CODE_HERE&state=...
```

URL mein se `code=` ke baad aur `&` se pehle wala part copy karo — ye tumhara **Authorization Code** hai.

**Step 2: Code ko Token mein Exchange Karo**

```bash
curl -X POST "https://www.linkedin.com/oauth/v2/accessToken" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=authorization_code" \
  -d "code=AUTHORIZATION_CODE_HERE" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "redirect_uri=http://localhost:8080/callback"
```

Response:
```json
{
    "access_token": "AQV...",
    "expires_in": 5184000
}
```

`5184000` seconds = **60 days**

---

## 8. Person URN Find Karna

> Person URN tumhara personal LinkedIn ID hai. **Personal profile pe post karne ke liye ye chahiye.**

**Step 7 se mila hua Access Token** yahan use karo — `YOUR_ACCESS_TOKEN` ki jagah paste karo:

```bash
curl -s "https://api.linkedin.com/v2/userinfo" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

Response:
```json
{
    "sub": "abc123def456",
    "name": "Shahzain Ali",
    "email": "your@email.com"
}
```

**Person URN:** `urn:li:person:abc123def456`

> `sub` field tumhara Person URN hai.

---

## 9. Organization URN Find Karna

> Organization URN tumhara Company Page ID hai. **Page pe post karne ke liye ye chahiye** (optional).

**Method 1 — Page Admin URL se (Easiest):**
1. Apni LinkedIn Company Page open karo browser mein
2. URL bar mein dekho — kuch aisa hoga: `linkedin.com/company/112495928/`
3. Number copy karo — ye tumhara Organization ID hai

**Method 2 — Page Source se:**
1. Company Page pe `Ctrl+U` press karo (View Page Source)
2. `Ctrl+F` se search karo: `urn:li:organization:`
3. Number copy karo

**Example:** `urn:li:organization:112495928`

---

## 10. LinkedIn Pe Post Karna (API Test)

> **2 values replace karo** command mein: `YOUR_ACCESS_TOKEN` (Step 7 se) aur `YOUR_PERSON_ID` (Step 8 se)

### Quick Test via curl:

```bash
curl -X POST "https://api.linkedin.com/v2/ugcPosts" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "author": "urn:li:person:YOUR_PERSON_ID",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
        "com.linkedin.ugc.ShareContent": {
            "shareCommentary": {
                "text": "Hello from LinkedIn API! 🚀 Test post from FTE AI Employee."
            },
            "shareMediaCategory": "NONE"
        }
    },
    "visibility": {
        "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"
    }
}'
```

### Expected Response:
```json
{
  "id": "urn:li:share:7000000000000000000"
}
```

**LinkedIn profile pe jao — post dikhni chahiye ✅**

### Test via Dashboard:

1. Dashboard start karo: `uv run python -m src.main dashboard`
2. **Social Media** tab pe jao → LinkedIn section
3. Content likho aur **Post** click karo

---

## 11. Token Renewal — Kab Aur Kaise

### LinkedIn Access Token

| Question | Answer |
|----------|--------|
| Expire hota hai? | **Haan — 60 days baad** |
| Renew karna padta hai? | **Haan — har 50 din mein** (10 din pehle) |
| Never-expiring option hai? | **Nahi** — LinkedIn mein ye option nahi |

### Renewal Process (har 50 din):

1. Jao: **https://www.linkedin.com/developers/tools/oauth**
2. Apni app select karo
3. Same scopes select karo (openid, profile, email, w_member_social)
4. **"Request access token"** click karo
5. Naya token `.env` mein update karo

### Token Expiry Check:

```bash
curl -s "https://api.linkedin.com/v2/userinfo" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

- Response mein name aaye → Token valid hai ✅
- `401 Unauthorized` → Token expire ho gaya — renew karo

> **Tip:** Phone mein calendar reminder lagao — "LinkedIn Token Renew" har 50 din pe.

---

## 12. .env Configuration

Setup complete hone ke baad `.env` file mein ye values add karo:

```env
# ===== LINKEDIN =====
LINKEDIN_CLIENT_ID=your_client_id
LINKEDIN_CLIENT_SECRET=your_client_secret
LINKEDIN_ACCESS_TOKEN=your_60_day_access_token
LINKEDIN_PERSON_URN=urn:li:person:your_person_id
LINKEDIN_ORGANIZATION_URN=urn:li:organization:your_org_id
```

| Variable | Value Kahan Se Milegi | Required? |
|----------|----------------------|-----------|
| `LINKEDIN_CLIENT_ID` | Developer Portal → Auth tab | ✅ Yes |
| `LINKEDIN_CLIENT_SECRET` | Developer Portal → Auth tab (eye icon) | ✅ Yes |
| `LINKEDIN_ACCESS_TOKEN` | Step 7 (OAuth token) | ✅ Yes |
| `LINKEDIN_PERSON_URN` | Step 8 (API call) | ✅ Yes |
| `LINKEDIN_ORGANIZATION_URN` | Step 9 (Page source) | Optional |

> ⚠️ **`.env` file kabhi git mein push mat karo.** Already `.gitignore` mein honi chahiye.

---

## 13. What You Can Post — Content Types

| Content Type | How | Example |
|-------------|-----|---------|
| **Text Post** | `shareCommentary.text` | "New product launch! 🚀" |
| **Link Post** | `shareMediaCategory: ARTICLE` + URL | Share article with link preview |
| **Image Post** | Upload via `/v2/assets` + attach | Product photos |
| **Video Post** | Upload via `/v2/assets` + attach | Demo videos |

**LinkedIn Restrictions:**
- Maximum post text: 3,000 characters
- Images: JPEG, PNG, GIF (max 10MB)
- Videos: MP4 (max 200MB, max 10 minutes)

**Example — Text Post:**
```json
{
    "author": "urn:li:person:YOUR_ID",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
        "com.linkedin.ugc.ShareContent": {
            "shareCommentary": {
                "text": "Excited to share our new AI tool! #tech #ai"
            },
            "shareMediaCategory": "NONE"
        }
    },
    "visibility": {
        "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"
    }
}
```

---

## 14. API Endpoints Quick Reference

| Action | Method | Endpoint | Auth |
|--------|--------|----------|------|
| Get Profile | GET | `/v2/userinfo` | Bearer Token |
| Create Text Post | POST | `/v2/ugcPosts` | Bearer Token |
| Create Article Post | POST | `/v2/ugcPosts` | Bearer Token |
| Get Posts | GET | `/v2/ugcPosts?q=authors&authors=List(URN)` | Bearer Token |
| Comment on Post | POST | `/v2/socialActions/{post-urn}/comments` | Bearer Token |
| Like a Post | POST | `/v2/socialActions/{post-urn}/likes` | Bearer Token |
| Upload Image | POST | `/v2/assets?action=registerUpload` | Bearer Token |

### Rate Limits

| Resource | Limit |
|----------|-------|
| API calls (general) | 100 requests per day per member |
| Post creation | 150 per day |
| Comments | 100 per day |

---

## 15. Troubleshooting

### Token Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `401 Unauthorized` | Token expire ho gaya | Step 11 follow karo — naya token generate karo |
| `invalid_token` | Token galat ya revoked | Dobara Step 7 follow karo |

### Permission Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `403 ACCESS_DENIED` | Organization URN use ki personal post mein | Person URN use karo: `urn:li:person:...` |
| `w_member_social` scope nahi | "Share on LinkedIn" product approved nahi | Developer Portal → Products → "Share on LinkedIn" request karo |
| `Insufficient permissions` | Token mein scope missing | Naya token generate karo with all scopes |

### Posting Errors

| Error | Cause | Solution |
|-------|-------|----------|
| Post nahi dikh rahi | `visibility` PUBLIC nahi hai | `MemberNetworkVisibility: PUBLIC` set karo |
| Post nahi dikh rahi | `lifecycleState` PUBLISHED nahi | `lifecycleState: PUBLISHED` set karo |
| Post 2-3 min late dikhi | LinkedIn delay | Normal hai — 2-3 min wait karo |

---

## 16. Checklist — Setup Complete?

### Prerequisites
- [ ] LinkedIn personal account ready
- [ ] Desktop browser available

### Accounts
- [ ] LinkedIn Company Page created (Step 3) — optional
- [ ] Developer App created (Step 4)

### Permissions
- [ ] "Share on LinkedIn" product enabled (Step 5)
- [ ] "Sign In with LinkedIn" product enabled (Step 5)
- [ ] `w_member_social` scope available
- [ ] Client ID noted (Step 6)
- [ ] Client Secret noted (Step 6)
- [ ] Redirect URLs configured (Step 6)

### Token + IDs
- [ ] Access Token generated (Step 7)
- [ ] Person URN found (Step 8)
- [ ] Organization URN found (Step 9) — optional
- [ ] Test post successful (Step 10)

### Configuration
- [ ] `.env` file updated with all values (Step 12)
- [ ] `.env` is in `.gitignore`
- [ ] Calendar reminder set for token renewal (every 50 days)

---

*Guide created for My Tech Company — AI Employee as a Service*
*Last updated: 2026-03-24*

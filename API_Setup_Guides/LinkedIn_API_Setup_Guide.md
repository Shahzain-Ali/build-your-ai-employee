# LinkedIn Official API — Complete Setup Guide

**Date:** 2026-04-11
**Author:** Shahzain Ali + Claude Opus 4.6
**Status:** FULLY WORKING — Post, Comment, Like on LinkedIn via Official API

> **Cost:** 100% free. No credit card, no payment, no hidden charges.

---

## Table of Contents

1. [Token Type — Quick Summary](#1-token-type--quick-summary)
2. [LinkedIn Page Create Karna](#2-linkedin-page-create-karna)
3. [Developer App Create Karna](#3-developer-app-create-karna)
4. [App Permissions (Products) Enable Karna](#4-app-permissions-products-enable-karna)
5. [Client Credentials + Redirect URLs](#5-client-credentials--redirect-urls)
6. [Access Token Generate Karna (OAuth 2.0)](#6-access-token-generate-karna-oauth-20)
7. [Person URN Find Karna](#7-person-urn-find-karna)
8. [Organization URN Find Karna](#8-organization-urn-find-karna)
9. [LinkedIn Pe Post Karna (API Test)](#9-linkedin-pe-post-karna-api-test)
10. [Token Renewal — Kab Aur Kaise](#10-token-renewal--kab-aur-kaise)
11. [.env Configuration](#11-env-configuration)
12. [What You Can Post — Content Types](#12-what-you-can-post--content-types)
13. [API Endpoints Quick Reference](#13-api-endpoints-quick-reference)
14. [Troubleshooting](#14-troubleshooting)
15. [Checklist — Setup Complete?](#15-checklist--setup-complete)

---

## 1. Token Type — Quick Summary

**Definition (English):** An access token is a credential that lets your app call LinkedIn's API on behalf of a user for a limited time.

**Roman Urdu:** Access token ek temporary password hota hai jo aapki app ko LinkedIn user ki taraf se action karne deta hai (post, comment, like).

| Token Type | Expiry | Use Case |
|------------|--------|----------|
| **Access Token** | **60 days** (5,184,000 seconds) | Post, comment, like on LinkedIn |

**Key Points:**
- LinkedIn issues only one token type for self-serve apps: Access Token (60 days).
- No never-expiring option is available for standard developer apps.
- Renew every 50 days (10 days before expiry) to avoid downtime.
- Token generation is quick — takes about 2 minutes.

---

## 2. LinkedIn Page Create Karna

**Time:** 5 minutes

> You need a LinkedIn Company Page to create a Developer App. If you already have one, skip to Step 3.

### Steps:

1. Open your browser and go to: **https://www.linkedin.com/company/setup/new**
   - Alternative: Open LinkedIn → click **"For Business"** (top-right grid icon) → **"Create a Company Page"**

2. Select the Page type:

| Type | Best For |
|------|----------|
| **Small business** | Startup or small company |
| Medium to large business | Larger company |
| Showcase page | Sub-brand |
| Educational institution | School / University |

3. Fill in the Page details:

| Field | Example | Notes |
|-------|---------|-------|
| **Name** | My Tech Company | Your company name |
| **LinkedIn public URL** | my-tech-company | Auto-generated, editable |
| **Website** | https://mytechcompany.com | Optional |
| **Industry** | Technology, Information and Internet | Pick from dropdown |
| **Organization size** | 2-10 employees | Or "0-1" for solo |
| **Organization type** | Sole Proprietorship | For solo founders |
| **Tagline** | Your company tagline here | Short description |

4. Tick the checkbox: *"I verify that I am an authorized representative..."*
5. Click **"Create page"**.

**Result:** Your LinkedIn Company Page is now live.

---

## 3. Developer App Create Karna

**Time:** 5 minutes

### Steps:

1. Open the LinkedIn Developer Portal: **https://developer.linkedin.com**
2. Click **"Create app"** (top-right corner).
3. Fill in the app details:

| Field | Value | Notes |
|-------|-------|-------|
| **App name** | My Tech Company App | Descriptive name |
| **LinkedIn Page** | My Tech Company | Select your Page from the dropdown (created in Step 2) |
| **Privacy policy URL** | https://mytechcompany.com/privacy | Optional for development |
| **App logo** | Upload logo | Required — minimum 100x100 pixels |

4. Accept the legal agreement.
5. Click **"Create app"**.

**Result:** Your Developer App is ready.

---

## 4. App Permissions (Products) Enable Karna

**Definition (English):** Products are feature bundles that unlock specific OAuth scopes (permissions) for your app.

**Roman Urdu:** Products woh feature packs hain jo aapki app ko specific LinkedIn permissions dete hain — jaise post karna ya profile dekhna.

### Steps:

1. In your app dashboard, click the **"Products"** tab (top navigation).
2. Find these two products and click **"Request access"** for each:

| Product | Scope Unlocked | Approval Time |
|---------|---------------|---------------|
| **Share on LinkedIn** | `w_member_social` | Instant (seconds) |
| **Sign In with LinkedIn using OpenID Connect** | `openid`, `profile`, `email` | Instant (seconds) |

3. Accept the Terms for each product.
4. Both products approve in seconds — no waiting, no manual review.

### Verify Permissions:

1. Stay in the **"Products"** tab.
2. Scroll to the **"Added products"** section.
3. Confirm both products show a green checkmark:
   - ✅ Share on LinkedIn
   - ✅ Sign In with LinkedIn using OpenID Connect

> **Note:** Scopes do not appear under the Auth tab. They become available automatically after the products are approved. You will select them during token generation in Step 6.

---

## 5. Client Credentials + Redirect URLs

### Note Your Credentials:

1. Click the **"Auth"** tab (top navigation).
2. Scroll to the **"Application credentials"** section.
3. Copy the following values:

| Credential | How to Find |
|------------|-------------|
| **Client ID** | Displayed directly — click the copy icon. |
| **Primary Client Secret** | Click the eye icon (👁) to reveal the secret, then copy it. |

> ⚠️ Never share your Client Secret publicly or commit it to Git.
>
> **Lost your Client Secret?** Click **"Generate a new Client Secret"** to create a fresh one.

### Configure Redirect URLs:

1. Stay in the **"Auth"** tab.
2. Scroll to **"Authorized redirect URLs for your app"**.
3. Click **"Add redirect URL"** and add these two URLs (one at a time):

```
http://localhost:8080/callback
https://www.linkedin.com/developers/tools/oauth/redirect
```

4. Click **"Update"** to save.

> ⚠️ If you skip the Update button, your redirect URLs will not be saved.

---

## 6. Access Token Generate Karna (OAuth 2.0)

**Definition (English):** OAuth 2.0 is an authorization framework that lets your app obtain limited access to a user's account without needing their password.

**Roman Urdu:** OAuth 2.0 ek secure tareeqa hai jis mein user sirf permission deta hai — password share kiye bina.

### Method A: LinkedIn Developer Tools (⭐ Recommended)

**Time:** 2 minutes

1. Open: **https://www.linkedin.com/developers/tools/oauth**
2. Select your app from the dropdown.
3. Under **"Scopes"**, tick all four:
   - ✅ `openid`
   - ✅ `profile`
   - ✅ `email`
   - ✅ `w_member_social`
4. Click **"Request access token"**.
5. A LinkedIn login popup opens. Log in and click **"Allow"**.
6. Copy the **Access Token** displayed on the screen.

> ⚠️ The token expires in 60 days. Set a calendar reminder for renewal.

### Method B: Manual OAuth Flow (For Production)

**Step 1: Get Authorization Code**

Open this URL in a browser (replace your values):

```
https://www.linkedin.com/oauth/v2/authorization?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=http://localhost:8080/callback&scope=openid%20profile%20email%20w_member_social
```

After clicking Allow, you will be redirected to:

```
http://localhost:8080/callback?code=AUTHORIZATION_CODE_HERE&state=...
```

Copy the value between `code=` and `&` — this is your **Authorization Code**.

> The authorization code is valid for **30 minutes only**. Exchange it for a token immediately.

**Step 2: Exchange Code for Token**

```bash
curl -X POST "https://www.linkedin.com/oauth/v2/accessToken" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=authorization_code" \
  -d "code=AUTHORIZATION_CODE_HERE" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "redirect_uri=http://localhost:8080/callback"
```

**Response:**

```json
{
    "access_token": "AQV...",
    "expires_in": 5184000
}
```

`5184000` seconds = **60 days**.

---

## 7. Person URN Find Karna

**Definition (English):** A Person URN (Uniform Resource Name) is LinkedIn's unique identifier for your personal profile.

**Roman Urdu:** Person URN aapki personal LinkedIn ID hai — personal profile pe post karne ke liye chahiye.

### Steps:

Run this curl command (replace `YOUR_ACCESS_TOKEN` with the token from Step 6):

```bash
curl -s "https://api.linkedin.com/v2/userinfo" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

**Response:**

```json
{
    "sub": "abc123def456",
    "name": "Shahzain Ali",
    "email": "your@email.com"
}
```

**Your Person URN:** `urn:li:person:abc123def456`

> The `sub` field is your Person ID. Prefix it with `urn:li:person:` to form the full URN.

---

## 8. Organization URN Find Karna

**Definition (English):** An Organization URN is LinkedIn's unique identifier for a Company Page.

**Roman Urdu:** Organization URN aapki Company Page ki unique ID hai — Page pe post karne ke liye chahiye.

### Method 1 — Page Admin URL (⭐ Recommended)

1. Open your LinkedIn Company Page in a browser.
2. Look at the URL bar — it will look like: `linkedin.com/company/112495928/`
3. Copy the number. This is your Organization ID.

### Method 2 — Page Source

1. On your Company Page, press `Ctrl+U` (View Page Source).
2. Press `Ctrl+F` and search: `urn:li:organization:`
3. Copy the number that appears.

**Example URN:** `urn:li:organization:112495928`

---

## 9. LinkedIn Pe Post Karna (API Test)

Replace two values in every command: `YOUR_ACCESS_TOKEN` (from Step 6) and the URN (from Step 7 or Step 8).

> All write requests must include the header `X-Restli-Protocol-Version: 2.0.0`.

### A. Post to Personal Profile (using Person URN)

```bash
curl -X POST "https://api.linkedin.com/v2/ugcPosts" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "X-Restli-Protocol-Version: 2.0.0" \
  -H "Content-Type: application/json" \
  -d '{
    "author": "urn:li:person:YOUR_PERSON_ID",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
        "com.linkedin.ugc.ShareContent": {
            "shareCommentary": {
                "text": "Hello from LinkedIn API! Test post from my AI Employee."
            },
            "shareMediaCategory": "NONE"
        }
    },
    "visibility": {
        "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"
    }
}'
```

### B. Post to Company Page (using Organization URN)

```bash
curl -X POST "https://api.linkedin.com/v2/ugcPosts" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "X-Restli-Protocol-Version: 2.0.0" \
  -H "Content-Type: application/json" \
  -d '{
    "author": "urn:li:organization:YOUR_ORG_ID",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
        "com.linkedin.ugc.ShareContent": {
            "shareCommentary": {
                "text": "Hello from LinkedIn API! Test post from our Company Page."
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

> **Tip (Roman Urdu):** Post karne ke baad LinkedIn pe jao — 2-3 minute mein post dikhni chahiye. Agar turant nahi dikhi toh ghabrao mat, LinkedIn ka feed refresh hone mein thoda time lagta hai.

---

## 10. Token Renewal — Kab Aur Kaise

### LinkedIn Access Token

| Question | Answer |
|----------|--------|
| Does it expire? | Yes — after 60 days. |
| Renewal frequency? | Every 50 days (10 days before expiry). |
| Never-expiring option? | No. Not available for self-serve apps. |

### Renewal Steps (every 50 days):

1. Open: **https://www.linkedin.com/developers/tools/oauth**
2. Select your app.
3. Tick the same scopes: `openid`, `profile`, `email`, `w_member_social`.
4. Click **"Request access token"**.
5. Update the new token in your `.env` file.

### Token Expiry Check:

```bash
curl -s "https://api.linkedin.com/v2/userinfo" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

- Name returned → Token is valid. ✅
- `401 Unauthorized` → Token expired. Renew it.

> **Tip (Roman Urdu):** Phone ke calendar mein reminder laga lo — "LinkedIn Token Renew" har 50 din pe. Ek chhota sa yaad dihani ghanton ka kaam bacha deti hai.

---

## 11. .env Configuration

Add these values to your `.env` file after setup:

```env
# ===== LINKEDIN =====
LINKEDIN_CLIENT_ID=your_client_id
LINKEDIN_CLIENT_SECRET=your_client_secret
LINKEDIN_ACCESS_TOKEN=your_60_day_access_token
LINKEDIN_PERSON_URN=urn:li:person:your_person_id
LINKEDIN_ORGANIZATION_URN=urn:li:organization:your_org_id
```

| Variable | Source |
|----------|--------|
| `LINKEDIN_CLIENT_ID` | Developer Portal → Auth tab |
| `LINKEDIN_CLIENT_SECRET` | Developer Portal → Auth tab (eye icon) |
| `LINKEDIN_ACCESS_TOKEN` | Step 6 (OAuth token) |
| `LINKEDIN_PERSON_URN` | Step 7 |
| `LINKEDIN_ORGANIZATION_URN` | Step 8 |

> ⚠️ Never commit `.env` to Git. Make sure it is listed in your `.gitignore`.

---

## 12. What You Can Post — Content Types

| Content Type | Field / Method | Example |
|-------------|---------------|---------|
| **Text Post** | `shareCommentary.text` | Plain text announcement |
| **Link Post** | `shareMediaCategory: ARTICLE` + URL | Article with link preview |
| **Image Post** | Upload via `/v2/assets` + attach | Product photo |
| **Video Post** | Upload via `/v2/assets` + attach | Demo video |

**Verified Limits:**

| Limit | Value |
|-------|-------|
| Post text (commentary) | **3,000 characters** |

> For image and video size and duration limits, verify on the [official LinkedIn API docs](https://learn.microsoft.com/en-us/linkedin/marketing/community-management/shares/ugc-post-api) — these values change and are not consistently documented in one place.

**Example — Text Post Body:**

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

## 13. API Endpoints Quick Reference

| Action | Method | Endpoint |
|--------|--------|----------|
| Get Profile | GET | `/v2/userinfo` |
| Create Post (Person or Org) | POST | `/v2/ugcPosts` |
| Get Posts | GET | `/v2/ugcPosts?q=authors&authors=List(URN)` |
| Comment on Post | POST | `/v2/socialActions/{post-urn}/comments` |
| Like a Post | POST | `/v2/socialActions/{post-urn}/likes` |
| Upload Image | POST | `/v2/assets?action=registerUpload` |

All write requests require:
- `Authorization: Bearer YOUR_ACCESS_TOKEN`
- `X-Restli-Protocol-Version: 2.0.0`

### Rate Limits

LinkedIn does not publish standard rate limits in its public documentation. To check your app's actual daily limits:

1. Open the LinkedIn Developer Portal.
2. Select your app from the list.
3. Click the **Analytics** tab.
4. The page shows usage and daily limits for every endpoint your app has called today (UTC).

> If you hit a `429 Too Many Requests` response, reduce request frequency and retry after a delay.

---

## 14. Troubleshooting

### Token Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `401 Unauthorized` | Token expired | Re-run Step 6 to generate a new token |
| `invalid_token` | Token is wrong or revoked | Re-run Step 6 |

### Permission Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `403 ACCESS_DENIED` | Wrong URN type used | Use `urn:li:person:...` for personal posts, `urn:li:organization:...` for page posts |
| `w_member_social` scope missing | "Share on LinkedIn" product not approved | Go to Products tab → Request access |
| `Insufficient permissions` | Scope missing from token | Re-generate token and select all four scopes |

### Posting Errors

| Error | Cause | Solution |
|-------|-------|----------|
| Post not visible | `visibility` is not PUBLIC | Set `MemberNetworkVisibility: PUBLIC` |
| Post not visible | `lifecycleState` not PUBLISHED | Set `lifecycleState: PUBLISHED` |
| Post appears 2-3 minutes late | LinkedIn feed delay | Normal — just wait 2-3 minutes |
| Missing header error | `X-Restli-Protocol-Version` not sent | Add `X-Restli-Protocol-Version: 2.0.0` to your request |

> **Beginner Tip (Roman Urdu):** Agar post nahi ho raha toh sab se pehle ye check karo — (1) token valid hai ya nahi, (2) URN sahi hai (person ya organization), (3) `X-Restli-Protocol-Version: 2.0.0` header laga hua hai, (4) JSON properly formatted hai.

---

## 15. Checklist — Setup Complete?

### Accounts
- [ ] LinkedIn Company Page created (Step 2)
- [ ] Developer App created (Step 3)

### Permissions
- [ ] "Share on LinkedIn" product enabled (Step 4)
- [ ] "Sign In with LinkedIn" product enabled (Step 4)
- [ ] Client ID copied (Step 5)
- [ ] Client Secret copied (Step 5)
- [ ] Redirect URLs saved (Step 5)

### Token + IDs
- [ ] Access Token generated (Step 6)
- [ ] Person URN found (Step 7)
- [ ] Organization URN found (Step 8)
- [ ] Test post successful on Personal Profile (Step 9A)
- [ ] Test post successful on Company Page (Step 9B)

### Configuration
- [ ] `.env` file updated with all values (Step 11)
- [ ] `.env` is in `.gitignore`
- [ ] Calendar reminder set for token renewal (every 50 days)

---

*Guide created for My Tech Company — AI Employee as a Service*
*Last updated: 2026-04-11*

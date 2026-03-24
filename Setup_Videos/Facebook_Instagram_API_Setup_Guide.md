# Facebook + Instagram API — Complete Setup Guide

**Date:** 2026-03-20
**Author:** Shahzain Ali + Claude Opus 4.6
**Status:** FULLY WORKING — Post, Comment, Reply on both Facebook Page + Instagram

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Token Types — Quick Summary](#2-token-types--quick-summary)
3. [Facebook Page Banana](#3-facebook-page-banana)
4. [Instagram Creator Account Banana](#4-instagram-creator-account-banana)
5. [Instagram Ko Facebook Page Se Connect Karna](#5-instagram-ko-facebook-page-se-connect-karna)
6. [Meta Developer App Banana](#6-meta-developer-app-banana)
7. [Business Portfolio Se Connect Karna](#7-business-portfolio-se-connect-karna)
8. [Short-Lived Token Generate Karna (Testing)](#8-short-lived-token-generate-karna-testing)
9. [Facebook Pe Post Karna (API Test)](#9-facebook-pe-post-karna-api-test)
10. [Instagram Pe Post Karna (API Test)](#10-instagram-pe-post-karna-api-test)
11. [Long-Lived Tokens Banana (Production)](#11-long-lived-tokens-banana-production)
12. [Token Renewal — Kab Aur Kaise](#12-token-renewal--kab-aur-kaise)
13. [.env Configuration](#13-env-configuration)
14. [What You Can Post — Content Types](#14-what-you-can-post--content-types)
15. [API Endpoints Quick Reference](#15-api-endpoints-quick-reference)
16. [Troubleshooting](#16-troubleshooting)
17. [Checklist — Setup Complete?](#17-checklist--setup-complete)

---

## 1. Prerequisites

Ye sab **pehle se ready** hona chahiye — is video mein ye nahi banayenge:

| # | Requirement | Notes |
|---|------------|-------|
| 1 | Facebook personal account | Login ke liye (already hoga) |
| 2 | **Facebook Page** (already created) | Business ya brand page — pehle se bana ke aao |
| 3 | **Instagram Creator/Business account** (already converted) | Personal account pe API nahi chalti — pehle Creator mein convert karo |
| 4 | **Instagram connected to Facebook Page** | Meta Accounts Center se connect karo pehle |
| 5 | Desktop browser | Chrome/Edge recommended |

> **Note:** Facebook Page banana, Instagram Creator account banana, aur dono ko connect karna — ye sab aapko **khud pehle se** karna hai. Is guide mein hum sirf **API access, Token generation, aur Posting** cover karenge.

**Is guide mein hum ye karenge:**

| Item | Guide Mein Step |
|------|----------------|
| Meta Developer App | Step 6 |
| Business Portfolio connection | Step 7 |
| Access Tokens (Short + Long-lived) | Steps 8–11 |
| Facebook pe post karna | Step 9 |
| Instagram pe post karna | Step 10 |

**Cost:** Sab kuch **100% free** hai. Koi payment nahi lagti.

---

## 2. Token Types — Quick Summary

Facebook aur Instagram dono tokens use karte hain. Ye samajhna zaroori hai pehle:

| Token Type | Expiry | Platform | Kab Use Hota Hai |
|------------|--------|----------|------------------|
| Short-lived User Token | **1–2 hours** | Testing only | Graph API Explorer mein quick testing |
| **Long-lived User Token** | **60 days** | **Instagram** | `IG_ACCESS_TOKEN` — Instagram automation |
| **Long-lived Page Token** | **Never expires** | **Facebook** | `FB_PAGE_ACCESS_TOKEN` — Facebook automation |

**Key Points:**
- **Instagram** ke liye Long-lived **User** Token chahiye (60 days, phir renew karo)
- **Facebook** ke liye Long-lived **Page** Token chahiye (never expires, ek baar banao bas)
- Dono tokens **ek hi App** se bante hain — alag app ki zaroorat nahi
- Long-lived Page Token tabhi never-expire hota hai jab wo Long-lived User Token se nikala jaye (Meta official documentation)

**Chinta mat karo** — ye sab step-by-step karenge aage. Pehle setup karte hain.

---

## 3. Facebook Page Banana

> **Agar Facebook Page already hai toh ye step skip karo — Step 4 pe jao.**

**Time:** 5 minutes

1. **Facebook** open karo desktop browser pe → Login karo
2. Left sidebar mein **"Pages"** click karo
3. **"+ Create New Page"** click karo
4. Page details fill karo:

| Field | Example | Notes |
|-------|---------|-------|
| **Page Name** | My Tech Company | Business ya brand ka naam |
| **Category** | Science & Technology | Dropdown se select karo |
| **Bio** | AI-Powered Automation Solutions | Short description (optional) |

5. **"Create Page"** click karo
6. Profile picture aur cover photo upload karo (optional, lekin recommended)

**Result:** Facebook Page ban gaya ✅

---

## 4. Instagram Creator Account Banana

> **Agar Instagram already Creator ya Business account hai toh skip karo — Step 5 pe jao.**
>
> API sirf Creator ya Business account pe kaam karta hai. Personal account pe API available nahi hai.

**Time:** 5 minutes

1. **Instagram App** open karo **phone** pe
2. Apni **Profile** pe jao (bottom right corner)
3. **Hamburger menu** (☰ three lines) tap karo — top right
4. **"Settings and privacy"** tap karo
5. Scroll down → **"Account type and tools"** tap karo
6. **"Switch to professional account"** tap karo
7. **"Creator"** select karo
8. Category choose karo (e.g., "Digital Creator", "Science & Tech")
9. Contact info add karo ya **"Don't use my contact info"** select karo
10. **"Done"** tap karo

### Creator vs Business — Kaunsa Select Karein?

| Feature | Creator | Business |
|---------|---------|----------|
| API access | ✅ Yes | ✅ Yes |
| Insights/Analytics | ✅ Yes | ✅ Yes |
| Profile look | Personal jaisa dikhta hai | Shop/brand jaisa dikhta hai |
| Best for | Content creators, developers | Brands, shops |

**Recommendation:** **Creator** account lo — API access milta hai aur profile natural dikhti hai.

**Result:** Instagram Creator account ready ✅

---

## 5. Instagram Ko Facebook Page Se Connect Karna

> **Ye step MANDATORY hai.** Instagram API Facebook ke through kaam karta hai — bina connection ke Instagram API nahi chalega.

**Time:** 5 minutes

### Method 1 — Meta Accounts Center (Recommended):

1. Browser mein jao: **accountscenter.facebook.com**
2. **"Accounts"** click karo
3. **"Add accounts"** click karo
4. **Instagram** select karo
5. Instagram credentials daalo (username + password)
6. Connect karo

### Method 2 — Facebook Page Settings se:

1. **Facebook** open karo desktop pe
2. Apna **Facebook Page** pe jao
3. **Page Settings** → **"Linked Accounts"** ya **"Instagram"**
4. **"Connect Account"** click karo
5. Instagram credentials daalo → **"Connect"**

### Method 3 — Instagram App se (Phone):

1. **Instagram App** → **Settings** → **"Accounts Center"** (top mein, Meta logo)
2. **"Accounts"** → **"Add accounts"** → Facebook add karo
3. Facebook login karo aur Page select karo

### Verify Connection:

Graph API Explorer mein baad mein ye check karenge (Step 8 ke baad):
```
{YOUR_PAGE_ID}?fields=instagram_business_account
```
Agar response mein `instagram_business_account` ID aaye → connection successful ✅

**Result:** Instagram aur Facebook Page connected ✅

---

## 6. Meta Developer App Banana

> Ye app dono platforms (Facebook + Instagram) ke liye use hogi. Ek hi app kaafi hai.

**Time:** 10 minutes

### 6.1 — Developer Portal Pe Jao

1. Browser mein jao: **developers.facebook.com**
2. Facebook account se automatically login ho jayega
3. **"My Apps"** click karo
4. Developer terms accept karo (agar pehli baar hai)

### 6.2 — New App Create Karo

1. **"Create App"** click karo
2. **App name** likho → e.g., `FTE Social Manager`
3. **Contact email** confirm karo
4. **"Next"** click karo

### 6.3 — Use Case Select Karo

1. **"Other"** select karo → **"Next"**
2. App type: **"Business"** select karo (**NOT** Consumer)
3. **"Next"** click karo

### 6.4 — App Details

1. **App Name:** `FTE Social Manager`
2. **Contact Email:** tumhara email
3. **Business Account:** Skip ya "No Business Manager"
4. **"Create App"** → Password confirm karo

**Result:** App ban gayi — **App ID** aur **App Secret** milte hain ✅

### 6.5 — Products Add Karo

App Dashboard → left side **"Add Product"**:

| Product | Click | Purpose |
|---------|-------|---------|
| **Facebook Login for Business** | "Set Up" | Facebook Page posting |
| **Instagram** | "Set Up" | Instagram posting |

### 6.6 — Facebook Permissions Check Karo

Left side: **"App Review"** → **"Permissions and Features"**

Ye permissions **"Ready to use"** honi chahiye:

| Permission | Purpose |
|------------|---------|
| `pages_manage_posts` | Facebook Page pe post karna |
| `pages_read_engagement` | Comments padhna |
| `pages_manage_engagement` | Comments reply karna |
| `pages_show_list` | Pages ki list dekhna |

### 6.7 — Instagram Tester Role Add Karna

1. Left side: **"App roles"** → **"Roles"**
2. **"Instagram Testers"** tab click karo
3. **"Add People"** → **"Instagram Tester"** role select karo
4. Apna Instagram username type karo
5. **"Add"** click karo

### 6.8 — Instagram Se Invite Accept Karo

1. **Instagram App** open karo phone pe
2. **Settings and privacy** → **"Apps and Websites"**
3. **"Tester Invites"** tab mein app dikhegi
4. Click karo aur **"Accept"** karo

> **Note:** Development mode mein sab permissions bina App Review ke kaam karti hain (sirf tumhare account pe). Production ke liye App Review submit karna padta hai.

---

## 7. Business Portfolio Se Connect Karna

> **⚠️ IMPORTANT:** Agar Facebook Page "New Pages Experience" pe hai (2024+ default), toh ye step **zaroori** hai. Bina iske `me/accounts` API call empty data return karti hai.

**Time:** 5 minutes

### Problem Jo Common Hai:

```json
// me/accounts API call ka response:
{"data": []}  // Empty — Page nahi milta!
```

**Ye hota hai kyunke** New Pages Experience mein Page Business Portfolio ke through managed hota hai.

### Solution — Step by Step:

**Part A: Business Portfolio Settings Kholna**

1. Browser mein jao: **business.facebook.com/settings/**
2. Apna Business Portfolio select karo

**Part B: Page Business Portfolio Mein Add Karna**

> Agar Pages section mein Page already dikh raha hai toh Part C pe jao.

1. Left side → **"Accounts"** → **"Pages"**
2. **"+ Add"** → **"Add an existing Facebook Page"**
3. Apna Page search karo aur select karo
4. **Page ID note karo** — ye number API ke liye chahiye

**Part C: App Ko Business Portfolio Se Connect Karna**

1. Left side → **"Accounts"** → **"Apps"**
2. **"+ Add"** click karo
3. Apna **App ID** paste karo (developers.facebook.com → App Settings → Basic se copy karo)

**Part D: Page Ko App Se Connect Karna**

1. Left side → **"Pages"** → Apna Page select karo
2. **"Connected assets"** tab → **"Connect assets"**
3. Apna App select karo

### ⚠️ CRITICAL — Do Tarah Ki Page IDs:

| ID Type | Example | Kahan Milti Hai | API Mein Use |
|---------|---------|-----------------|-------------|
| New Pages Experience ID | `61585031032595` | Facebook URL bar mein | ❌ NAHI karo |
| **Business Portfolio Page ID** | `1044367502088758` | Business Settings → Pages | ✅ YE use karo |

**Hamesha Business Portfolio Page ID use karo!** URL bar wali ID se "Object does not exist" error aata hai.

**Result:** Page + App + Business Portfolio sab connected ✅

---

## 8. Short-Lived Token Generate Karna (Testing)

> Ye sirf testing ke liye hai. Production ke liye Step 11 (Long-Lived Tokens) follow karo.

**Time:** 5 minutes

1. Jao: **developers.facebook.com/tools/explorer/**
2. **"Meta App"** dropdown mein apna App select karo
3. **"User or Page"** mein **"Get User Access Token"** select karo
4. **"Permissions"** mein ye add karo:

**Facebook Permissions:**
- `pages_show_list`
- `pages_read_engagement`
- `pages_read_user_content`
- `pages_manage_posts`
- `pages_manage_engagement`

**Instagram Permissions:**
- `instagram_basic`
- `instagram_content_publish`
- `instagram_manage_comments`
- `instagram_manage_insights`

5. **"Generate Access Token"** click karo
6. Popup mein:
   - "Continue as [Name]" click karo
   - Sab permissions allow karo
   - **Apna Page select karo** (checkbox ON karo)
   - Save/Done click karo

**Result:** Short-lived User Token mil gaya ✅ (1–2 hours valid)

### Page Token Nikalna (Facebook testing ke liye):

1. **GET** mode mein URL likho:
```
{YOUR_PAGE_ID}?fields=access_token
```
2. Submit karo
3. Response mein `access_token` aayega — ye **Page Token** hai

### Instagram Business Account ID Nikalna:

1. **GET** mode mein:
```
{YOUR_PAGE_ID}?fields=instagram_business_account
```
2. Response:
```json
{
  "instagram_business_account": {
    "id": "17841477106514810"
  }
}
```
3. Ye `id` tumhara **Instagram Business Account ID** hai — note karo

---

## 9. Facebook Pe Post Karna (API Test)

> **Token:** Page Token use karo (Step 8 se nikala hua)

### Test Post:

1. Graph API Explorer mein **Page Token** set karo:
   - GET mode → `{YOUR_PAGE_ID}?fields=access_token` → Submit
   - Response ka `access_token` copy karo
   - Access Token field mein paste karo (purana replace karo)

2. **POST** mode select karo

3. URL mein likho:
```
{YOUR_PAGE_ID}/feed
```

4. **"Add parameter"** click karo:
   - Key: `message`
   - Value: `Hello from Facebook API! 🚀 Test post from FTE AI Employee.`

5. **Submit** karo

### Expected Response:
```json
{
  "id": "1044367502088758_122094486825167701"
}
```

**Facebook Page pe jao — post dikhni chahiye ✅**

### Comment Karna:

- **POST** → `{post_id}/comments` → Parameter: `message` = `Test comment`

### Reply Karna:

- **POST** → `{comment_id}/comments` → Parameter: `message` = `Test reply`

---

## 10. Instagram Pe Post Karna (API Test)

> **Token:** User Token use karo (Step 8 mein generate kiya hua)
>
> **Important:** Instagram pe posting **2-step process** hai (Facebook se different)

### Step 1: Media Container Banao

1. **POST** mode select karo
2. URL: `{YOUR_IG_ID}/media`
3. **"Add parameter"** se ye add karo:

| Key | Value |
|-----|-------|
| `image_url` | Koi bhi public image URL (e.g., `https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885_1280.jpg`) |
| `caption` | `Hello from Instagram API! 🤖 Test post from FTE AI Employee.` |

> **⚠️ IMPORTANT:** Parameters ko URL mein mat likho! "Add parameter" button use karo. Warna "Only photo or video can be accepted" error aayega.

4. Submit karo

Response:
```json
{
  "id": "17869164552570218"
}
```
Ye `id` = **creation_id** hai

### Step 2: Publish Karo

1. **POST** mode
2. URL: `{YOUR_IG_ID}/media_publish`
3. Parameter: `creation_id` = Step 1 se mili ID
4. Submit karo

Response:
```json
{
  "id": "18194284255350604"
}
```

**Instagram pe jao — post dikhni chahiye ✅**

### Comment Karna:

- **POST** → `{media_id}/comments` → Parameter: `message` = `Test comment`

### Reply Karna:

- **POST** → `{comment_id}/replies` → Parameter: `message` = `Test reply`

---

## 11. Long-Lived Tokens Banana (Production)

> **Ye sabse important step hai.** Testing ke tokens 1–2 ghante mein expire ho jate hain. Production/automation ke liye long-lived tokens chahiye.

**Time:** 10 minutes

### Step 1: App Secret Nikalo

1. **developers.facebook.com** → **My Apps** → Apna App
2. Left side: **"App settings"** → **"Basic"**
3. **"App Secret"** ke saamne **"Show"** click karo
4. Password daalo agar puche
5. **App Secret copy** karo

> ⚠️ **App Secret kabhi kisi ko mat batao aur kabhi public mat karo!**

### Step 2: Long-Lived User Token Banao (Instagram ke liye — 60 days)

1. Graph API Explorer mein fresh **short-lived User Token** generate karo (Step 8 wala process)
   - Sab Facebook + Instagram permissions select karo
   - Page select karo
   - Token copy karo

2. **Naye browser tab** mein ye URL paste karo:

```
https://graph.facebook.com/v21.0/oauth/access_token?grant_type=fb_exchange_token&client_id={APP_ID}&client_secret={APP_SECRET}&fb_exchange_token={SHORT_LIVED_TOKEN}
```

3. **Replace karo:**

| Placeholder | Kya Daalna Hai |
|-------------|---------------|
| `{APP_ID}` | Tumhara App ID (App Settings → Basic se) |
| `{APP_SECRET}` | App Secret (Step 1 se) |
| `{SHORT_LIVED_TOKEN}` | Graph Explorer ka short-lived token |

4. **Enter** press karo

5. Response:
```json
{
  "access_token": "EAAxxxxxxx_BOHOT_LAMBA_TOKEN_xxxxxxx",
  "token_type": "bearer",
  "expires_in": 5184000
}
```

6. **`expires_in: 5184000`** = **60 days** — ye confirm karta hai ke long-lived token ban gaya ✅

7. **Ye token copy karo** — ye tumhara **`IG_ACCESS_TOKEN`** hai (Instagram automation ke liye)

### Step 3: Never-Expiring Page Token Banao (Facebook ke liye)

1. Step 2 ka **long-lived User Token** Graph API Explorer ke **Access Token** field mein paste karo

2. **GET** mode mein:
```
{YOUR_PAGE_ID}?fields=access_token
```

3. **Submit** karo

4. Response:
```json
{
  "access_token": "EAAxxxxxxx_PAGE_TOKEN_xxxxxxx",
  "id": "1044367502088758"
}
```

5. **Ye token copy karo** — ye tumhara **`FB_PAGE_ACCESS_TOKEN`** hai

### Kyun Never-Expiring?

| User Token Type | Se Nikala Page Token |
|-----------------|---------------------|
| Short-lived User Token (1–2 hours) | Short-lived Page Token (1–2 hours) |
| **Long-lived User Token (60 days)** | **Never-expiring Page Token** ✅ |

> Ye Meta ki **official documentation** mein confirmed hai: jab long-lived User Token se Page Token nikaalte ho toh wo **kabhi expire nahi hota** — jab tak app delete na ho ya permissions revoke na hon.

### Token Verify Karna:

Browser mein ye URL open karo:
```
https://graph.facebook.com/v25.0/{YOUR_PAGE_ID}?fields=access_token&access_token={LONG_LIVED_USER_TOKEN}
```
2. **Replace karo:**

| Placeholder | Kya Daalna Hai |
|-------------|---------------|
| `{YOUR_PAGE_ID}` | Tumhara App ID (App Settings → Basic se) |
| `{LONG_LIVED_USER_TOKEN}` | App Secret (Step 1 se) |

3. **Enter** press karo

4. Response mein jo `access_token` aaye — ye **never-expiring Page Token** hai

```json
{
  "access_token": "EAAxxxxxxx_PAGE_TOKEN_xxxxxxx",
  "id": "1044367502088758"
}
```

5. **Ye token copy karo** — ye tumhara **FB_PAGE_ACCESS_TOKEN** hai

6. `.env` file mein save karo:
```env
# Facebook — Never-expiring Page Token
FB_PAGE_ACCESS_TOKEN=EAAxxxxxxx_PAGE_TOKEN_xxxxxxx
```

---

## 12. Token Renewal — Kab Aur Kaise

### Facebook Page Token (`FB_PAGE_ACCESS_TOKEN`)

| Question | Answer |
|----------|--------|
| Expire hota hai? | **Nahi — Never expires** |
| Renew karna padta hai? | **Nahi** |
| Kab invalid hota hai? | Sirf agar: App delete karo, permissions revoke karo, ya password change karo |

**Koi action nahi chahiye — ek baar banao, bhool jao.**

### Instagram User Token (`IG_ACCESS_TOKEN`)

| Question | Answer |
|----------|--------|
| Expire hota hai? | **Haan — 60 days baad** |
| Renew karna padta hai? | **Haan — har 50 din mein** (10 din pehle) |
| Kaise renew karein? | Step 11 ka Step 2 dobara follow karo |

**Renewal Process (har 50 din):**

1. Graph API Explorer mein naya short-lived User Token generate karo (sab permissions + Page select)
2. Browser mein long-lived token URL paste karo (App ID + App Secret + new short-lived token)
3. Naya 60-day token milega
4. `.env` mein `IG_ACCESS_TOKEN` update karo

> **Tip:** Phone mein calendar reminder lagao — "Instagram Token Renew" har 50 din pe.

---

## 13. .env Configuration

Setup complete hone ke baad `.env` file mein ye values add karo:

```env
# ===== FACEBOOK =====
FB_PAGE_ID=your_business_portfolio_page_id
FB_PAGE_ACCESS_TOKEN=your_never_expiring_page_token

# ===== INSTAGRAM =====
IG_USER_ID=your_instagram_business_account_id
IG_ACCESS_TOKEN=your_60_day_long_lived_user_token

# ===== META COMMON =====
META_API_VERSION=v21.0
```

| Variable | Value Kahan Se Milegi | Token Type |
|----------|----------------------|------------|
| `FB_PAGE_ID` | Business Portfolio → Pages (Step 7) | — |
| `FB_PAGE_ACCESS_TOKEN` | Step 11, Step 3 | Never-expiring Page Token |
| `IG_USER_ID` | Step 8 (`instagram_business_account` ID) | — |
| `IG_ACCESS_TOKEN` | Step 11, Step 2 | 60-day Long-lived User Token |
| `META_API_VERSION` | Current stable version | — |

> ⚠️ **`.env` file kabhi git mein push mat karo.** Already `.gitignore` mein honi chahiye.

---

## 14. What You Can Post — Content Types

### Facebook Page

| Content Type | How | Example |
|-------------|-----|---------|
| **Text Post** | `message` parameter | "New product launch! 🚀" |
| **Link Post** | `message` + `link` parameter | Share article with URL |
| **Photo Post** | `url` parameter (public image URL) | Product photos |
| **Scheduled Post** | `scheduled_publish_time` + `published=false` | Future date post |

**Example — Text + Link Post:**
```
POST /{page_id}/feed
Parameters:
  message = "Check out our new AI tool!"
  link = "https://your-website.com"
```

### Instagram

| Content Type | How | Requirements |
|-------------|-----|-------------|
| **Photo Post** | `image_url` + `caption` | Public URL, JPEG/PNG, max 8MB |
| **Carousel Post** | Multiple `image_url` + `caption` | 2–10 images |
| **Reel (Video)** | `video_url` + `caption` | Public URL, MP4, max 100MB, 3–90 sec |

**Instagram Restrictions:**
- Image must be hosted on a **public URL** (not local file)
- Minimum image size: 320x320 pixels
- Maximum caption: 2,200 characters
- Maximum hashtags: 30

**Example — Photo Post (2-step):**
```
Step 1: POST /{ig_id}/media
Parameters:
  image_url = https://example.com/photo.jpg
  caption = "Hello world! #tech #ai"

Step 2: POST /{ig_id}/media_publish
Parameters:
  creation_id = (Step 1 response ID)
```

---

## 15. API Endpoints Quick Reference

### Facebook Page (Page Token use karo)

| Action | Method | Endpoint | Parameters |
|--------|--------|----------|------------|
| Get Page Info | GET | `/{page_id}?fields=id,name` | — |
| Get Page Token | GET | `/{page_id}?fields=access_token` | — |
| Create Text Post | POST | `/{page_id}/feed` | `message` |
| Create Link Post | POST | `/{page_id}/feed` | `message`, `link` |
| Get Posts | GET | `/{page_id}/feed` | — |
| Get Comments | GET | `/{post_id}/comments` | — |
| Comment on Post | POST | `/{post_id}/comments` | `message` |
| Reply to Comment | POST | `/{comment_id}/comments` | `message` |
| Get Page Insights | GET | `/{page_id}/insights` | `metric`, `period` |

### Instagram (User Token use karo)

| Action | Method | Endpoint | Parameters |
|--------|--------|----------|------------|
| Get IG Account ID | GET | `/{page_id}?fields=instagram_business_account` | — |
| Get IG Profile | GET | `/{ig_id}?fields=id,username,name` | — |
| Create Photo Container | POST | `/{ig_id}/media` | `image_url`, `caption` |
| Create Reel Container | POST | `/{ig_id}/media` | `video_url`, `caption`, `media_type=REELS` |
| Publish Media | POST | `/{ig_id}/media_publish` | `creation_id` |
| Get Media | GET | `/{ig_id}/media` | — |
| Get Comments | GET | `/{media_id}/comments` | — |
| Comment on Media | POST | `/{media_id}/comments` | `message` |
| Reply to Comment | POST | `/{comment_id}/replies` | `message` |
| Get Insights | GET | `/{ig_id}/insights` | `metric`, `period` |

### Rate Limits

| Platform | Limit |
|----------|-------|
| Facebook Page | ~4,800 calls per Page per 24 hours |
| Instagram Content Publishing | 25 posts per 24 hours |
| Instagram API General | 200 calls per hour per user |

---

## 16. Troubleshooting

### Token Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `OAuthException: Error validating access token` | Token expire ho gaya | Naya token generate karo (Step 8 ya Step 11) |
| `Invalid OAuth access token` | Token galat paste hua | Copy-paste check karo, extra spaces remove karo |

### Facebook Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `me/accounts` returns `{"data": []}` | Page Business Portfolio managed hai | Step 7 follow karo — App ko Business Portfolio se connect karo |
| `Object does not exist` | URL bar wali Page ID use ki | Business Portfolio Page ID use karo (Step 7 mein milti hai) |
| `requires pages_read_engagement and pages_manage_posts` | User Token se post kar rahe ho | Page Token use karo — GET se pehle nikalo |
| `Requires pages_manage_metadata` | POST mode mein token fetch kiya | Token fetch karte waqt **GET** mode use karo, POST nahi |
| Page select option nahi aata token generate mein | Purani permissions cached | Facebook Settings → Business Integrations → App remove karo → Dobara generate karo |

### Instagram Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Only photo or video can be accepted` | Parameters URL mein likhe | "Add parameter" button use karo, URL mein sirf `{ig_id}/media` likho |
| `instagram_business_account` nahi aa rahi | Instagram permissions missing ya connection nahi | Step 5 (connection) + Step 6.7 (tester role) check karo |
| Instagram permissions Graph Explorer mein nahi | Instagram product add nahi hua | App Dashboard → "Add Product" → "Instagram" → "Set Up" |
| `The image could not be downloaded` | Image URL public nahi hai ya expired | Public accessible image URL use karo (test: browser mein URL paste karo, image dikhni chahiye) |

### Business Portfolio Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Invalid redirect URI` (Instagram connect mein) | OAuth redirect URI configured nahi | developers.facebook.com → App → Facebook Login → Settings → "Valid OAuth Redirect URIs" mein `https://business.facebook.com/` add karo |
| App add nahi ho rahi Business Portfolio mein | App ID galat | developers.facebook.com → App Settings → Basic se correct App ID copy karo |

---

## 17. Checklist — Setup Complete?

### Prerequisites
- [ ] Facebook personal account ready
- [ ] Desktop browser available

### Accounts
- [ ] Facebook Page created (Step 3)
- [ ] Instagram Creator/Business account (Step 4)
- [ ] Instagram connected to Facebook Page (Step 5)

### Developer Setup
- [ ] Meta Developer App created (Step 6)
- [ ] Facebook Login for Business product added
- [ ] Instagram product added
- [ ] Instagram Tester role added + accepted
- [ ] All permissions "Ready to use"

### Business Portfolio
- [ ] App added to Business Portfolio (Step 7)
- [ ] Page connected to App
- [ ] Business Portfolio Page ID noted

### Tokens
- [ ] Short-lived token works (testing) (Step 8)
- [ ] Instagram Business Account ID found
- [ ] Facebook test post successful (Step 9)
- [ ] Instagram test post successful (Step 10)
- [ ] **Long-lived User Token generated (IG_ACCESS_TOKEN — 60 days)** (Step 11)
- [ ] **Never-expiring Page Token generated (FB_PAGE_ACCESS_TOKEN)** (Step 11)
- [ ] Token verified via debug_token URL

### Configuration
- [ ] `.env` file updated with all values (Step 13)
- [ ] `.env` is in `.gitignore`
- [ ] Calendar reminder set for Instagram token renewal (every 50 days)

---

*Guide created for AI Employee as a Service*
*Last updated: 2026-03-20*

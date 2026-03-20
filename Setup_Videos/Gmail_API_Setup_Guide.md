# Gmail API — Complete Setup Guide

**Date:** 2026-03-20
**Author:** Shahzain Bangash + Claude Opus 4.6
**Status:** FULLY WORKING — Read, Send, Modify Emails via Gmail API

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Token Type — Quick Summary](#2-token-type--quick-summary)
3. [Google Cloud Project Create Karna](#3-google-cloud-project-create-karna)
4. [Gmail API Enable Karna](#4-gmail-api-enable-karna)
5. [OAuth Consent Screen Configure Karna](#5-oauth-consent-screen-configure-karna)
6. [OAuth Client Credentials Create Karna](#6-oauth-client-credentials-create-karna)
7. [First-Time Authorization (Token Generate Karna)](#7-first-time-authorization-token-generate-karna)
8. [Verify Token Working Hai](#8-verify-token-working-hai)
9. [Test Email Send Karna](#9-test-email-send-karna)
10. [Token Lifecycle — Auto-Refresh Kaise Kaam Karta Hai](#10-token-lifecycle--auto-refresh-kaise-kaam-karta-hai)
11. [.env Configuration](#11-env-configuration)
12. [What You Can Do — Email Operations](#12-what-you-can-do--email-operations)
13. [API Scopes Quick Reference](#13-api-scopes-quick-reference)
14. [Troubleshooting](#14-troubleshooting)
15. [Checklist — Setup Complete?](#15-checklist--setup-complete)

---

## 1. Prerequisites

Ye sab **pehle se ready** hona chahiye — is video mein ye nahi banayenge:

| # | Requirement | Notes |
|---|------------|-------|
| 1 | **Gmail account** (already hoga) | Jis se emails send/receive karne hain |
| 2 | Desktop browser | Chrome/Edge recommended |

> **Note:** Sirf Gmail account chahiye — bus. Baaki sab (Google Cloud Project, API enable, credentials) is guide mein karenge.

**Is guide mein hum ye karenge:**

| Item | Guide Mein Step |
|------|----------------|
| Google Cloud Project | Step 3 |
| Gmail API enable | Step 4 |
| OAuth Consent Screen | Step 5 |
| OAuth Credentials (JSON file) | Step 6 |
| Access Token (auto-refresh) | Step 7 |
| Email send karna | Step 9 |

**Cost:** Sab kuch **100% free** hai. Gmail API Google Cloud Free Tier mein included hai.

---

## 2. Token Type — Quick Summary

Gmail ka token **ek baar setup karo — phir bhool jao.** System khud refresh karta hai, manually kuch karna nahi padta.

**Sirf tab dobara setup (Step 7) karna padta hai jab:**
- Google account ka password change karo
- Google account se permissions revoke karo
- `token.json` file delete ho jaye
- Credentials file (`.secrets/gmail_credentials.json`) + Token file (`.secrets/gmail_token.json`) — dono chahiye

---

## 3. Google Cloud Project Create Karna

**Time:** 2 minutes

1. Google Cloud Console kholein: **console.cloud.google.com**
2. Top bar mein project dropdown pe click karo
3. **"New Project"** click karo
4. Project details:

| Field | Value |
|-------|-------|
| **Project name** | FTE AI Employee |
| **Organization** | No organization (ya apni org) |

5. **"Create"** click karo
6. Project create hone ke baad usse **select** karo (top bar dropdown se)

> ⚠️ Google Cloud mein limited free projects ban sakte hain. Agar limit hit ho toh existing project use karo.

**Result:** Google Cloud Project ready ✅

---

## 4. Gmail API Enable Karna

**Time:** 1 minute

1. Left sidebar → **"APIs & Services"** → **"Library"**
2. Search box mein type karo: **"Gmail API"**
3. **Gmail API** pe click karo
4. **"Enable"** button pe click karo

**Result:** Gmail API enabled ✅

---

## 5. OAuth Consent Screen Configure Karna

> **Ye step zaroori hai — bina iske credentials nahi banenge.**

**Time:** 5 minutes

### 5.1 — Screen Create Karo

1. **"APIs & Services"** → **"OAuth consent screen"**
2. User Type select karo:

| Type | Use Case |
|------|----------|
| **External** | Testing ke liye (most cases — ye select karo) |
| Internal | Sirf Google Workspace accounts ke liye |

3. **"Create"** click karo

### 5.2 — Details Fill Karo

| Field | Value | Notes |
|-------|-------|-------|
| **App name** | FTE AI Employee | Ya koi bhi naam |
| **User support email** | apni email | Required |
| **Developer contact email** | apni email | Required |

4. **"Save and Continue"** click karo

### 5.3 — Scopes Add Karo

1. **"Add or Remove Scopes"** click karo
2. Ye scopes search karo aur select karo:

| Scope | Purpose |
|-------|---------|
| `https://www.googleapis.com/auth/gmail.readonly` | Emails read karna |
| `https://www.googleapis.com/auth/gmail.modify` | Emails mark as read |
| `https://www.googleapis.com/auth/gmail.send` | Emails send karna |

3. **"Update"** → **"Save and Continue"**

### 5.4 — Test Users Add Karo

1. **"Add Users"** click karo
2. Apni Gmail address add karo (e.g., `your@gmail.com`)
3. **"Save and Continue"**

> **Testing Mode:** Jab tak app "In Production" na ho, sirf test users hi use kar sakte hain. Personal use ke liye testing mode kaafi hai.

---

## 6. OAuth Client Credentials Create Karna

**Time:** 3 minutes

1. **"APIs & Services"** → **"Credentials"**
2. Top pe **"+ Create Credentials"** → **"OAuth client ID"**
3. Settings:

| Field | Value |
|-------|-------|
| **Application type** | Desktop app |
| **Name** | FTE AI Employee Gmail |

4. **"Create"** click karo

### Credentials Download Karo:

1. Popup mein **"Download JSON"** button pe click karo
2. Downloaded file ko **rename** karo: `gmail_credentials.json`
3. File ko move karo project ke `.secrets/` folder mein:

```
your-project/.secrets/gmail_credentials.json
```

> ⚠️ **Ye file kabhi git mein commit mat karo!** `.secrets/` already `.gitignore` mein hai.

**Result:** OAuth credentials ready ✅

---

## 7. First-Time Authorization (Token Generate Karna)

> Ye step sirf **ek baar** karna hai. Baad mein token auto-refresh hoga.
>
> **Credentials vs Token ka fark:**
> - `credentials.json` = App ka ID card (Google ko pata chale ye kaun hai)
> - `token.json` = User ki permission (Google ko pata chale ke USER ne allow kiya hai)
>
> Sirf credentials download karna kaafi nahi — **user ki permission (token) bhi chahiye.**

**Time:** 2 minutes

### Step 1: Install Library

```bash
pip install google-auth-oauthlib
```

### Step 2: Script Banao

`gmail_token_setup.py` naam se file banao:

```python
# gmail_token_setup.py
# Gmail API Token Generate Karne Ki Script
# Ek baar run karo — token auto-save ho jayega

from google_auth_oauthlib.flow import InstalledAppFlow

SCOPES = [
    "https://www.googleapis.com/auth/gmail.readonly",
    "https://www.googleapis.com/auth/gmail.modify",
    "https://www.googleapis.com/auth/gmail.send",
]

flow = InstalledAppFlow.from_client_secrets_file(
    "credentials.json",  # Google Cloud se download ki hui file (Step 6)
    SCOPES,
)

creds = flow.run_local_server(port=0)

# Token save karo
with open("token.json", "w") as f:
    f.write(creds.to_json())

print("Token saved to token.json!")
```

### Step 3: Run Karo

```bash
python gmail_token_setup.py
```

> **Note:** `credentials.json` (Step 6 mein download ki hui) same folder mein honi chahiye jahan script hai.

**Kya hoga:**
1. Browser **automatically** open hoga
2. Google account select karo
3. **"Allow"** pe click karo — sab permissions accept karo
4. Browser mein dikhega: **"The authentication flow has completed."**
5. Token automatically **`token.json`** mein save ho jayega

**Result:** `token.json` ban gaya — ab is token se emails read, send, sab kar sakte ho ✅

> **Ye script generic hai** — koi bhi apne project mein use kar sakta hai. AI agent, chatbot, automation — jahan bhi Gmail API chahiye.

### Alternative: Via FTE Command (Agar hamara project use kar rahe ho)

```bash
uv run python -m src.main gmail --authorize
```

Ye same kaam karta hai lekin project ke `.secrets/` folder mein token save karta hai.

### Method C: Manual Code Exchange (Agar MismatchingStateError Aaye)

1. Browser mein ye URL open karo (CLIENT_ID apna daalo):
```
https://accounts.google.com/o/oauth2/auth?client_id=YOUR_CLIENT_ID.apps.googleusercontent.com&redirect_uri=http://127.0.0.1:9876&response_type=code&scope=https://www.googleapis.com/auth/gmail.readonly%20https://www.googleapis.com/auth/gmail.modify%20https://www.googleapis.com/auth/gmail.send&access_type=offline&prompt=consent
```

2. Google login karo aur Allow karo
3. Browser "Site can't be reached" dikhayega — **YEH NORMAL HAI!**
4. Address bar se poora URL copy karo — `code=` ke baad wala code nikalo
5. Terminal mein run karo (apna code daalo):

```bash
uv run python -c "
from dotenv import load_dotenv; load_dotenv('.env')
import os
from pathlib import Path
from google_auth_oauthlib.flow import InstalledAppFlow
SCOPES = ['https://www.googleapis.com/auth/gmail.readonly','https://www.googleapis.com/auth/gmail.modify','https://www.googleapis.com/auth/gmail.send']
creds_path = os.getenv('GMAIL_CREDENTIALS_PATH', '.secrets/gmail_credentials.json')
token_path = os.getenv('GMAIL_TOKEN_PATH', '.secrets/gmail_token.json')
flow = InstalledAppFlow.from_client_secrets_file(creds_path, SCOPES, redirect_uri='http://127.0.0.1:9876')
flow.fetch_token(code='YOUR_CODE_HERE')
token_file = Path(token_path)
token_file.parent.mkdir(parents=True, exist_ok=True)
token_file.write_text(flow.credentials.to_json(), encoding='utf-8')
print('SUCCESS: Token saved!')
"
```

> ⚠️ Authorization code **5-10 minutes** mein expire hota hai — jaldi paste karo!

**Result:** Token saved to `.secrets/gmail_token.json` ✅

---

## 8. Done — Kya Mila?

Setup complete! Ab aapke paas ye **2 files** hain:

| File | Kya Hai | Kaise Mili |
|------|---------|-----------|
| `credentials.json` | App ka ID card | Google Cloud se download kiya (Step 6) |
| `token.json` | User ki permission | Script run karke generate kiya (Step 7) |

**In 2 files se aap Gmail API ka kuch bhi kar sakte ho** — emails read karo, send karo, mark as read karo. Ye files apne kisi bhi project mein use karo — AI agent, chatbot, automation, kuch bhi.

### Via MCP Tool (Claude Code):

```
Use the send_email_tool to send an email to your@gmail.com with subject "Test" and body "Hello!"
```

---

## 10. Token Lifecycle — Auto-Refresh Kaise Kaam Karta Hai

```
┌──────────────────────────────────────────────┐
│              Token Lifecycle                  │
├──────────────────────────────────────────────┤
│                                              │
│  First Time (Step 7):                        │
│  Browser → Google Login → Allow → Token Save │
│                                              │
│  Normal Use (Automatic):                     │
│  Token Load → Valid? → YES → Use API         │
│                        NO  → Auto-Refresh    │
│                              → New Token     │
│                              → Save & Use    │
│                                              │
│  Token Expired + No Refresh:                 │
│  → Re-authorize (Step 7 again)              │
│                                              │
└──────────────────────────────────────────────┘
```

| Token | Lifespan | Renewal |
|-------|----------|---------|
| **Access Token** | ~1 hour | Auto-refresh (code handles it) |
| **Refresh Token** | Long-lived | Valid until revoked by user |
| **Re-authorization** | — | Sirf jab refresh token bhi invalid ho |

**Matlab:** Gmail mein **manual token renewal ki zaroorat nahi hai.** System khud handle karta hai. Sirf Step 7 ek baar karo.

---

## 11. .env Configuration

Setup complete hone ke baad `.env` file mein ye values add karo:

```env
# ===== GMAIL =====
GMAIL_CREDENTIALS_PATH=.secrets/gmail_credentials.json
GMAIL_TOKEN_PATH=.secrets/gmail_token.json
```

| Variable | Purpose | Default |
|----------|---------|---------|
| `GMAIL_CREDENTIALS_PATH` | OAuth client credentials JSON file | `.secrets/gmail_credentials.json` |
| `GMAIL_TOKEN_PATH` | OAuth token (auto-generated in Step 7) | `.secrets/gmail_token.json` |

### Files in `.secrets/`:

| File | Created By | Purpose |
|------|-----------|---------|
| `gmail_credentials.json` | You (downloaded from Google Cloud — Step 6) | App identity |
| `gmail_token.json` | Auto-generated (Step 7 authorization) | User access |

> ⚠️ **Dono files kabhi git mein push mat karo.** `.secrets/` already `.gitignore` mein hai.

---

## 12. What You Can Do — Email Operations

| Operation | How | Used By |
|-----------|-----|---------|
| **Read new emails** | Gmail Watcher polls every 60 seconds | `src/watchers/gmail_watcher.py` |
| **Send email** | Dashboard + MCP tool + approval handler | `src/utils/email_sender.py` |
| **Draft email** | MCP tool (preview without sending) | `src/mcp/email_server.py` |
| **Mark as read** | Gmail Watcher (after processing) | Automatic |
| **Search emails** | Gmail API query filters | Programmatic |

### Email Flow in FTE System:

```
New Email Arrives
  → Gmail Watcher detects it (polls every 60 seconds)
  → Creates EMAIL_*.md in /Needs_Action/
  → Claude reads and plans response
  → Creates draft in /Pending_Approval/
  → Human reviews in Obsidian
  → Moves to /Approved/
  → System sends reply via Gmail API
  → Task moves to /Done/
```

---

## 13. API Scopes Quick Reference

| Scope | Permission | Required? |
|-------|-----------|-----------|
| `gmail.readonly` | Read emails, labels, threads | ✅ Yes |
| `gmail.modify` | Mark read/unread, add/remove labels | ✅ Yes |
| `gmail.send` | Send emails on behalf of user | ✅ Yes |
| `gmail.compose` | Create/update drafts | Optional |
| `gmail.labels` | Create/modify labels | Optional |

> Hamare system mein sirf first 3 scopes use hoti hain.

---

## 14. Troubleshooting

### Token Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Token has been expired or revoked` | Token expire/revoke ho gaya | Delete `.secrets/gmail_token.json` → Step 7 dobara follow karo |
| `MismatchingStateError` | Browser cache mein purana OAuth request | Sab localhost tabs band karo → Method C use karo (Step 7) |
| `invalid_grant` | Refresh token bhi invalid | Delete `.secrets/gmail_token.json` → Step 7 dobara |

### Permission Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Error 400: redirect_uri_mismatch` | Google Console mein redirect URI configured nahi | Credentials → OAuth Client → Authorized redirect URIs mein `http://localhost:8090/` add karo |
| `Error 403: access_denied` | User test users mein nahi | OAuth Consent Screen → Test Users → Apni email add karo |
| `Insufficient Permission` (sending) | Token mein `gmail.send` scope nahi | Delete `.secrets/gmail_token.json` → Step 7 se sab 3 scopes ke saath authorize karo |

### Setup Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Gmail API has not been used in project` | API enable nahi | Step 4 follow karo — APIs & Services → Library → Gmail API → Enable |
| `Gmail credentials path not set` | `.env` mein path nahi | `.env` mein `GMAIL_CREDENTIALS_PATH=.secrets/gmail_credentials.json` add karo |
| `File not found: gmail_credentials.json` | Credentials download nahi kiye | Step 6 follow karo — Google Cloud Console se JSON download karo |

---

## 15. Checklist — Setup Complete?

### Google Cloud Setup
- [ ] Google Cloud project created/selected (Step 3)
- [ ] Gmail API enabled (Step 4)
- [ ] OAuth Consent Screen configured (Step 5)
- [ ] Test users added — your Gmail address (Step 5)

### Credentials
- [ ] OAuth Client ID created — Desktop app (Step 6)
- [ ] Credentials JSON downloaded (Step 6)
- [ ] File saved as `.secrets/gmail_credentials.json`

### Authorization
- [ ] First-time authorization completed (Step 7)
- [ ] Token saved to `.secrets/gmail_token.json`
- [ ] Token verification successful — "Gmail connected" (Step 8)

### Testing
- [ ] Test email sent from Dashboard (Step 9)
- [ ] Test email sent from MCP tool (Step 9)

### Configuration
- [ ] `.env` file updated with paths (Step 11)
- [ ] `.secrets/` in `.gitignore`

### No Manual Renewal Needed!
- [ ] Understand that Gmail token auto-refreshes — no calendar reminder needed

---

*Guide created for Agentive Solutions — AI Employee as a Service*
*Last updated: 2026-03-20*

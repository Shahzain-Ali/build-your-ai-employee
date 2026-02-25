# Hackathon-0: Silver Tier — Complete Guide
**Personal AI Employee: Building Autonomous FTEs in 2026**

> **Video Length Target**: 60–90 minutes (Single Video)
> **Audience**: Developers who completed Bronze Tier
> **Focus**: Theory + Architecture + Step-by-Step Implementation
> **Language**: English (Examples in Roman Urdu)
> **Prerequisite**: Bronze Tier must be fully working

---

### PART 1: THEORY & CONCEPTS
| Section | Topic |
|---------|-------|
| 1 | Introduction — What Silver Tier Adds |
| 2 | Architecture Evolution — Bronze → Silver |
| 3 | Gmail Watcher — OAuth2 & Gmail API |
| 4 | WhatsApp Watcher — Playwright & Browser Automation |
| 5 | MCP Server — Claude Gets Hands |
| 6 | Claude Reasoning Loop & Plan.md |
| 7 | Human-in-the-Loop Approval Workflow |
| 8 | Agent Skills — Silver Tier Skills |
| 9 | Dashboard Enhancement — Multi-Platform View |
| 10 | Complete Flow — Putting It All Together |

### PART 2: IMPLEMENTATION (PROMPT-DRIVEN via SpecKit Plus)
| Section | Topic |
|---------|-------|
| 11 | How It Works — SpecKit Plus Workflow |
| 12 | The Prompts That Build Silver Tier |
| 13 | Manual Setup Steps (OAuth2, WhatsApp QR, MCP) |
| 14 | Testing & Verification |
| 15 | Troubleshooting & Common Issues |

### APPENDIX
| Section | Topic |
|---------|-------|
| A | Command Reference |
| B | Key Concepts Quick Reference |
| C | Common Beginner Questions |
| D | What's Next: Gold Tier |

---

# ═════════════════════════
# PART 1: THEORY & CONCEPTS
# ═════════════════════════

## SECTION 1: INTRODUCTION — WHAT SILVER TIER ADDS

### What You Will Learn in This Video

By the end of this video, you will:
- Understand how **Gmail Watcher** connects to your real inbox via OAuth2
- Understand how **WhatsApp Watcher** monitors messages via Playwright browser automation
- Know what an **MCP Server** is and why Claude needs "hands" to send emails
- Understand **Claude's Reasoning Loop** and Plan.md — how Claude thinks before acting
- See the complete **Human-in-the-Loop Approval** workflow for sensitive actions
- Know how to build all of this using **SpecKit Plus prompts** (you don't write code)

### Who Is This For?

- You have **completed Bronze Tier** and it's working (pm2 status shows both processes online)
- You want to connect your AI Employee to **real services** (Gmail, WhatsApp)
- You want Claude to **take real actions** (send emails, reply to messages)
- You want **human approval** before any sensitive action executes

### Prerequisites (Bronze Tier + New)

| Tool | Required | Why Needed | Check Command |
|------|----------|------------|---------------|
| Bronze Tier | ✅ Working | Foundation | `pm2 status` |
| Google Cloud Console | Account | Gmail API credentials | browser |
| WhatsApp | Personal account | QR code login | phone |
| Node.js | v24+ | MCP Email Server | `node --version` |
| Playwright | Latest | WhatsApp browser automation | `uv run playwright --version` |

> **Roman Urdu Note:**
> Bronze mein AI Employee sirf local files dekhta tha — aankh ek hi thi.
> Silver mein "aankhein" badi hoti hain — ab Gmail aur WhatsApp bhi dekhe ga.
> Aur "haath" milte hain — ab Claude email bhej bhi sakta hai MCP ke zariye.

---

## SECTION 2: ARCHITECTURE EVOLUTION — BRONZE → SILVER

### What Changed from Bronze?

Bronze was local-only. Silver connects to the real world:

```
BRONZE TIER (Local Only):
  Inbox/ folder → File Watcher → Orchestrator → Claude → Done/

SILVER TIER (Internet Connected):
  Gmail        → Gmail Watcher    → Orchestrator → Claude → Email Reply (MCP)
  WhatsApp     → WhatsApp Watcher → Orchestrator → Claude → WhatsApp Reply
  Inbox/       → File Watcher     → Orchestrator → Claude → Done/
```

### The 4 Layers — Updated for Silver

```
┌──────────────────────────────────────────────────────┐
│  LAYER 4: HANDS (MCP Servers)               ← NEW!  │
│  Claude can now SEND emails via Gmail API             │
│  MCP = Model Context Protocol (Anthropic standard)    │
├──────────────────────────────────────────────────────┤
│  LAYER 3: BRAIN (Claude Code)                         │
│  Now creates Plan.md before acting          ← NEW!   │
│  Reasoning loop: think → plan → approve → execute     │
├──────────────────────────────────────────────────────┤
│  LAYER 2: MEMORY / GUI (Obsidian Vault)               │
│  Enhanced Dashboard: watcher status, platform stats   │
│  Pending_Approval/ folder for HITL          ← NEW!   │
├──────────────────────────────────────────────────────┤
│  LAYER 1: SENSES (Python Watchers)                    │
│  File System Watcher (Bronze)                         │
│  + Gmail Watcher (OAuth2, Gmail API)        ← NEW!   │
│  + WhatsApp Watcher (Playwright)            ← NEW!   │
└──────────────────────────────────────────────────────┘
```

### Layer Comparison Table

| Layer | Bronze | Silver | What Changed |
|-------|--------|--------|-------------|
| Senses | File System Watcher only | + Gmail Watcher + WhatsApp Watcher | 2 new watchers added |
| Memory | Obsidian Vault, Dashboard | Same + enhanced Dashboard | Watcher status, platform stats |
| Brain | Claude processes files | Claude creates Plan.md first | Reasoning loop added |
| Hands | None (read only) | MCP Email Server | Claude can send emails |

> **Roman Urdu Example:**
> Bronze mein AI Employee andha tha — sirf Inbox/ folder mein file aaye to dekhta tha.
> Silver mein usko do naye "aankh" mil gayi — Gmail aur WhatsApp.
> Aur "haath" bhi mil gaye — ab sirf padhta nahi, email bhej bhi sakta hai.
> Lekin — har important kaam se pehle TUMSE poochta hai. Koi bhi bada kaam
> bina approval ke nahi hoga.

---

## SECTION 3: GMAIL WATCHER — OAUTH2 & GMAIL API

### What Is Gmail Watcher?

Gmail Watcher is a Python script that:
- Connects to your real Gmail inbox using **Google's official API**
- Polls for new unread important emails every 2 minutes
- Creates action files in `Needs_Action/` — exactly like the file watcher did in Bronze
- Does **NOT** use Claude — pure Python, zero AI tokens

### How Gmail API Authentication Works (OAuth2)

```
First Time Setup (one time only):
┌─────────────┐    ┌──────────────────┐    ┌──────────┐
│ Your Script  │───→│ Google Cloud      │───→│ Browser  │
│ (gmail_auth) │    │ Console (OAuth2)  │    │ Login    │
└─────────────┘    └──────────────────┘    └────┬─────┘
                                                 │
                              "Allow access?"     │
                              You click "Allow"   │
                                                 ▼
                                          token.json saved
                                          (auto-refresh forever)
```

**What are these files?**

| File | What It Is | Created How |
|------|-----------|-------------|
| `credentials.json` | Your app's identity (from Google Cloud Console) | You download it manually |
| `token.json` | Your login session (auto-refreshes) | Created when you first login |

> **Roman Urdu Example:**
> credentials.json = Aapke office ka ID card — Google ko batata hai "yeh app meri hai"
> token.json = Login session — jaise WhatsApp Web mein QR scan karo to baar baar nahi karna padta
>
> Pehli baar: Google browser kholega → "Allow karo?" → "Allow" dabao → token.json ban jaye ga
> Baad mein: token.json automatically refresh hota hai — baar baar login nahi karna padta

### Gmail Watcher Flow

```
Gmail Inbox
    ↓
Gmail API (OAuth2 — token.json)
    ↓
GmailWatcher.check_new_emails()
    ↓ polls every 2 minutes
New unread important email found?
    ↓ Yes
Creates: Needs_Action/EMAIL_{message_id}.md
    ↓
    Content:
    ---
    source: gmail
    sender: john@example.com
    subject: Invoice for February
    date: 2026-02-24T10:30:00
    status: pending
    ---
    # Email from john@example.com
    Subject: Invoice for February
    Body: Hi, please find attached...
    ↓
Marks email as read in Gmail (processed)
    ↓
Orchestrator picks it up → Claude processes it
```

### Key Technical Details

| Feature | Implementation |
|---------|---------------|
| Library | `google-api-python-client` + `google-auth-oauthlib` |
| Auth Method | OAuth2 (not API key — we need to read user's inbox) |
| Polling Interval | 120 seconds (configurable) |
| Filter | Unread + Important emails only |
| Duplicate Prevention | Tracks processed message IDs |
| Token Refresh | Automatic (google-auth handles it) |

### Why OAuth2 and Not Just an API Key?

```
API Key = Read-only public data → "Show me weather in Karachi"
OAuth2  = Access user's private data → "Read MY inbox, mark MY emails"

Gmail is private → OAuth2 required. No shortcut.
```

---

## SECTION 4: WHATSAPP WATCHER — PLAYWRIGHT & BROWSER AUTOMATION

### What Is WhatsApp Watcher?

WhatsApp Watcher uses **Playwright** (browser automation by Microsoft) to:
- Open WhatsApp Web in a real Chromium browser
- Login via QR code (first time only — session persists)
- Monitor for new messages from specific contacts
- Create action files in `Needs_Action/` when messages arrive

### Why Playwright and Not WhatsApp API?

| Option | Pros | Cons |
|--------|------|------|
| **WhatsApp Business API** | Official Meta API | Requires business verification, paid |
| **Twilio WhatsApp** | Reliable, official | Paid, separate number |
| **Playwright (our approach)** | Free, personal number | Browser automation, session expiry |

> **Roman Urdu Example:**
> WhatsApp ka official API personal accounts ke liye nahi hai — sirf business ke liye hai.
> Twilio bhi paid hai aur alag number chahiye.
> Playwright se hum apne personal WhatsApp Web ko automate karte hain — free aur simple.
> Lekin session 14 din mein expire ho sakta hai — dobara QR scan karna padta hai.

### What Is Playwright?

Playwright is a **browser automation library** by Microsoft:
- Controls a real Chromium browser programmatically
- Can click buttons, fill forms, read text — like a human
- Used with `playwright-stealth` to avoid bot detection

```python
# Simple Playwright example
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)  # Visible browser
    page = browser.new_page()
    page.goto("https://web.whatsapp.com")
    # QR code dikhega — phone se scan karo
```

### WhatsApp Watcher Flow

```
First Time:
┌────────────┐    ┌─────────────────┐    ┌───────────┐
│ Playwright  │───→│ WhatsApp Web    │───→│ QR Code   │
│ (Chromium)  │    │ Opens in browser│    │ Scan karo │
└────────────┘    └─────────────────┘    └─────┬─────┘
                                                │
                                         Session saved
                                    (persistent context)

After First Time:
WhatsApp Web auto-opens → already logged in → monitoring starts
```

```
Monitoring Flow:
WhatsApp Web (running in Playwright)
    ↓
Check for new unread messages (green dot / unread badge)
    ↓ polls every 30-60 seconds
New message from monitored contact?
    ↓ Yes
Extract: sender name, message text, timestamp
    ↓
Creates: Needs_Action/WA_{sender}_{timestamp}.md
    ↓
Orchestrator picks it up → Claude processes it
```

### Important: Session Expiry

| Scenario | What Happens |
|----------|-------------|
| Normal restart | Session persists — no QR scan needed |
| 14 days inactive | WhatsApp server expires session → QR scan needed again |
| Phone changes | New QR scan needed |

> **Roman Urdu Example:**
> WhatsApp Web QR scan = ek baar scan karo, session save ho jata hai.
> Lekin agar 14 din tak use nahi kiya → WhatsApp server session expire kar deta hai.
> Yeh WhatsApp ki taraf se hota hai — humara code nahi rok sakta.
> Solution: System regularly chalao taake session expire na ho.

### SingletonLock Issue (Common Problem)

When Playwright Chromium crashes, it leaves a lock file behind. Next launch fails with:
```
Error: SingletonLock — another instance is running
```

**Fix:** The WhatsApp Watcher automatically cleans up SingletonLock before launching.
If it still happens, manually delete the lock file from the Playwright user data directory.

---

## SECTION 5: MCP SERVER — CLAUDE GETS HANDS

### What Is MCP?

**MCP = Model Context Protocol** — created by Anthropic. It's a standard that lets Claude
call external tools directly, like sending emails or creating files.

```
Without MCP (Bronze):
Claude can only: Read files, Write files, Think

With MCP (Silver):
Claude can: Read files, Write files, Think + SEND EMAILS + CREATE DRAFTS
```

> **Roman Urdu Example:**
> Bronze mein Claude ka sirf dimaag tha — soch sakta tha, likh sakta tha, lekin
> kuch bhej nahi sakta tha. Email bhejna ho to tumhe manually karna padta tha.
>
> MCP = Claude ke haath. Ab Claude direct Gmail API ko call karke email bhej sakta hai.
> "send_email_tool" call karo → email chali gayi.
>
> Insaan ka analogy: Pehle dimaag tha bina haath ke. Ab haath bhi mil gaye.

### How MCP Works Technically

```
┌─────────────┐     stdio (JSON-RPC)     ┌──────────────────┐
│ Claude Code  │ ◄─────────────────────► │ MCP Email Server │
│ (AI Brain)   │     Tool calls          │ (Node.js)        │
└─────────────┘                          └────────┬─────────┘
                                                   │
                                                   │ Gmail API
                                                   ▼
                                            ┌──────────────┐
                                            │ Gmail (Real)  │
                                            │ Your Inbox    │
                                            └──────────────┘
```

**Key Concepts:**

| Term | Meaning |
|------|---------|
| stdio | Communication channel (standard input/output) |
| JSON-RPC | Message format (tool name + parameters as JSON) |
| Tool | A function Claude can call (e.g., `send_email_tool`) |
| Transport | How messages travel (stdio for local, HTTP for remote) |

### Our MCP Server — Two Tools

| Tool | Purpose | When Used |
|------|---------|-----------|
| `send_email_tool` | Sends a real email via Gmail API | After human approval |
| `draft_email_tool` | Creates a draft in Gmail Drafts folder | Preview before sending |

### Why Node.js and Not Python?

We tried Python first. It didn't work. Here's why:

```
Attempt 1: Python FastMCP
→ Connection timed out (30 seconds)
→ stdio transport issues with Claude Code

Attempt 2: Node.js MCP SDK
→ Also timed out!
→ Root cause: `import { google } from 'googleapis'` loads 171MB package at startup
→ Takes 30+ seconds → exceeds Claude Code's 30s connection timeout

Fix: Lazy import — only load googleapis WHEN a tool is called, not at startup
→ Server starts instantly → Claude connects within 2 seconds ✅
```

> **Roman Urdu Example — Lazy Import:**
> Socho tumhare paas ek bhari almari hai (171MB — googleapis package).
> Agar tum office mein aate hi almari ko uthane lagein → 30 second lag jaayein →
> boss samjhe ga tum nahi aaye (timeout).
>
> Lazy import = Pehle aao, baithoo, available ho jao (server start).
> Almari tab uthao jab kaam aaye (tool call).
> Boss dekhta hai tum time pe aa gaye ✅

### MCP Configuration

The `.mcp.json` file in project root tells Claude Code where the MCP server is:

```json
{
  "mcpServers": {
    "fte-email": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/project/src/mcp/index.js"],
      "env": {}
    }
  }
}
```

---

## SECTION 6: CLAUDE REASONING LOOP & PLAN.MD

### What Is the Reasoning Loop?

In Bronze, Claude was simple: get file → process → done.
In Silver, Claude **thinks first** — creates a plan before acting.

```
BRONZE (Simple):
Input → Process → Output

SILVER (Reasoning Loop):
Input → Think → Create Plan.md → Human Reviews Plan → Execute Steps → Output
```

### What Is Plan.md?

Plan.md is a **temporary working file** in the `Plans/` folder where Claude writes
its action plan before executing. It's NOT the project's architecture plan —
it's a per-task scratchpad.

```markdown
# Plan: Reply to John's Invoice Email

## Steps:
- [x] Read email content
- [x] Identify: invoice for February services
- [ ] Draft professional reply acknowledging receipt
- [ ] Request human approval for email send
- [ ] Send email via MCP after approval

## Status: In Progress
## Created: 2026-02-24T10:45:00
```

### Why Plan.md Matters

| Benefit | Explanation |
|---------|------------|
| **Transparency** | You can see what Claude is about to do BEFORE it does it |
| **Recovery** | If Claude crashes mid-task, it can resume from the plan |
| **Human Oversight** | Review the plan, approve or reject steps |
| **Audit Trail** | Plans folder shows history of all AI decisions |

> **Roman Urdu Example:**
> Bronze mein Claude seedha kaam karta tha — koi baat nahi agar galat ho.
> Silver mein Claude pehle likhta hai "Main yeh karne wala hoon:
> 1. Email padhoon ga, 2. Reply draft karoon ga, 3. Aapse approval loonga"
>
> Tum plan dekho — theek hai to approve karo, galat hai to reject karo.
> Yeh transparency hai — Claude chhup ke kuch nahi karta.

---

## SECTION 7: HUMAN-IN-THE-LOOP APPROVAL WORKFLOW

### Why Approval Is Critical in Silver

Bronze was safe — Claude only read/wrote local files. Worst case: delete and redo.
Silver is different — Claude performs **irreversible real-world actions**:

| Action | Reversible? | Risk |
|--------|-------------|------|
| Send email | ❌ No | Wrong email = professional damage |
| LinkedIn post | ❌ No (public) | Wrong post = reputation risk |
| WhatsApp reply | ❌ No | Wrong message to wrong person |
| Process local file | ✅ Yes | Low risk (Bronze-level) |

> **Roman Urdu Example:**
> Bronze mein agar Claude galat file bana de — delete karo, dubara banao. Koi nuqsaan nahi.
> Silver mein agar Claude galat email bhej de client ko — wapas nahi aa sakti.
> Isliye HITL (Human-in-the-Loop) = koi bhi bada kaam karne se pehle TUM se poochna.

### Approval Flow (File-Based)

```
Claude decides: "I need to send an email reply"
    ↓
Creates: Pending_Approval/APPROVAL_email_send_{timestamp}.md
    ↓
Content:
    ---
    action: send_email
    to: john@example.com
    subject: Re: Invoice for February
    status: pending_approval
    created: 2026-02-24T10:50:00
    ---
    # Approval Required: Send Email

    **To:** john@example.com
    **Subject:** Re: Invoice for February
    **Body:**
    Hi John,
    Thank you for sending the February invoice.
    I've reviewed it and everything looks correct.
    Payment will be processed by end of week.
    Best regards

    ## Instructions
    - Move this file to `Approved/` to send the email
    - Move this file to `Rejected/` to cancel
    ↓
Dashboard shows: ⚠️ 1 Pending Approval
    ↓
YOU open Obsidian → read the file → decide
    ↓
Move to Approved/ → Orchestrator detects → Claude sends email via MCP → Done/
Move to Rejected/ → Orchestrator detects → Claude logs rejection → Done/
```

### What Requires Approval?

| Action Type | Requires Approval? | Why |
|-------------|-------------------|-----|
| Send email | ✅ Yes | Irreversible, external |
| WhatsApp reply | ✅ Yes | Irreversible, external |
| LinkedIn post | ✅ Yes | Public, irreversible |
| Process local file | ❌ No | Safe, reversible |
| Update Dashboard | ❌ No | Internal only |

---

## SECTION 8: AGENT SKILLS — SILVER TIER SKILLS

### Bronze vs Silver Skills

Bronze had 3 skills. Silver adds 3 more specialized skills:

```
.claude/skills/
├── process_document.md        ← Bronze (still active)
├── update_dashboard.md        ← Bronze (still active)
├── create_approval_request.md ← Bronze (still active)
├── email_responder.md         ← NEW: Email handling
├── whatsapp_handler.md        ← NEW: WhatsApp handling
└── plan_creator.md            ← NEW: Reasoning loop
```

### New Skills Explained

**email_responder.md** — Handles incoming emails:
- Reads email content (sender, subject, body)
- Determines appropriate response
- Drafts professional reply
- Creates approval request before sending

**whatsapp_handler.md** — Handles WhatsApp messages:
- Reads message content and sender
- Determines if response needed
- Drafts appropriate reply
- Creates approval request before sending

**plan_creator.md** — Manages the reasoning loop:
- Creates Plan.md files for multi-step tasks
- Updates plan as steps complete
- Handles failures by revising the plan

> **Roman Urdu Example:**
> Skills = SOPs (Standard Operating Procedures).
> Bronze mein 3 SOPs thi: file process karo, dashboard update karo, approval banao.
> Silver mein 3 naye SOPs add hue: email ka jawab do, WhatsApp handle karo, pehle plan banao.
>
> Skill file = ek .md file add karo. Code change? Zero. Yahi hai Agent Skills ka fayda.

---

## SECTION 9: DASHBOARD ENHANCEMENT — MULTI-PLATFORM VIEW

### Bronze Dashboard vs Silver Dashboard

**Bronze:**
```markdown
# AI Employee Dashboard
Last Updated: 2026-02-24
Status: 🟢 Idle
Pending: 0 | Completed Today: 3
```

**Silver (Enhanced):**
```markdown
# AI Employee Dashboard
Last Updated: 2026-02-24 15:45:00
Status: 🟢 Idle

## Watcher Status
| Watcher    | Status | Last Activity      | Items Today |
|------------|--------|--------------------|-------------|
| Gmail      | ✅ Active | 2 min ago       | 5           |
| WhatsApp   | ✅ Active | 5 min ago       | 3           |
| FileSystem | ✅ Active | 1 hour ago      | 1           |

## Platform Breakdown
| Platform  | Completed |
|-----------|-----------|
| Email     | 5         |
| WhatsApp  | 3         |
| File      | 1         |

## Active Plans
| Plan | Progress |
|------|----------|
| Reply to invoice email | 75% (3/4 steps) |

## Pending Approvals: 1 ⚠️
## Completed Today: 9
## Recent Activity (Last 5)
- [15:40] Email reply to john@example.com → Pending Approval
- [15:30] WhatsApp from Ali → Processed → Done/
- [15:15] Invoice.pdf → Processed → Done/
```

### What's New in the Dashboard

| Feature | Bronze | Silver |
|---------|--------|--------|
| Watcher Status Table | ❌ | ✅ Shows all watchers active/inactive |
| Platform Breakdown | ❌ | ✅ Email vs WhatsApp vs File counts |
| Active Plans | ❌ | ✅ In-progress Plan.md with % progress |
| Pending Approvals | Basic count | Detailed list |

---

## SECTION 10: COMPLETE FLOW — PUTTING IT ALL TOGETHER

### Flow 1: Gmail Email → Claude Reply → Human Approval → Send

```
Important email arrives in your Gmail
    ↓
[Gmail Watcher — polling every 2 minutes]
Detects unread important email via Gmail API
Creates: Needs_Action/EMAIL_{message_id}.md
    ↓
[Orchestrator — polling every 60 seconds]
Sees EMAIL file → triggers Claude Code
    ↓
[Claude Code — reasoning loop]
1. Reads Company_Handbook.md → rules
2. Reads email_responder.md skill → knows how to reply
3. Creates Plan.md:
   - Step 1: Read email content ✅
   - Step 2: Draft reply ✅
   - Step 3: Request approval (email is external action)
   - Step 4: Send via MCP after approval
4. Drafts professional reply
5. Creates: Pending_Approval/APPROVAL_email_send_{timestamp}.md
6. Updates Dashboard → "⚠️ 1 Pending Approval"
    ↓
[YOU — Human-in-the-Loop]
Open Obsidian → see ⚠️
Read approval file → check the reply text
Move to Approved/
    ↓
[Orchestrator detects approval]
Triggers Claude → Claude calls MCP send_email_tool
Email sent via Gmail API ✅
File moved to Done/
Dashboard updated
```

### Flow 2: WhatsApp Message → Process → Approval → Reply

```
WhatsApp message from "Ali" arrives
    ↓
[WhatsApp Watcher — Playwright browser monitoring]
Detects unread message from monitored contact
Creates: Needs_Action/WA_Ali_{timestamp}.md
    ↓
[Orchestrator → Claude → Plan.md → Approval → Send]
Same flow as Gmail — approval required before reply
```

### Flow 3: File Drop (Same as Bronze)

```
You drop invoice.pdf in Inbox/
    ↓
[File System Watcher → Needs_Action/ → Orchestrator → Claude → Done/]
Same as Bronze — still works exactly the same way
```

### The Complete Silver Tier Architecture

```
EXTERNAL WORLD                     SILVER TIER SYSTEM
─────────────────                  ──────────────────────────────────

Gmail Inbox        ─→ GmailWatcher ────→ Needs_Action/EMAIL_*.md ──┐
WhatsApp           ─→ WAWatcher ───────→ Needs_Action/WA_*.md ────┤
Inbox/ folder      ─→ FileWatcher ─────→ Needs_Action/FILE_*.md ──┤
                                                                     ↓
                                               Orchestrator (polling 60s)
                                                         ↓
                                             Claude Code (with Skills)
                                                         ↓
                                              Plan.md (reasoning loop)
                                                         ↓
                                    ┌── Needs Approval? ──────────────────┐
                                    │ YES                                  │ NO
                                    ▼                                      ▼
                          Pending_Approval/                            Done/
                                    │                              Dashboard ✅
                              YOU DECIDE
                           ┌────────┴────────┐
                           ▼                  ▼
                      Approved/          Rejected/
                           │                  │
                           ▼                  ▼
                    MCP Email Send       Logged + Done/
                    WhatsApp Reply
                    LinkedIn Post
                           │
                           ▼
                      Done/ + Dashboard ✅
```

---

# ════════════════════════════════════════════════════════
# PART 2: IMPLEMENTATION (PROMPT-DRIVEN via SpecKit Plus)
# ════════════════════════════════════════════════════════

## SECTION 11: HOW IT WORKS — SPECKIT PLUS WORKFLOW

> **The Most Important Thing to Understand:**
> Aap code nahi likhte. Aap sirf Claude Code ko **prompts** dete hain.
> Claude sab kuch karta hai — specs banata hai, plan banata hai, code likhta hai,
> tests run karta hai. Aap sirf direction dete hain aur approve karte hain.

### The SpecKit Plus Framework (Same as Bronze)

Silver Tier follows the **exact same SpecKit Plus workflow** as Bronze:

```
Step 0 → ANALYZE      → Claude reads official docs + Bronze architecture (MUST DO FIRST)
Step 1 → /sp.specify  → Claude generates specification (spec.md)
Step 2 → /sp.plan     → Claude generates architecture plan (plan.md)
Step 3 → /sp.tasks    → Claude generates testable tasks (tasks.md)
Step 4 → /sp.implement → Claude builds everything per tasks

Manual → OAuth2 Setup → You set up Gmail credentials (one time)
Manual → WhatsApp QR  → You scan QR code for WhatsApp (one time)
Manual → MCP Config   → You configure .mcp.json (one time)
```

> **Roman Urdu Note:**
> SpecKit Plus ka pattern hamesha same hai: Specify → Plan → Tasks → Implement.
> Bronze mein yahi kiya tha, Silver mein bhi yahi karein ge.
> Sirf content alag hai — ab Gmail, WhatsApp, MCP ke baare mein.
> Manual steps sirf credentials aur login ke liye hain — code nahi likhna.

---

## SECTION 12: THE PROMPTS THAT BUILD SILVER TIER

### PROMPT 0 — Analyze Sources & Understand Context (MUST DO FIRST)

**Why this prompt is critical:**
Silver Tier Bronze ke upar build hota hai. Agar Claude ko Bronze ka architecture,
Hackathon-0 ke official requirements, aur existing codebase ki samajh nahi hogi —
toh specification galat banay ga. Yeh prompt Claude ko sab kuch padhne aur samajhne
ka mauka deta hai PEHLE spec banaye.

**Sources that Claude must analyze:**

| Source | Path | What It Contains |
|--------|------|-----------------|
| Official Hackathon Documentation | `Personal-AI-Employee-Hackathon-0-Building-Autonomous-FTEs-in-2026.pdf` | Silver Tier requirements (Page 4) |
| Bronze Tier Spec | `specs/001-bronze-fte-foundation/spec.md` | Bronze requirements, success criteria |
| Bronze Tier Plan | `specs/001-bronze-fte-foundation/plan.md` | Architecture decisions, tech stack |
| Bronze Tier Tasks | `specs/001-bronze-fte-foundation/tasks.md` | Implementation details |
| Existing Codebase | `src/`, `AI_Employee_Vault/`, `.claude/skills/` | What's already built |
| Bronze Tier Documentation | `Bronze_Tier.md` | Complete Bronze theory + implementation |

```
Go through the following sources carefully and analyze what Silver Tier requires:

1. Official Hackathon-0 documentation:
   @Personal-AI-Employee-Hackathon-0-Building-Autonomous-FTEs-in-2026.pdf
   Focus on Silver Tier requirements (Page 4) — what exactly needs to be built.

2. Bronze Tier implementation (already working):
   - Read specs/001-bronze-fte-foundation/spec.md (what Bronze built)
   - Read specs/001-bronze-fte-foundation/plan.md (architecture decisions)
   - Check existing code: src/, AI_Employee_Vault/, .claude/skills/
   - Read Bronze_Tier.md for full architecture understanding

3. System prerequisites check:
   - Verify Python, Node.js, uv, PM2 versions
   - Check if Gmail API and Playwright are available
   - Verify Bronze Tier is fully working (pm2 status)

4. Report back summary:
   - What Silver Tier officially requires (from PDF)
   - What Bronze already provides (foundation)
   - What new components need to be built
   - Any system prerequisites missing
   - Recommended implementation order

Do NOT generate any specs yet — just analyze and report.
```

**What Claude does after this prompt:**
- Reads the official PDF documentation (Silver Tier section)
- Reads all Bronze Tier specs, plans, and existing code
- Checks system prerequisites (`python3 --version`, `node --version`, etc.)
- Reports a complete analysis: what exists, what's needed, what's missing
- Aap review karein aur confirm karein to proceed

> **Roman Urdu Note:**
> Yeh sabse important step hai. Jaise koi naya employee hire ho toh pehle usko
> company ki documentation padhao, existing system samjhao, phir kaam do.
> Claude ko bhi pehle sab sources padhne do — phir spec banaye ga.
> Bina yeh step ke direct `/sp.specify` dena = bina naqsha safar karna.

---

## SECTION 12: THE PROMPTS THAT BUILD SILVER TIER

### PROMPT 1 — Generate the Specification

**What this prompt does:**
Claude reads the Hackathon-0 documentation, analyzes Silver tier requirements,
and generates a complete specification document.

```
/sp.specify

Hackathon-0 Silver Tier: Functional Assistant — Extends Bronze tier with:
1. Gmail Watcher (OAuth2, Gmail API — polls for unread important emails, creates
   EMAIL_*.md action files in Needs_Action/)
2. WhatsApp Watcher (Playwright browser automation with persistent context —
   monitors messages from specific contacts, creates WA_*.md action files)
3. Claude reasoning loop that creates Plan.md files before executing multi-step tasks
4. One working MCP server for email sending (Node.js, Gmail API,
   send_email_tool + draft_email_tool)
5. Human-in-the-loop approval workflow (Pending_Approval/ → Approved/Rejected/)
   for all sensitive external actions (email send, WhatsApp reply)
6. Enhanced Dashboard with watcher status, platform breakdown, active plans
7. Agent Skills for email handling, WhatsApp handling, and plan creation
Must maintain all Bronze tier functionality (file watcher, orchestrator, vault).
```

**What Claude generates:**
- `specs/002-silver-fte-foundation/spec.md`
- User stories with acceptance criteria
- Functional requirements (FR-xxx)
- Success criteria (SC-xxx)
- Out of scope items (Gold tier features)

---

### PROMPT 2 — Generate the Plan

**What this prompt does:**
Claude reads the spec and generates the full architecture document — technology
decisions, file structure, component design, risk analysis.

```
/sp.plan
```

**What Claude generates:**
- `specs/002-silver-fte-foundation/plan.md`
- Technology decisions:
  - `google-api-python-client` for Gmail API
  - `playwright` + `playwright-stealth` for WhatsApp
  - `@modelcontextprotocol/sdk` (Node.js v0.5.0) for MCP server
  - Lazy import pattern for googleapis (avoid 30s timeout)
- Component architecture for each watcher
- MCP server design
- Approval workflow design
- Risk analysis (OAuth expiry, session expiry, rate limits)

---

### PROMPT 3 — Generate the Tasks

**What this prompt does:**
Claude reads the plan and generates all implementation tasks — ordered, testable,
with clear acceptance criteria.

```
/sp.tasks
```

**What Claude generates:**
- `specs/002-silver-fte-foundation/tasks.md`
- Phased implementation:
  - Phase 1: Gmail OAuth2 authentication
  - Phase 2: Gmail Watcher implementation
  - Phase 3: WhatsApp Watcher with Playwright
  - Phase 4: MCP Email Server (Node.js)
  - Phase 5: Approval workflow
  - Phase 6: Claude reasoning loop + Plan.md
  - Phase 7: Agent Skills
  - Phase 8: Dashboard enhancement
  - Phase 9: Integration testing

---

### PROMPT 4 — Build Everything

**What this prompt does:**
Claude reads the tasks and implements them one by one — creating all files,
writing all code, running tests.

```
/sp.implement

Go through the tasks in specs/002-silver-fte-foundation/tasks.md one by one.
Build the complete Silver tier:

1. Gmail Watcher:
   - OAuth2 authentication (gmail_auth.py)
   - Gmail polling and action file creation (gmail_watcher.py)

2. WhatsApp Watcher:
   - Playwright setup with persistent context
   - Message monitoring and action file creation (whatsapp_watcher.py)

3. MCP Email Server:
   - Node.js with @modelcontextprotocol/sdk
   - send_email_tool and draft_email_tool
   - Lazy import for googleapis (CRITICAL — avoids 30s timeout)

4. Approval Workflow:
   - approval_handler.py watches Pending_Approval/ folder
   - Detects files moved to Approved/ or Rejected/
   - Triggers appropriate action

5. Reasoning Loop:
   - plan_manager.py creates/updates Plan.md files
   - Claude creates plan before multi-step tasks

6. Agent Skills:
   - email_responder.md, whatsapp_handler.md, plan_creator.md

7. Dashboard Enhancement:
   - Watcher status table
   - Platform breakdown
   - Active plans section

8. Integration:
   - Update main.py to start all watchers
   - Update orchestrator to handle all action types
   - All Bronze functionality preserved

Follow all requirements from spec.md exactly.
Maintain all Bronze tier functionality.
```

**What Claude builds (New Files):**

```
src/watchers/gmail_auth.py         ← OAuth2 authentication helper
src/watchers/gmail_watcher.py      ← Gmail polling + action file creation
src/watchers/whatsapp_watcher.py   ← Playwright WhatsApp monitoring
src/mcp/index.js                   ← MCP Email Server (Node.js)
src/mcp/package.json               ← Node.js dependencies
src/orchestrator/approval_handler.py ← Approval workflow handler
src/utils/plan_manager.py          ← Plan.md creation/management
src/utils/email_sender.py          ← Email sending utility
src/utils/whatsapp_sender.py       ← WhatsApp reply utility

.claude/skills/email_responder.md  ← Email handling skill
.claude/skills/whatsapp_handler.md ← WhatsApp handling skill
.claude/skills/plan_creator.md     ← Reasoning loop skill

.mcp.json                          ← MCP server configuration
```

**What Claude modifies (Existing Files):**

```
src/main.py                        ← Add Gmail + WhatsApp watcher startup
src/orchestrator/orchestrator.py   ← Handle EMAIL_*, WA_* action types
src/utils/dashboard.py             ← Add watcher status, platform stats
pyproject.toml                     ← Add new Python dependencies
```

---

## SECTION 13: MANUAL SETUP STEPS

> These steps require YOUR manual action — Claude cannot do them for you.
> Do these AFTER Claude has built the code (Prompt 4).

### Step 1: Gmail OAuth2 Setup

**Time required:** 10-15 minutes (one time only)

```
1. Go to: https://console.cloud.google.com/
2. Create a new project (or use existing)
3. Go to: APIs & Services → Library
4. Search "Gmail API" → Enable it
5. Go to: APIs & Services → Credentials
6. Click "Create Credentials" → OAuth Client ID
7. Application type: "Desktop application"
8. Download the JSON file
9. Rename it to: credentials.json
10. Move it to: .secrets/gmail_credentials.json
```

**First Run — Browser Login:**
```bash
# Run the Gmail auth script
uv run python -c "from src.watchers.gmail_auth import authenticate_gmail; authenticate_gmail()"

# Browser opens → Login with your Gmail → Click "Allow"
# token.json is created automatically in .secrets/gmail_token.json
# You never need to do this again (token auto-refreshes)
```

> **Roman Urdu:**
> Yeh sirf ek baar karna hai. Google Cloud Console pe jaao, Gmail API enable karo,
> credentials download karo. Pehli baar script chalao — browser khulega, login karo,
> "Allow" dabao. Bas. Token save ho jaye ga. Agla baar automatic.

---

### Step 2: WhatsApp QR Code Scan

**Time required:** 2 minutes (repeats every ~14 days if inactive)

```bash
# Run WhatsApp watcher — browser opens with QR code
uv run python -c "from src.watchers.whatsapp_watcher import WhatsAppWatcher; w = WhatsAppWatcher(); w.start()"

# WhatsApp Web opens in Chromium
# Open WhatsApp on your phone → Settings → Linked Devices → Link a Device
# Scan the QR code shown in the browser
# Session saved — next time auto-login
```

> **Roman Urdu:**
> WhatsApp Web wahi hai jo tum browser mein use karte ho.
> Playwright Chromium browser kholega → QR code dikhega → phone se scan karo.
> Session save ho jaye ga. 14 din tak kuch nahi karna padega.

---

### Step 3: MCP Email Server Setup

**Time required:** 5 minutes (one time only)

```bash
# Install Node.js dependencies for MCP server
cd src/mcp && npm install && cd ../..

# Verify .mcp.json exists in project root with correct path
cat .mcp.json

# Restart Claude Code to pick up MCP configuration
# Exit claude → start claude again
# Check MCP connection:
# Inside Claude Code, type: /mcp
# Should show: fte-email ✅ connected
```

> **Roman Urdu:**
> MCP server Node.js mein hai. `npm install` se dependencies install karo.
> `.mcp.json` file already Claude ne bana di hai — sirf path check karo.
> Claude Code restart karo — MCP automatically connect ho jaye ga.

---

### Step 4: Running the System

**Run all watchers together:**
```bash
uv run python src/main.py
```

**Run individual components for testing:**
```bash
# Gmail Watcher only
uv run python -c "
from src.watchers.gmail_watcher import GmailWatcher
w = GmailWatcher()
w.start()
"

# WhatsApp Watcher only
uv run python -c "
from src.watchers.whatsapp_watcher import WhatsAppWatcher
w = WhatsAppWatcher()
w.start()
"

# Orchestrator only
uv run python -c "
from src.orchestrator.orchestrator import Orchestrator
o = Orchestrator()
o.start()
"
```

**Using PM2 for production (24/7):**
```bash
pm2 start ecosystem.config.js
pm2 status
pm2 logs
```

---

## SECTION 14: TESTING & VERIFICATION

### Test 1: Gmail Watcher

```
1. Start the system: uv run python src/main.py
2. Send yourself an important email from another account
3. Wait 2 minutes
4. Check: ls AI_Employee_Vault/Needs_Action/
   → EMAIL_{message_id}.md should appear ✅
5. Check the file content — should contain sender, subject, body
```

### Test 2: WhatsApp Watcher

```
1. Start the system (WhatsApp Watcher running)
2. Send a WhatsApp message from another phone to your number
3. Wait 30-60 seconds
4. Check: ls AI_Employee_Vault/Needs_Action/
   → WA_{sender}_{timestamp}.md should appear ✅
```

### Test 3: MCP Email Server

```
1. Open Claude Code in the project directory
2. Type: /mcp
   → Should show fte-email connected ✅
3. Ask Claude: "Draft an email to test@example.com with subject Test"
   → Claude calls draft_email_tool → Draft created in Gmail Drafts ✅
4. Ask Claude: "Send an email to your-other-email@gmail.com saying Hello"
   → Claude calls send_email_tool → Check your inbox ✅
```

### Test 4: Approval Workflow

```
1. Trigger a sensitive action (email reply via orchestrator)
2. Check: ls AI_Employee_Vault/Pending_Approval/
   → APPROVAL_*.md should appear ✅
3. Read the file in Obsidian
4. Move it to Approved/
5. Wait for orchestrator to detect and execute
6. Check: ls AI_Employee_Vault/Done/
   → APPROVAL_*.md should be there ✅
```

### Test 5: Dashboard

```
1. After any watcher processes items
2. Open AI_Employee_Vault/Dashboard.md in Obsidian
3. Verify:
   - Watcher Status table shows all watchers ✅
   - Platform Breakdown shows correct counts ✅
   - Recent Activity shows latest actions ✅
```

### Silver Tier Success Criteria Checklist

| # | Criteria | How to Verify |
|---|---------|---------------|
| 1 | All Bronze requirements still work | Drop file in Inbox/ → processed |
| 2 | Two+ watcher scripts | Gmail + WhatsApp watchers running |
| 3 | Claude reasoning loop + Plan.md | Check Plans/ folder for Plan files |
| 4 | One working MCP server | `/mcp` shows fte-email connected |
| 5 | Human approval workflow | Sensitive action → Pending_Approval/ |
| 6 | All AI as Agent Skills | `.claude/skills/` has 6 skill files |

---

## SECTION 15: TROUBLESHOOTING & COMMON ISSUES

### Issue 1: MCP Server Won't Connect (Timeout)

**Symptom:** `Connection timed out after 30000ms`

**Cause:** `googleapis` npm package (171MB) loading at startup exceeds 30s timeout.

**Fix:** Ensure `index.js` uses lazy import:
```javascript
// ❌ WRONG — top-level import causes timeout
import { google } from 'googleapis';

// ✅ CORRECT — lazy import inside function
async initializeGmail() {
    const { google } = await import('googleapis');
    // ...
}
```

---

### Issue 2: SingletonLock Error (Playwright)

**Symptom:** `Error: SingletonLock — another instance is running`

**Cause:** Chromium crashed and left a lock file behind.

**Fix:** Delete the lock file:
```bash
# Find and remove SingletonLock
find ~/.cache/ms-playwright -name "SingletonLock" -delete
# Or: the WhatsApp watcher auto-cleans this on startup
```

---

### Issue 3: WhatsApp Session Expired

**Symptom:** QR code page shows again instead of auto-login.

**Cause:** 14 days of inactivity → WhatsApp server expires the session.

**Fix:** Scan QR code again. Keep system running regularly to prevent expiry.

---

### Issue 4: Gmail OAuth Token Expired

**Symptom:** `RefreshError: Token has been expired or revoked`

**Cause:** Token was revoked in Google Account settings, or refresh failed.

**Fix:**
```bash
# Delete old token
rm .secrets/gmail_token.json

# Re-authenticate
uv run python -c "from src.watchers.gmail_auth import authenticate_gmail; authenticate_gmail()"
# Browser opens → login again
```

---

### Issue 5: Orchestrator Nested Session Error

**Symptom:** `Cannot start nested Claude Code session`

**Cause:** `CLAUDE_CODE` environment variable leaks into subprocess.

**Fix:** Orchestrator removes this variable before calling Claude:
```python
env = os.environ.copy()
env.pop('CLAUDE_CODE', None)
env.pop('CLAUDE_CODE_ENTRY_POINT', None)
subprocess.run(["claude", ...], env=env)
```

---

### Issue 6: WSL2 File Detection Delay

**Symptom:** File watcher doesn't detect new files in Inbox/.

**Cause:** WSL2 doesn't support inotify for Windows-mounted drives.

**Fix:** Use `PollingObserver` instead of `Observer`:
```python
from watchdog.observers.polling import PollingObserver
observer = PollingObserver()  # Works on WSL2
```

---

# ═════════
# APPENDIX
# ═════════

## APPENDIX A: COMMAND REFERENCE

```bash
# ── System Startup ──
uv run python src/main.py              # Start all watchers + orchestrator
pm2 start ecosystem.config.js          # Start via PM2 (production)
pm2 status                              # Check process status
pm2 logs                                # View logs

# ── Individual Components ──
uv run python -c "from src.watchers.gmail_watcher import GmailWatcher; GmailWatcher().start()"
uv run python -c "from src.watchers.whatsapp_watcher import WhatsAppWatcher; WhatsAppWatcher().start()"

# ── Gmail Auth ──
uv run python -c "from src.watchers.gmail_auth import authenticate_gmail; authenticate_gmail()"

# ── MCP Server ──
cd src/mcp && npm install              # Install dependencies (one time)
node src/mcp/index.js                   # Test MCP server manually

# ── Vault Inspection ──
ls AI_Employee_Vault/Needs_Action/     # Pending tasks
ls AI_Employee_Vault/Pending_Approval/ # Awaiting your approval
ls AI_Employee_Vault/Done/             # Completed items
cat AI_Employee_Vault/Dashboard.md     # Current status

# ── SpecKit Plus ──
/sp.specify                             # Generate specification
/sp.plan                                # Generate architecture plan
/sp.tasks                               # Generate implementation tasks
/sp.implement                           # Build per tasks
```

---

## APPENDIX B: KEY CONCEPTS QUICK REFERENCE

| Concept | Simple Definition | Roman Urdu Analogy |
|---------|------------------|-------------------|
| OAuth2 | Google login permission system | "Allow karo" button — ek baar karo, phir automatic |
| Gmail API | Official way to read/send Gmail | Gmail ke andar jaane ka darwaza |
| Playwright | Browser automation by Microsoft | Robot jo browser chalata hai — insaan ki tarah |
| Stealth Mode | Hide that browser is automated | Robot ko insaan ka mask pehnana |
| MCP | Claude's tool calling protocol | Claude ke haath — bahar ki duniya se interact |
| stdio | Communication pipe between processes | Do programs ke beech ki phone line |
| Lazy Import | Load heavy package only when needed | Almari tab uthao jab zaroorat ho |
| Plan.md | Claude's task plan (temporary) | Kaam karne se pehle to-do list banana |
| Reasoning Loop | Think → Plan → Approve → Execute | Pehle socho, phir karo |
| HITL | Human-in-the-loop approval | "Sir, aap approve karein tab karoon" |
| Persistent Context | Browser session saved to disk | QR scan ek baar → login yaad rahe |
| Polling | Check at regular intervals | Har 2 minute mailbox dekhna |
| Action File | Task card in Needs_Action/ | AI ka to-do note |
| Approval File | Pending decision file | Sign karne wala document |

---

## APPENDIX C: COMMON BEGINNER QUESTIONS

**Q: Kya Bronze ka code change hota hai Silver mein?**
Haan, kuch files modify hoti hain (main.py, orchestrator.py, dashboard.py) — lekin Bronze
ka core flow wahi rehta hai. Silver Bronze ke upar build hota hai, replace nahi karta.

**Q: Gmail Watcher ke liye paid Google account chahiye?**
Nahi. Free Gmail account se kaam hota hai. Google Cloud Console bhi free tier deta hai.
Sirf Gmail API enable karna hai — koi payment nahi.

**Q: WhatsApp Watcher mere personal WhatsApp ko use karta hai?**
Haan — WhatsApp Web ke through. Jaise tum browser mein WhatsApp Web use karte ho,
waise Playwright use karta hai. Phone connected rehna chahiye (internet pe).

**Q: MCP server ko baar baar start karna padta hai?**
Nahi. Claude Code start hone pe `.mcp.json` padhta hai aur automatically MCP server
start karta hai. Tum sirf Claude Code start karo — MCP khud connect ho jata hai.

**Q: Agar main approve nahi karta to kya hoga?**
File `Pending_Approval/` mein padi rahegi. System blocked nahi hoga — doosre kaam
continue honge. Jab approve karo tab execute hoga. Jab reject karo tab cancel.

**Q: Kya multiple emails/messages ek saath process ho sakte hain?**
Haan — watchers independently action files create karte hain. Orchestrator queue
mein ek ek process karta hai (sequential — safe).

**Q: MCP server Python mein kyun nahi bana?**
Banaya tha — connect nahi hua. Python FastMCP ka stdio transport Claude Code ke saath
30 second timeout mein connect nahi ho pata tha. Node.js implementation instantly
connect hoti hai (lazy import ke saath). Working solution > theoretical preference.

**Q: LinkedIn automation Silver mein hai?**
Silver Tier spec mein hai: "Automatically Post on LinkedIn about business to generate sales."
Lekin LinkedIn ka ToS bot automation ko restrict karta hai. Test account use karo demo ke liye.
Implementation Playwright se hoti hai — same pattern as WhatsApp.

**Q: Kiro kya hai? Yeh Silver mein zaruri hai?**
Kiro ek IDE hai free Claude credits ke saath. Silver mein zaruri nahi — yeh ek optional
fallback hai jab Anthropic credits khatam hon. Plan.md ke Risk Analysis mein mention hai.

---

## APPENDIX D: WHAT'S NEXT — GOLD TIER

```
SILVER ✅ (This Video)
├── Gmail Watcher (OAuth2)
├── WhatsApp Watcher (Playwright)
├── MCP Email Server (Node.js)
├── Claude Reasoning Loop + Plan.md
├── Human-in-the-Loop Approval
└── 6 Agent Skills

        ↓

GOLD (Next Video)
├── Ralph Wiggum Loop — Claude continuously iterates on tasks
├── Odoo Integration — Business management via Docker (JSON-RPC)
├── Facebook MCP Server — Post to Facebook via Meta Graph API
├── Instagram MCP Server — Post to Instagram via Meta Graph API
├── Cross-Domain Workflows — Email → LinkedIn → CRM (automated chains)
├── CEO Briefing — Weekly automated business summary report
├── Audit Logging — Full trail of all autonomous decisions
├── Error Recovery — Self-healing when things go wrong
└── Multiple MCP Servers — Claude has many "hands" now

        ↓

PLATINUM (Future)
├── Cloud sync (always-on)
├── Multi-device access
└── Production-grade deployment
```

> **Roman Urdu Final Note:**
> Silver mein tumne AI Employee ko "aankhein" (Gmail, WhatsApp watchers) aur
> "haath" (MCP email server) diye. Ab woh bahar ki duniya se connect hai.
>
> Lekin abhi bhi har important kaam ke liye TUM se poochta hai — HITL.
> Gold mein "dimaag" powerful hoga — Claude khud sochega, chains banaye ga,
> CEO briefing generate karega. Tum sirf weekly review karo.
>
> Har tier pichle tier ke upar build hota hai. Silver galat hua toh Gold collapse.
> Isliye Silver ko theek se samjho, test karo, verify karo — phir Gold pe jaao.

---

*Hackathon-0 Silver Tier Video Guide*
*Date: February 2026 | Audience: Bronze Tier Completers | Language: English + Roman Urdu examples*
*Based on official Hackathon-0 documentation and specs/002-silver-fte-foundation/*

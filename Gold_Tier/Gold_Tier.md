# Hackathon-0: Gold Tier — Complete Guide
**Personal AI Employee: Building Autonomous FTEs in 2026**

> **Video Length Target**: 90–120 minutes (Single Video)
> **Audience**: Developers who completed Silver Tier
> **Focus**: Theory + Architecture + Step-by-Step Implementation
> **Language**: English (Examples in Roman Urdu)
> **Prerequisite**: Silver Tier must be fully working

---

### PART 1: THEORY & CONCEPTS
| Section | Topic |
|---------|-------|
| 1 | Introduction — What Gold Tier Adds |
| 2 | Architecture Evolution — Silver → Gold |
| 3 | Odoo Accounting System — Docker + JSON-RPC |
| 4 | Social Media Platforms — Facebook, Instagram, Twitter/X, LinkedIn |
| 5 | Weekly CEO Briefing Generation |
| 6 | Comprehensive Audit Logging |
| 7 | Error Recovery & Graceful Degradation |
| 8 | Ralph Wiggum Loop — Autonomous Multi-Step Tasks |
| 9 | Multiple MCP Servers Architecture |
| 10 | Complete Flow — Putting It All Together |

### PART 2: IMPLEMENTATION (PROMPT-DRIVEN via SpecKit Plus)
| Section | Topic |
|---------|-------|
| 11 | How It Works — SpecKit Plus Workflow |
| 12 | The Prompts That Build Gold Tier (Prompt 0-4) |
| 13 | Manual Setup Steps (Docker, Odoo, Meta API, MCP) |
| 14 | Testing & Verification |
| 15 | Troubleshooting & Common Issues |

> **Important:** Section 12 starts with **Prompt 0** (Analyze Sources) — this is MANDATORY before any other prompt. Do NOT skip it.

### APPENDIX
| Section | Topic |
|---------|-------|
| A | Command Reference |
| B | Key Concepts Quick Reference |
| C | Common Beginner Questions |
| D | What's Next: Platinum Tier |

---

# ═════════════════════════
# PART 1: THEORY & CONCEPTS
# ═════════════════════════

## SECTION 1: INTRODUCTION — WHAT GOLD TIER ADDS

### What You Will Learn in This Video

By the end of this video, you will:
- Understand how **Odoo Accounting** runs locally via Docker and connects via JSON-RPC API
- Understand how **Facebook Business Page** integration works via Meta Graph API
- Understand how **Instagram Business/Creator Account** integration works (same Meta API)
- Understand how **Twitter/X** automation works via Playwright (browser-based, free)
- Understand how **LinkedIn** automation works via Playwright (browser-based, free)
- Know what **Cross-Domain Integration** means — Personal + Business domains connected
- Understand **CEO Briefing** generation — automated weekly business intelligence
- Know how **Audit Logging** tracks every AI action with workflow IDs
- Understand **Error Recovery** — exponential backoff, component health tracking
- Know what the **Ralph Wiggum Loop** is — autonomous multi-step task completion
- See how **Multiple MCP Servers** work together (6 servers simultaneously)

### Who Is This For?

- You have **completed Silver Tier** and it's working (Gmail + WhatsApp watchers running)
- You want your AI Employee to handle **business tasks** (accounting, social media)
- You want **true autonomy** — Claude executes multi-step tasks without constant input
- You want **business intelligence** — weekly reports, financial summaries, analytics

### Prerequisites (Silver Tier + New)

| Tool | Required | Why Needed | Check Command |
|------|----------|------------|---------------|
| Silver Tier | ✅ Working | Foundation | `pm2 status` |
| Docker Desktop | Installed | Odoo runs in container | `docker --version` |
| Docker Compose | Installed | Multi-container orchestration | `docker compose version` |
| Meta Developer Account | Free account | Facebook + Instagram API | developers.facebook.com |
| Facebook Business Page | Created | For social media posting | facebook.com/pages |
| Instagram Business/Creator | Converted account | API requires professional account | Instagram Settings |
| Python `requests` | Added via uv | HTTP calls for JSON-RPC + Graph API | `uv pip list \| grep requests` |

> **Roman Urdu Note:**
> Silver mein AI Employee sirf Personal domain tha — Gmail, WhatsApp, LinkedIn.
> Gold mein Business domain add hota hai — Accounting (Odoo), Social Media (Facebook, Instagram).
> Aur sabse important — ab ye dono domains **connected** hain. Email aaya → Invoice bana → Email bheja → Facebook post kiya.
> Yehi hai **Cross-Domain Integration**.

---

## SECTION 2: ARCHITECTURE EVOLUTION — SILVER → GOLD

### What Changed from Silver?

Silver was Personal domain only. Gold adds Business domain and connects them:

```
SILVER TIER (Personal Domain Only):
  Gmail        → Gmail Watcher    → Orchestrator → Claude → Email Reply (MCP)
  WhatsApp     → WhatsApp Watcher → Orchestrator → Claude → WhatsApp Reply
  LinkedIn     → Playwright       → Manual posts

GOLD TIER (Personal + Business Connected):
  Gmail        → Gmail Watcher    ┐
  WhatsApp     → WhatsApp Watcher  ├→ Cross-Domain Orchestrator → Claude → 6 MCP Servers
  Odoo         ← JSON-RPC (Docker)┤    (Workflow Engine)        ↓
  Facebook     ← Meta Graph API   ┤    ┌→ Odoo (Invoice)
  Instagram    ← Meta Graph API   ┤    ├→ Facebook (Post)
  Twitter/X    ← Playwright       ┤    ├→ Instagram (Post)
  LinkedIn     ← Playwright       ┘    ├→ Twitter (Tweet)
                                       ├→ LinkedIn (Post)
                                       └→ Email (Reply)
```

 FULL CROSS-DOMAIN INTEGRATION (PERSONAL + BUSINESS)

 ### What Is Cross-Domain Integration?

 Cross-Domain Integration means **Personal** and **Business** domains work together as one connected system, not as silos.

 **Three Domains:**

 | Domain | Services | From Which Tier |
 |--------|----------|-----------------|
 | **Personal** | Gmail, WhatsApp, LinkedIn | Silver |
 | **Business - Finance** | Odoo (Invoices, Accounting) | Gold (NEW) |
 | **Business - Social** | Facebook, Instagram, Twitter | Gold (NEW) |

 ### Why Domains Must Connect

 Without Cross-Domain (Silver — silos):
 - **Scenario:** Tum freelance web developer ho. Client "Ahmed" ne email kiya: "Bhai project complete ho gaya, 50,000 ka invoice bhejo"
 - AI ne email parha, summary banaya, vault mein daal diya
 - **Bas. Khatam.** Tumhe khud Odoo mein jaake invoice banana padega, khud email karna padega, khud record rakhna padega.

 With Cross-Domain Integration (Gold — connected):
 - **Same Scenario:** Client "Ahmed" ne email kiya: "Bhai project complete ho gaya, 50,000 ka invoice bhejo"
 - AI ne email parha → samjha ke ye invoice request hai ✅
 - AI ne **Odoo Accounting** mein Ahmed ke naam se 50,000 PKR ka invoice create kiya ✅
 - AI ne **email** se Ahmed ko invoice bhej diya: "Hi Ahmed, here's your invoice #INV-2026-042" ✅
 - AI ne **WhatsApp** pe tumhe (owner ko) notify kiya: "Ahmed ka 50,000 PKR invoice create aur send ho gaya — Invoice #INV-2026-042" ✅
 - AI ne **audit log** mein ye poora workflow record kiya (workflow_id: wf-abc123) ✅

 > **Roman Urdu Example:**
 > Dekho? Ahmed ne sirf ek email bheja — aur AI ne poora kaam kar diya.
 > Invoice bhi banaya, client ko bheja bhi, aur tumhe WhatsApp pe update bhi de diya.
 > Tumhe kuch karna nahi padha — bas WhatsApp pe notification dekhi aur chain se baith gaye.
 >
 > Yeh hai asl maqsad — har domain ko pata ho ke doosre domain mein kya ho raha hai,
 > aur sab milke ek cohesive employee ki tarah kaam karein.

 ### How It Works Technically

 ```
 Trigger: Client "Ahmed" ne email kiya: "Project ho gaya, 50,000 ka invoice bhejo"
     ↓
 Gmail Watcher: Naya email detect kiya → Orchestrator ko bheja
     ↓
 Orchestrator: "Ye invoice request hai" → Claude Code ko trigger kiya
     ↓
 Claude Code (AI Brain): Email analyze kiya → samjha ke invoice banana hai
     → Plan banaya: 4 steps execute karne hain
     ↓
 Claude → Action 1: Odoo MCP Server → Ahmed ke naam 50,000 ka invoice create (Business-Finance)
 Claude → Action 2: Email MCP Server → Ahmed ko invoice email bhejo (Personal)
 Claude → Action 3: WhatsApp MCP → Owner (tumhe) notify karo: "Ahmed ka invoice sent" (Personal)
 Claude → Action 4: Audit Log → Poora workflow record karo with workflow_id (System)
     ↓
 Done! Claude ne sab decide kiya, MCP servers ne execute kiya.
 ```

 ### Workflow Engine

 The **Workflow Engine** (`src/orchestrator/workflow_engine.py`) manages cross-domain workflows:

 **Responsibilities:**
 - Generate unique `workflow_id` (UUID format)
 - Execute steps sequentially
 - Track completed/failed/remaining steps
 - Handle partial failures (preserve completed steps)
 - Log all actions with shared `workflow_id`

 ### Workflow State Tracking

 ```json
 {
   "workflow_id": "wf-abc123",
   "trigger": "EMAIL_18d4a5b2.md",
   "steps_total": 4,
   "steps_completed": 2,
   "steps_failed": 0,
   "steps_remaining": 2,
   "status": "in_progress",
   "actions": [
     {"step": 1, "action": "odoo_invoice_created", "status": "success"},
     {"step": 2, "action": "email_sent_to_client", "status": "success"},
     {"step": 3, "action": "whatsapp_owner_notified", "status": "pending"},
     {"step": 4, "action": "audit_log_recorded", "status": "pending"}
   ]
 }
 ```

 ### Cross-Domain Use Cases (Real Industry Examples)

 | # | Scenario | Trigger | What AI Does (Cross-Domain) |
 |---|----------|---------|----------------------------|
 | 1 | **Freelancer Invoice** | Client emails: "Project done, invoice bhejo" | Odoo invoice create → Client ko email → Owner ko WhatsApp notify |
 | 2 | **Payment Received** | Client WhatsApp: "Payment kar di" | Odoo mein payment mark → Client ko thank you email → Owner ko WhatsApp confirm |
 | 3 | **Overdue Follow-up** | Odoo: Invoice 7 days overdue | Client ko reminder email → Owner ko WhatsApp alert |
 | 4 | **Product Launch** | Owner WhatsApp: "Naye product ki post karo" | Facebook post → Instagram post → Twitter post → LinkedIn post |
 | 5 | **Weekly Report** | Sunday 10 PM (scheduled) | Odoo se financial data + Social media analytics → CEO Briefing generate → Owner ko email |

 ### Audit Logging with Workflow IDs

 Every action in a workflow shares the same `workflow_id`:

 ```json
 // Log entry 1 — Invoice created
 {
   "timestamp": "2026-03-06T10:30:00Z",
   "action_type": "odoo_invoice_created",
   "workflow_id": "wf-abc123",
   "mcp_server": "fte-odoo",
   "result": "success"
 }

 // Log entry 2 — Email sent to client
 {
   "timestamp": "2026-03-06T10:30:15Z",
   "action_type": "email_sent",
   "workflow_id": "wf-abc123",
   "mcp_server": "fte-email",
   "result": "success"
 }

 // Log entry 3 — Owner notified on WhatsApp
 {
   "timestamp": "2026-03-06T10:30:20Z",
   "action_type": "whatsapp_notification",
   "workflow_id": "wf-abc123",
   "mcp_server": "fte-whatsapp",
   "result": "success"
 }
 ```

 > **Benefit:** Kal ko agar kuch galat ho — toh `wf-abc123` search karo logs mein aur poora workflow trace ho jayega.

 ### What Are Multiple MCP Servers?

 In Silver Tier, you had **one MCP server** (Email). In Gold Tier, you have **6 MCP servers** — one for each service:

 ```
 ┌──────────────────────────────────────────────────────────────────────┐
 │                        CLAUDE CODE (AI)                              │
 │                      (Orchestrates All)                              │
 └──────────────────────────┬───────────────────────────────────────────┘
                            │
    ┌──────────┬──────────┬─┼─────────┬──────────┬──────────┐
    ▼          ▼          ▼ ▼         ▼          ▼          ▼
 ┌────────┐┌────────┐┌────────┐┌─────────┐┌────────┐┌────────┐
 │ Email  ││  Odoo  ││Facebook││Instagram││Twitter ││LinkedIn│
 │  MCP   ││  MCP   ││  MCP   ││   MCP   ││  MCP   ││  MCP   │
 └───┬────┘└───┬────┘└───┬────┘└────┬────┘└───┬────┘└───┬────┘
     │         │         │          │         │         │
     ▼         ▼         ▼          ▼         ▼         ▼
 ┌────────┐┌────────┐┌────────┐┌─────────┐┌────────┐┌────────┐
 │ Gmail  ││ Odoo   ││ Meta   ││  Meta   ││Twitter ││LinkedIn│
 │  API   ││JSON-RPC││ Graph  ││  Graph  ││  Web   ││  Web   │
 └────────┘└────────┘└────────┘└─────────┘└────────┘└────────┘
 ```

 ### MCP Servers in Gold Tier

 | MCP Server | Domain | Method | Tools Available |
 |------------|--------|--------|-----------------|
 | `fte-email` | Personal — Email | Gmail API | send_email, draft_email |
 | `fte-odoo` | Business — Finance | JSON-RPC | create_invoice, get_invoices, mark_payment, get_weekly_summary, create_expense, get_expenses |
 | `fte-facebook` | Business — Social | Meta Graph API | create_page_post, get_page_posts, get_post_comments, reply_to_comment, get_page_insights |
 | `fte-instagram` | Business — Social | Meta Graph API | create_ig_post, create_ig_reel, get_ig_media, get_ig_comments, reply_ig_comment, get_ig_insights |
 | `fte-twitter` | Business — Social | Playwright | post_tweet, get_my_tweets, reply_to_tweet, like_tweet |
 | `fte-linkedin` | Business — Social | Playwright | create_post, get_posts, comment_post, like_post |

 > **Roman Urdu Example:**
 > 6 MCP servers hain — jaise 6 alag alag workers:
 > - Email wala — Gmail handle karta hai
 > - Odoo wala — Invoices aur accounting handle karta hai
 > - Facebook wala — Page posts handle karta hai
 > - Instagram wala — Photos aur reels handle karta hai
 > - Twitter wala — Tweets handle karta hai
 > - LinkedIn wala — Professional posts handle karta hai
 >
 > Sab alag hain, lekin sab Claude Code se connected hain.

 ---

### The 4 Layers — Updated for Gold

```
┌──────────────────────────────────────────────────────────────────┐
│  LAYER 4: HANDS (MCP Servers)                          ← GOLD:   │
│  fte-email (Silver)                                              │
│  + fte-odoo (NEW — JSON-RPC to Docker)                           │
│  + fte-facebook (NEW — Meta Graph API)                           │
│  + fte-instagram (NEW — Meta Graph API)                          │
│  + fte-twitter (NEW — Playwright)                                │
│  + fte-linkedin (NEW — Playwright)                               │
├──────────────────────────────────────────────────────────────────┤
│  LAYER 3: BRAIN (Claude Code)                                    │
│  Now has Ralph Wiggum Loop (autonomous multi-step)      ← GOLD:  │
│  + Workflow Engine (cross-domain orchestration)                  │
│  + CEO Briefing Generator (weekly intelligence)                  │
├──────────────────────────────────────────────────────────────────┤
│  LAYER 2: MEMORY / GUI (Obsidian Vault)                          │
│  Enhanced Dashboard: Financial summary, Social metrics  ← GOLD:  │
│  + Briefings/ folder (weekly reports)                            │
│  + Tasks/ folder (Ralph Wiggum tasks)                            │
│  + .state/health.json (component health)                         │
├──────────────────────────────────────────────────────────────────┤
│  LAYER 1: SENSES (Python Watchers)                               │
│  File System Watcher (Bronze)                                    │
│  Gmail Watcher (Silver)                                          │
│  WhatsApp Watcher (Silver)                                       │
│  + Cross-Domain Triggers (Gold) — Email → Odoo → Social          │
└──────────────────────────────────────────────────────────────────┘
```

### Layer Comparison Table

| Layer | Silver | Gold | What Changed |
|-------|--------|------|--------------|
| Senses | File + Gmail + WhatsApp | Same + Cross-Domain triggers | Triggers cascade across domains |
| Memory | Vault + Dashboard | Same + Briefings/ + Tasks/ + .state/ | New folders for new features |
| Brain | Claude + Plan.md | Claude + Ralph Wiggum + Workflow Engine | Autonomous multi-step execution |
| Hands | 1 MCP (email) | 6 MCPs (email, odoo, facebook, instagram, twitter, linkedin) | 5 new MCP servers |

### The Gold Tier Difference: 14 New Capabilities

| # | Capability | Description | Business Value |
|---|------------|-------------|----------------|
| 1 | **Odoo Accounting** | Self-hosted accounting via Docker | Track invoices, payments, expenses |
| 2 | **Facebook Integration** | Business Page posting via Meta Graph API | Automated social media presence |
| 3 | **Instagram Integration** | Business/Creator account posting via Meta Graph API | Visual content automation |
| 4 | **Twitter/X Integration** | Tweet posting via Playwright (free, no API cost) | Real-time social media presence |
| 5 | **LinkedIn Integration** | Professional posting via Playwright (free) | B2B networking automation |
| 6 | **Cross-Domain Workflows** | Personal triggers → Business actions | End-to-end automation |
| 7 | **CEO Briefing** | Weekly automated business report | Monday morning intelligence |
| 8 | **Audit Logging** | Every action logged with workflow ID | Complete traceability |
| 9 | **Error Recovery** | Exponential backoff retry | System doesn't crash on failures |
| 10 | **Graceful Degradation** | Continue when components fail | High availability |
| 11 | **Component Health** | Track health of all domains | Know what's working |
| 12 | **Ralph Wiggum Loop** | Autonomous multi-step tasks | True employee-like behavior |
| 13 | **Multiple MCP Servers** | 6 servers running simultaneously | Modular, scalable architecture |
| 14 | **Agent Skills (Gold)** | New skills for all functionality | Reusable, maintainable AI logic |

> **Roman Urdu Example:**
> Silver mein agar client ka email aata tha "Invoice bhejo" → AI padhta tha, summary banata tha, vault mein daal deta tha.
> Gold mein same email aata hai → AI invoice banata hai Odoo mein → client ko email pe bhejta hai → tumhe WhatsApp pe notify karta hai.
> Yehi hai **Cross-Domain Integration** — ek trigger, multiple domains mein actions.

---

## SECTION 3: ODOO ACCOUNTING SYSTEM — DOCKER + JSON-RPC

### What Is Odoo?

Odoo is a **free, open-source business management software**. It has many modules (CRM, Inventory, HR, etc.) but Gold tier uses
only the **Accounting module**.

Think of Odoo as your **digital accountant** — it keeps all your financial records.

### Why Use Odoo?

- **Free** — No money needed
- **Self-hosted** — Runs on your own system, not cloud dependent
- **JSON-RPC API** — Your AI can talk to it programmatically
- **MCP Server** — Claude Code can control Odoo directly

### What Odoo Handles

| Function | Description |
|----------|-------------|
| **Invoices** | Create, send, and track client invoices |
| **Payments** | Record payments received, track what's pending |
| **Expenses** | Track business expenses |
| **Financial Reports** | Generate profit/loss, balance sheet |
| **Audit Trail** | Every transaction is recorded |

### Odoo Setup (Docker)

> **Roman Urdu Note:**
> Odoo Docker mein chalta hai. Docker install hona chahiye (basic knowledge assume kiya ja raha hai).
>
> Setup command:
> ```bash
> docker run -d -p 8069:8069 --name odoo --env DB_PASSWORD=mysecretpassword -v odoo-data:/var/lib/odoo odoo:17
> ```
> Ye Odoo 17 community edition chala dega. Access: `localhost:8069`

### What Claude Does on Odoo

Your AI agent (via Odoo MCP Server) will:

1. **Create Invoice** — When client requests
2. **Check Payment Status** — When payment arrives
3. **Mark Invoice "Paid"** — When payment confirmed
4. **Generate Weekly Summary** — For CEO Briefing
5. **Generate Audit Report** — Transaction history

### Real-World Example — Complete Flow

```
Day 1 — Email aaya:
Gmail → "Ahmed: Invoice bhejo 50,000 ka"
     ↓
AI ne email parha → Odoo MCP ko bola
     ↓
Odoo mein invoice create hua (Status: Draft)
     ↓
AI ne invoice PDF export kiya → Email MCP se Ahmed ko bheja (Status: Sent)

Day 5 — Payment aayi:
WhatsApp → "Ahmed: Payment kar di"
     ↓
AI ne Odoo check kiya → Payment confirm → Status "Paid" mark hua
     ↓
AI ne thank you email bheji

Monday Morning — CEO Briefing:
AI ne Odoo se report nikali:
"Is hafte 50,000 revenue aaya (Ahmed - Paid)"
 ```

> **Roman Urdu Example:**
> Sochnay aap ek online store chalate hain. Jab koi customer order karta hai,
> Gold Tier Odoo mein automatically invoice create karega, customer ka record save karega,
> aur products ki inventory update karega. Ye sab automatically hoga, aapko manually karni ne hogi.
>
> Odoo sirf template nahi hai — ye ek complete accounting system hai.
> Aapka AI isko "remote control" ki tarah use karta hai MCP ke zariye.



> **Roman Urdu Example:**
> Docker ek container hai. Docker mein Odoo run hota hai — aapke system se isolated, lekin aap use kar sakte ho.
> Jab kaam khatam → container delete → system clean.

### Why Docker for Odoo?

| Reason | Explanation |
|--------|-------------|
| **Easy Setup** | One command: `docker compose up -d` |
| **Isolated** | Odoo runs in container, doesn't touch your system |
| **Reproducible** | Same setup on any machine with Docker |
| **Easy Cleanup** | `docker compose down` → everything removed |
| **Local-First** | Runs on your machine, no cloud dependency |

### How Odoo Connects: JSON-RPC API

**JSON-RPC** is a simple way to call functions over HTTP.

**How it works:**
```
1. AI Employee wants to create invoice
2. Odoo MCP Server sends HTTP POST to http://localhost:8069/jsonrpc
3. Body contains: which function to call + parameters
4. Odoo responds with result (invoice ID, status, etc.)
```

**Example JSON-RPC Call:**
```json
POST http://localhost:8069/jsonrpc

{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "service": "object",
    "method": "execute_kw",
    "args": [
      "fte_gold",     // Database name
      "admin",        // Username
      "password",     // Password
      "account.move", // Model (invoices)
      "create",       // Action
      [{
        "move_type": "out_invoice",
        "partner_id": 7,
        "invoice_line_ids": [...]
      }]
    ]
  },
  "id": 1
}
```

### Odoo MCP Server Tools

The `fte-odoo` MCP server exposes 6 tools:

| Tool | Purpose | Example |
|------|---------|---------|
| `create_invoice` | Create customer invoice | Client X ko 5000 PKR ka invoice |
| `get_invoices` | List invoices | Saare pending invoices dikhao |
| `mark_payment_received` | Record payment | Client ne payment bhej di |
| `get_weekly_summary` | Financial summary | Is hafte kitni kamayi hui |
| `get_expenses` | List expenses | Saare expenses dikhao |
| `create_expense` | Record expense | Office supplies ka expense daalo |



### Odoo Setup Checklist

- [ ] Docker installed (`docker --version`)
- [ ] Docker Compose installed (`docker compose version`)
- [ ] Odoo container running (`docker compose ps`)
- [ ] Odoo accessible at http://localhost:8069
- [ ] Database created (name: `fte_gold`)
- [ ] Invoicing module installed
- [ ] Expenses module installed
- [ ] Credentials in `.env` file (ODOO_URL, ODOO_DB, ODOO_USER, ODOO_PASSWORD)

---

## SECTION 4: SOCIAL MEDIA PLATFORMS — Facebook, Instagram, Twitter/X, LinkedIn

Gold Tier integrates **four social media platforms**:

| Platform | Method | Status |
|---------|--------|--------|
| **Facebook Page** | Meta Graph API | Production ready |
| **Instagram** | Meta Graph API | Production ready |
| **Twitter/X** | Playwright (Browser) | Production ready |
| **LinkedIn** | Playwright (Browser) | Production ready |

### Facebook + Instagram — Meta Graph API

> **Roman Urdu Note:**
> Facebook aur Instagram dono Meta ki company hain. Dono ke liye official API available hai
> jisko hum "Meta Graph API" kehte hain. Yeh API-based approach hai, stable aur reliable.

**Why Meta Graph API?**

| Approach | Pros | Cons |
|----------|------|------|
| **Meta Graph API (Recommended)** | Stable, Fast, Official | Setup complex (tokens, permissions) |
| **Playwright (Browser)** | Easy setup | Fragile (UI change se toot jaye) |

### What is Meta Graph API?

**Meta Graph API** is Facebook's official API for:
- Facebook Pages (business pages)
- Instagram Business/Creator accounts
- WhatsApp Business (not used in Gold Tier)

**Key Point:** Facebook **personal profiles** pe API se post **NAHI** kar sakte. Sirf **Business Pages** pe kaam karta hai.


### Twitter — Playwright

> **Roman Urdu Note:**
> Twitter ka official API ab paid hai ($5/month basic). Free tier nahi milta naye developers ko.
> Isliye hum Playwright use karte hain — free, browser automation se kaam chalta hai.

**What You Can Do:**
- Post tweets (In this video we only check post)
- Reply to tweets
- Like tweets

### LinkedIn — Playwright

> **Roman Urdu Note:**
> LinkedIn ka official API posting ke liye restricted hai (sirf approved partners ko milta hai).
> Isliye hum wahan bhi Playwright use karte hain, jaise WhatsApp mein kiya tha.

**What You Can Do:**
- Create text posts (In this video we only check post)
- Comment on posts
- Like posts

### Human-in-the-Loop (HITL)

**All Facebook posts require approval before execution:**

```
1. AI decides to post
2. Creates approval file in Needs_Action/
3. You review and move file to Approved/
4. MCP server posts to Facebook
5. File moves to Done/
```

> **Roman Urdu Example:**
> AI Employee Facebook pe post karna chahta hai.
> Lekin woh khud se post NAHI karta.
> Pehle aapko dikhata hai: "Ye post karna hai, approve karo?"
> Aap approve karte ho → tab post hota hai.
> Yehi hai **Human-in-the-Loop**.

---

### Instagram vs Facebook API

| Feature | Facebook | Instagram |
|---------|----------|-----------|
| Account Type | Business Page | Business/Creator |
| Posting Flow | 1-step | 2-step (container) |
| Daily Post Limit | None (reasonable) | 25 (hard limit) |
| Media Types | Text, Link, Image | Image, Video, Reel |
| API Base | Same Meta Graph API | Same Meta Graph API |
| Token Type | Page Token | User Token |

> **Roman Urdu Example:**
> Facebook aur Instagram dono ka API ek hi hai — Meta Graph API.
> Farq bas itna hai ke Instagram mein 2 steps hain:
> 1. Pehle container banao (image upload)
> 2. Phir publish karo
> Facebook mein direct post ho jata hai.
>
> **Token Rule:**
> - Facebook ke liye **Page Token** use karo
> - Instagram ke liye **User Token** use karo

---

## SECTION 5: WEEKLY CEO BRIEFING GENERATION (CEO BRIEFING)

### What is CEO Briefing?

**CEO Briefing** is an automated weekly business intelligence report.

**Generated:** Every Sunday at 10 PM (scheduled via APScheduler)

**Content:**
- Financial summary from Odoo (revenue, expenses, pending invoices)
- Social media metrics (Facebook + Instagram posts, reach, engagement)
- Communication summary (Gmail + WhatsApp activity)
- Action items and proactive suggestions

### CEO Briefing Architecture

```
Sunday 10 PM (APScheduler trigger)
  ↓
CEOBriefingGenerator.generate()
  ↓
Collect data from all domains:
  ├─ Odoo MCP → get_weekly_summary()
  ├─ Facebook MCP → get_page_insights()
  ├─ Instagram MCP → get_ig_insights()
  └─ Vault → Count EMAIL_/WA_ files in Done/
  ↓
Generate markdown report
  ↓
Save to Briefings/CEO_Briefing_YYYY-MM-DD.md
  ↓
Optionally email to owner (via fte-email MCP)
```

### CEO Briefing Template

```markdown
---
type: ceo_briefing
week_start: 2026-03-03
week_end: 2026-03-09
generated_at: 2026-03-09T22:00:00Z
data_sources: [odoo, facebook, instagram, gmail, whatsapp]
missing_sources: []
---

# Monday Morning CEO Briefing
## Week of Mar 3 – Mar 9, 2026

## Financial Summary (Odoo)
| Metric | Value |
|--------|-------|
| Revenue | PKR 150,000 |
| Pending Invoices | 3 (PKR 45,000) |
| Expenses | PKR 25,000 |
| Net Profit | PKR 125,000 |

## Social Media (Facebook + Instagram)
| Platform | Posts | Reach | Engagement |
|----------|-------|-------|------------|
| Facebook | 5 | 2,500 | 180 |
| Instagram | 3 | 1,800 | 95 |

## Communications (Gmail + WhatsApp)
- Emails processed: 23
- WhatsApp messages: 15
- Pending responses: 2
- New client contacts: 3

## Action Items
1. Follow up with ABC Corp (invoice overdue 5 days)
2. Instagram engagement dropped 15% — consider more visual content
3. 2 client emails awaiting response

## Proactive Suggestions
- Schedule a Facebook post about recent project completion
- Send payment reminder to XYZ Ltd (due in 3 days)
```

### Handling Missing Data Sources

If a domain is unavailable (e.g., Odoo Docker is down):

```markdown
## Financial Summary (Odoo)
**Data unavailable** — Odoo service was down during report generation.
Last known status: Healthy (2026-03-08T15:30:00Z)

## Social Media (Facebook + Instagram)
[... data available ...]
```

> **Graceful degradation:** Report is still generated with available data.

### APScheduler Configuration

```json
// config/schedules.json
{
  "id": "ceo_briefing_weekly",
  "task": "generate_ceo_briefing",
  "cron": "0 22 * * 0",  // Sunday at 22:00
  "description": "Weekly CEO Briefing every Sunday at 10 PM"
}
```

> **Roman Urdu Example:**
> Har Sunday raat 10 baje, AI Employee automatically:
> - Odoo se financial data leta hai
> - Facebook/Instagram se analytics leta hai
> - Gmail/WhatsApp se communication count leta hai
> - Sab ko mila ke ek report banata hai
> - Monday morning aapko ready milti hai — "CEO Briefing"
> Jaise aapka assistant har hafte report prepare karke de.

---

## SECTION 6: COMPREHENSIVE AUDIT LOGGING

### What is Audit Logging?

**Audit Logging** records every action the AI Employee takes in structured JSON format.

**Purpose:**
- **Traceability:** Kaunsa action kab, kyun, kaise hua
- **Debugging:** Error analysis, root cause identification
- **Compliance:** Business records, accountability
- **Security:** Detect unauthorized actions

### Audit Log Entry Structure (Gold Tier)

```json
{
  "timestamp": "2026-03-06T10:30:00Z",
  "action_type": "odoo_invoice_created",
  "actor": "fte-odoo",
  "target": "account.move:42",
  "parameters": {
    "partner_id": 7,
    "amount": 5000,
    "due_date": "2026-03-20"
  },
  "approval_status": "approved",
  "result": "success",
  "duration_ms": 1250,
  "mcp_server": "fte-odoo",
  "workflow_id": "wf-abc123",
  "domain": "odoo",
  "error_message": null,
  "retry_count": 0
}
```

### New Fields in Gold Tier (vs Silver)

| Field | Type | Purpose | Example |
|-------|------|---------|---------|
| `workflow_id` | string | Link related actions | `wf-abc123` |
| `duration_ms` | integer | Execution time | `1250` |
| `mcp_server` | string | Which MCP handled this | `fte-odoo` |
| `retry_count` | integer | Number of retries | `0` |
| `error_message` | string | Error details (if failed) | `Connection refused` |
| `domain` | enum | Which domain | `odoo`, `facebook`, `instagram` |

### New Action Types (Gold Tier)

| Action Type | Source | Description |
|-------------|--------|-------------|
| `odoo_invoice_created` | fte-odoo | Invoice created in Odoo |
| `odoo_payment_recorded` | fte-odoo | Payment marked received |
| `odoo_expense_created` | fte-odoo | Expense recorded |
| `fb_post_created` | fte-facebook | Post published on Page |
| `fb_comment_replied` | fte-facebook | Reply to comment posted |
| `ig_post_published` | fte-instagram | Image/video published |
| `ig_reel_published` | fte-instagram | Reel published |
| `ig_comment_replied` | fte-instagram | Reply to IG comment |
| `ceo_briefing_generated` | scheduler | Weekly briefing created |
| `workflow_started` | workflow_engine | Cross-domain workflow began |
| `workflow_completed` | workflow_engine | Cross-domain workflow finished |
| `workflow_failed` | workflow_engine | Cross-domain workflow failed |
| `component_health_changed` | health_registry | Component status changed |
| `ralph_wiggum_iteration` | stop_hook | Loop iteration logged |

### Log Storage

**Location:** `AI_Employee_Vault/Logs/YYYY-MM-DD.json`

**Example:**
```
AI_Employee_Vault/
└── Logs/
    ├── 2026-03-05.json
    ├── 2026-03-06.json  ← Today's logs
    └── 2026-03-07.json
```

### Log Retention Policy

**Default:** 90 days

**Policy:**
- Scan `Logs/` directory daily
- Archive or delete files older than 90 days
- Dashboard shows disk usage warning if logs exceed threshold

> **Roman Urdu Example:**
> Har action ka detailed record rehta hai:
> - Kab hua? (timestamp)
> - Kya hua? (action_type)
> - Kaunse MCP se hua? (mcp_server)
> - Kis workflow ka part tha? (workflow_id)
> - Success hua ya error? (result, error_message)
> - Kitna time laga? (duration_ms)
> 
> Kal ko agar kuch galat hua → logs check karo → pata chal jayega kahan problem thi.

---

## SECTION 7: ERROR RECOVERY & GRACEFUL DEGRADATION

### Why Error Recovery Matters

**Autonomous systems must handle failures gracefully.**

Without error recovery:
- Odoo Docker stops → System crashes
- Meta API rate limit → All operations fail
- Network timeout → Workflow stuck

With error recovery:
- Odoo Docker stops → Queue tasks, continue other domains, retry when back
- Meta API rate limit → Pause FB/IG operations, continue Gmail/WhatsApp/Odoo
- Network timeout → Retry with exponential backoff

### Types of Errors

| Error Type | Examples | Recovery Strategy |
|------------|----------|-------------------|
| **Transient** | Network timeout, rate limit, temporary service down | Retry with exponential backoff |
| **Permanent** | Invalid credentials, permission denied, account banned | Alert owner, pause operations |
| **Critical** | Payment failures, data corruption | Never auto-retry, immediate alert |

### Exponential Backoff Retry

**Pattern:**
```
Attempt 1: Fail → Wait 1 second
Attempt 2: Fail → Wait 2 seconds
Attempt 3: Fail → Wait 4 seconds
Attempt 4: Give up, log error, alert owner
```

**Formula:** `delay = base_delay × (2 ^ attempt)`

**Implementation:**
```python
from src.utils.retry import retry_with_backoff

@retry_with_backoff(max_retries=3, base_delay=1)
def call_odoo_api():
    # May fail transiently
    pass
```

> **Note:** Payment/financial actions are **NEVER** auto-retried (FR-026).

### Component Health Registry

**Tracks health of all 5 domains:**

| Domain | Status Values | Trigger |
|--------|---------------|---------|
| Odoo | `healthy`, `degraded`, `down`, `unknown` | Based on consecutive failures |
| Facebook | `healthy`, `degraded`, `down`, `unknown` | Based on API responses |
| Instagram | `healthy`, `degraded`, `down`, `unknown` | Based on API responses |
| Gmail | `healthy`, `degraded`, `down`, `unknown` | Based on watcher status |
| WhatsApp | `healthy`, `degraded`, `down`, `unknown` | Based on watcher status |

**Status Transitions:**
```
0 failures → healthy
1-2 failures → degraded
3+ failures → down
```

**Storage:** `.state/health.json`

### Graceful Degradation Example

**Scenario:** Odoo Docker container stops unexpectedly

**System Behavior:**
1. Odoo MCP server detects connection refused
2. Logs error with `mcp_server: "fte-odoo"`, `error_message: "Connection refused"`
3. Updates component health: `odoo → down`
4. Creates notification file: `NOTIFICATION_odoo_down_TIMESTAMP.md`
5. **Continues processing** Gmail, WhatsApp, Facebook, Instagram tasks
6. Queues Odoo-related actions for retry
7. When Odoo restarts → health updates to `healthy` → queued actions process

> **Roman Urdu Example:**
> Agar Odoo band ho gaya → system crash nahi hota.
> Bas Odoo wala part pause ho jata hai, baaki sab chalta rehta hai.
> Jab Odoo wapis aaya → automatically resume.
> Jaise office mein agar accountant chhutti pe chala gaya → baaki kaam chalta rehta hai.


**Impact:**
- Invoice creation paused
- Payment recording paused
- CEO Briefing will note missing Odoo data

---

## SECTION 8: RALPH WIGGUM LOOP

### What is the Ralph Wiggum Loop?

**Ralph Wiggum Loop** enables **autonomous multi-step task completion**.

**Named after:** The Simpsons character known for persistence.

**Purpose:** Claude executes multiple steps **without stopping** for user input at each step.

### The Problem: Constant Stopping

Without Ralph Wiggum:
```
Task: "Process invoice request"

Step 1: Read email → ✅ Done
[Claude stops] "Should I continue?"
User: "Yes"

Step 2: Create Odoo invoice → ✅ Done
[Claude stops] "Should I continue?"
User: "Yes"

Step 3: Send email → ✅ Done
[Claude stops] "Should I continue?"
User: "Yes"

... This is tedious.
```

### The Solution: Ralph Wiggum Loop

With Ralph Wiggum:
```
Task: "Process invoice request"

Step 1: Read email → ✅ Done
Step 2: Create Odoo invoice → ✅ Done
Step 3: Send email (requires approval) → ⏳ Waiting for approval
[User approves]
Step 4: Post Facebook thank you → ✅ Done
Step 5: Update Dashboard → ✅ Done

[Task file moves to Done/]
[Loop exits]
```

### How It Works: Stop Hook Pattern

**Claude Code** has a **Stop hook** that fires when Claude thinks it's done.

**Hook Script:** `scripts/ralph-wiggum-check.sh`

**Logic:**
```bash
#!/bin/bash

# Check if task files exist in Tasks/
if [ "$(ls -A Tasks/)" ]; then
    echo "Tasks remaining!"
    exit 1  # Force Claude to continue
fi

# No tasks → allow stop
exit 0  # Claude can stop
```

**Exit Codes:**
- `exit 0` → Claude stops (task complete)
- `exit 1` → Claude continues (more work to do)

### Task File Structure

```markdown
---
type: ralph_wiggum_task
task: Process invoice request and notify client
status: in_progress
max_iterations: 10
current_iteration: 3
steps_total: 5
steps_completed: 2
---

# Task: Process Invoice Request

## Steps

- [x] Read client email and extract invoice details (completed 10:31)
- [x] Create invoice in Odoo via MCP (completed 10:32)
- [ ] Send invoice to client via email (REQUIRES APPROVAL)
- [ ] Post confirmation on Facebook Page
- [ ] Update Dashboard and log completion

## Context

Client: ABC Corp
Amount: PKR 50,000
Source: EMAIL_18d4a5b2.md
```

### Max Iterations Safety

**Default:** 10 iterations

**Purpose:** Prevent infinite loops

**Counter:** Stored in `/tmp/ralph-wiggum-counter`

**When max reached:**
```
Max iterations (10) reached. Stopping.
```

### Approval Steps in Ralph Wiggum Loop

**Important:** Approval-required steps still pause for human input:

```
Step 3: Send email → Requires approval
  ↓
Creates approval file in Needs_Action/
  ↓
[Loop continues, but waits at this step]
  ↓
User moves file to Approved/
  ↓
Loop resumes from Step 4
```

 ### Safety Mechanisms

 Ralph Wiggum Loop dangerous bhi ho sakta hai agar control na ho. Isliye:

 1. **Approval Gates** — Critical actions (payment, delete) mein approval chahiye
 2. **Max Steps Limit** — Infinite loop se bachne ke liye (e.g., MAX_STEPS = 10)
 3. **Error Handling** — Agar kuch galat ho toh stop karo aur user ko notify karo
 4. **Audit Logging** — Har step log karo (transparency ke liye)

 ### Example 1: Invoice Creation Workflow

**Scenario:** Client ka email aaya: "Invoice bhejo 50,000 ka"

```
Step 1: Parse email
          → Extract: client name, amount, details
          ↓
Step 2: Check Odoo (Customer exist karta hai?)
          → Try #1: Query customer by name/email
          → Not found ✗
          ↓
          → Try #2: Create new customer in Odoo
          → Created ✅
          ↓
Step 3: Create Invoice in Odoo
          → Product, Quantity, Price from Odoo product list
          → Invoice #123 created ✅
          ↓
Step 4: Send Invoice to Client
          → Email MCP → Client ko invoice bheja ✅
          ↓
Step 5: Post Thank You on Social Media
          → Facebook: Posted ✅
          → Instagram: Posted ✅
          ↓
Step 6: Notify Owner
          → WhatsApp: "Invoice bheja client ko" ✅
          ↓
Step 7: Audit Log
          → Har step record kiya ✅
          ↓
Done! 7 steps, 0 manual approvals (except critical payment)
 ```

> **Roman Urdu Example:**
> Sochnay aap ek order receive karte hain. Gold Tier pehle try karega Odoo mein invoice create karne ka.
> Agar success ho gaya, toh next step jayega. Agar fail ho gaya (shayad customer naya hai),
> toh pehle customer create karega, phir invoice banayega.
> Aur agar kuch bhi fail ho jaye, toh WhatsApp par aapko message bhej dega.
> Yeh sab automatically hoga!

### Example 2: Social Media Campaign

**Scenario:** Naya product launch hua, sab social media platforms par post karna hai.

```
Trigger: Product launch event
     ↓
Platform #1: Facebook
     → Try #1: Post via Facebook MCP
     → Check: Posted successfully?
     → Success ✅ → Move to next
     ↓ (or FAIL → Try again → Skip if fails)
Platform #2: Instagram
     → Try #1: Post via Instagram MCP (2-step: container + publish)
     → Check: Posted successfully?
     → Success ✅ → Move to next
     ↓
Platform #3: Twitter
     → Try #1: Post via Playwright
     → Check: Posted successfully?
     → Success ✅ → Move to next
     ↓
Platform #4: LinkedIn
     → Try #1: Post via Playwright
     → Check: Posted successfully?
     → Success ✅ → Done
     ↓
Summary: "Posted to all 4 platforms. Facebook: 1200 reach, Instagram: 800 impressions..."
 ```

> **Roman Urdu Example:**
> Jab aap naya product launch karte hain, Gold Tier automatically Facebook,
> Instagram, Twitter, aur LinkedIn par post kar dega.
> Lekin agar Facebook par post fail ho jaye (API issue), toh woh try karega.
> Agar dobara bhi fail ho, toh skip kar dega aur next platform (Instagram) try karega.
> Ye process tab tak chalega jab tak saare platforms try na ho jayein.

### Example 3: CEO Briefing Generation

**Scenario:** Weekly CEO briefing banani hai — har Sunday night.

```
Schedule: Sunday 11 PM (via APScheduler)
     ↓
Ralph Wiggum Loop START

Step #1: Collect Odoo Data
     → Try #1: Fetch from Odoo MCP
     → • Sales this week
     → • New customers
     → • Pending invoices
     → Check: Data fetched?
     → Success ✅
     ↓ (or FAIL → Use fallback/cached data)
Step #2: Collect Social Media Data
     → Facebook insights
     → Instagram metrics
     → Twitter analytics
     → LinkedIn statistics
     → Check: Data fetched?
     → Success ✅
     ↓ (or FAIL → Use partial data)
Step #3: Collect Communication Data
     → Gmail: emails processed
     → WhatsApp: messages handled
     ↓
Step #4: AI Analysis
     → Combine all data
     → Generate insights
     → Create report
     ↓
Step #5: Save and Send
     → Save to vault: Briefings/CEO_Briefing_2026-03-09.md
     → Send via Email MCP to CEO
     ↓
 > **Roman Urdu Example:**
> CEO Briefing ek weekly report hai jo business ki performance dikhata hai.
> Gold Tier automatically Odoo se sales data lega, social media se engagement metrics lega,
> aur AI se ek beautiful report banayega.
> Yeh report Sunday ko automatically generate hogi aur CEO ko email par bhej di jayegi.
> Aapko kuch nahi karna!
```
---

## SECTION 9: MULTIPLE MCP SERVERS ARCHITECTURE

### What are MCP Servers?

**MCP = Model Context Protocol** (Anthropic standard)

**Purpose:** Give Claude "hands" to interact with external systems.

**Analogy:**
```
Claude (Brain) → MCP Servers (Hands) → External APIs (Tools)
```

### MCP Servers in Gold Tier

| Server | Backend | Purpose |
|--------|---------|---------|
| `fte-email` | Gmail API (SMTP) | Send/receive emails |
| `fte-odoo` | Odoo JSON-RPC | Invoices, payments, expenses |
| `fte-facebook` | Meta Graph API | Facebook Page posting |
| `fte-instagram` | Meta Graph API | Instagram publishing |
| `fte-twitter` | Playwright (Browser) | Twitter/X posting |
| `fte-linkedin` | Playwright (Browser) | LinkedIn posting |

### MCP Server Architecture

```
┌─────────────────────────────────────────────────────────┐
│  Claude Code                                            │
│    ↓ Connects via stdio                                 │
│  MCP Protocol                                           │
│    ↓ Tool calls                                         │
│  MCP Server (Python)                                    │
│    ↓ HTTP calls / Browser automation                    │
│  External API (Odoo, Meta Graph, Gmail, Twitter, LinkedIn) │
└─────────────────────────────────────────────────────────┘
```

### Why Custom MCP Servers?

**Security First:** No third-party MCP servers.

| Approach | Pros | Cons |
|----------|------|------|
| **Custom MCP** (Gold Tier) | Full control, no secrets shared, audit logging | More development effort |
| Third-party MCP | Pre-built, quick setup | Security risk, secrets shared |

### MCP Server Registration

**.mcp.json:**
```json
{
  "mcpServers": {
    "fte-email": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/email_server.py"],
      "env": {}
    },
    "fte-odoo": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/odoo_server.py"],
      "env": {}
    },
    "fte-facebook": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/facebook_server.py"],
      "env": {}
    },
    "fte-instagram": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/instagram_server.py"],
      "env": {}
    },
    "fte-twitter": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/twitter_server.py"],
      "env": {}
    },
    "fte-linkedin": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/linkedin_server.py"],
      "env": {}
    }
  }
}
```

### MCP Tool Naming

Claude Code auto-namespaces tools:

```
fte-odoo.create_invoice     → mcp__fte-odoo__create_invoice
fte-facebook.create_page_post → mcp__fte-facebook__create_page_post
```

### MCP Server Health Check

Each MCP server's health is tracked:

```json
// .state/health.json
{
  "components": {
    "odoo": {
      "name": "Odoo (Docker)",
      "status": "healthy",
      "last_check": "2026-03-06T10:30:00Z",
      "consecutive_failures": 0
    },
    "facebook": {
      "name": "Facebook Graph API",
      "status": "healthy",
      "last_check": "2026-03-06T10:30:00Z",
      "consecutive_failures": 0
    }
  }
}
```

### Shared Meta Client

**File:** `src/mcp/_meta_client.py`

**Purpose:** Shared HTTP client for Facebook + Instagram (both use Meta Graph API).

**Avoids:** Code duplication.

**Methods:**
- `get(endpoint, params)` — GET request
- `post(endpoint, data)` — POST request
- Handles: Authentication, rate limits, token expiration

> **Roman Urdu Example:**
> 6 MCP servers hain — jaise 6 alag alag workers:
> - Email wala — Gmail handle karta hai
> - Odoo wala — Accounting handle karta hai
> - Facebook wala — Page posts handle karta hai
> - Instagram wala — Photos aur reels handle karta hai
> - Twitter wala — Tweets handle karta hai
> - LinkedIn wala — Professional posts handle karta hai
>
> Facebook + Instagram dono ek hi API use karte hain — Meta Graph API.
> Isliye ek shared client hai — `_meta_client.py`.
> Dono usko use karte hain — code repeat nahi hota.
> Twitter + LinkedIn dono Playwright use karte hain — browser automation se free mein kaam hota hai.

---

## SECTION 10: COMPLETE FLOW — PUTTING IT ALL TOGETHER

### End-to-End Example: Client Invoice Request

**Scenario:** Client emails: "Please send invoice for 5000 PKR"

#### Step 1: Gmail Watcher Detects Email

```
[Gmail Watcher]
  ↓ Polls Gmail API every 2 minutes
  ↓ New unread email detected
  ↓ Creates action file: EMAIL_18d4a5b2.md
  ↓ Saves to Needs_Action/
```

#### Step 2: Orchestrator Routes to Claude

```
[Orchestrator]
  ↓ Detects EMAIL_18d4a5b2.md in Needs_Action/
  ↓ Triggers Claude with action file content
```

#### Step 3: Claude Analyzes & Creates Plan

```
[Claude + Plan.md]
  ↓ Reads email content: "Please send invoice for 5000 PKR"
  ↓ Identifies intent: Invoice request
  ↓ Creates Plan.md:
    1. Extract invoice details (client, amount)
    2. Create invoice in Odoo
    3. Send invoice via email (requires approval)
    4. Notify on WhatsApp
    5. Log workflow
```

#### Step 4: Ralph Wiggum Loop Starts

```
[Ralph Wiggum Loop]
  ↓ Task file created: TASK_process_invoice_20260306.md
  ↓ Stop hook active
  ↓ Iteration 1 begins
```

> **How Multiple Tasks Work:**
>
> Agar ek waqt mein 3 Needs_Action files aayin — Claude har ek ke liye alag TASK file banata hai:
>
> ```
> Needs_Action/
> ├── EMAIL_18d4a5b2.md    → "Ahmed: Invoice bhejo 50,000"
> ├── EMAIL_29e5b6c3.md    → "Sara: Payment kar di"
> ├── WA_37f8c9d4.md       → "Ali: Meeting schedule karo"
>
> Claude reads Plan.md (ek baar) → samjhta hai rules
>     ↓
> Tasks/
> ├── TASK_invoice_ahmed_20260306.md      (Step 2/4 — chal raha hai)
> ├── TASK_payment_sara_20260306.md       (Step 1/3 — abhi start hua)
> ├── TASK_meeting_ali_20260306.md        (Step 0/2 — queue mein hai)
> ```
>
> Claude **ek waqt mein ek TASK** execute karta hai (sequentially):
> 1. Ahmed ka invoice TASK → sab steps done → Tasks/Done/ mein
> 2. Stop Hook: "Tasks/ mein aur file hai?" → HAI! → Continue
> 3. Sara ka payment TASK → sab steps done → Tasks/Done/ mein
> 4. Stop Hook: "Tasks/ mein aur file hai?" → HAI! → Continue
> 5. Ali ka meeting TASK → sab steps done → Tasks/Done/ mein
> 6. Stop Hook: "Tasks/ mein koi file?" → NAHI! → Claude ruk gaya

#### Step 5: Step 1 — Create Odoo Invoice

```
[Workflow Engine]
  ↓ workflow_id: wf-abc123
  ↓ Invokes fte-odoo MCP: create_invoice
  ↓ Odoo JSON-RPC: Create account.move
  ↓ Response: Invoice ID 42 created
  ↓ Audit log: odoo_invoice_created, workflow_id=wf-abc123
  ↓ Component health: odoo → healthy
```

#### Step 6: Step 2 — Send Email (Requires Approval)

```
[Workflow Engine]
  ↓ Creates approval file: APPROVAL_email_send_20260306.md
  ↓ Waits for user approval
  ↓ [User moves file to Approved/]
  ↓ Invokes fte-email MCP: send_email
  ↓ Gmail API: Email sent to client
  ↓ Audit log: email_sent, workflow_id=wf-abc123
```

#### Step 7: Step 3 — WhatsApp Notification

```
[Workflow Engine]
  ↓ Invokes fte-whatsapp MCP: send_message
  ↓ Playwright: WhatsApp message sent
  ↓ Audit log: whatsapp_sent, workflow_id=wf-abc123
```

#### Step 8: Step 4 — Facebook Thank You Post (Optional)

```
[Workflow Engine]
  ↓ Creates approval file: APPROVAL_fb_post_20260306.md
  ↓ [User approves]
  ↓ Invokes fte-facebook MCP: create_page_post
  ↓ Meta Graph API: Post published
  ↓ Audit log: fb_post_created, workflow_id=wf-abc123
```

#### Step 9: Step 5 — Update Dashboard

```
[Workflow Engine]
  ↓ Updates Dashboard.md
  ↓ Financial summary: +5000 PKR revenue
  ↓ Social media: +1 post
  ↓ Recent activity: Invoice sent to ABC Corp
```

#### Step 10: Task Complete

```
[Ralph Wiggum Loop]
  ↓ All steps completed
  ↓ Task file moves to Tasks/Done/
  ↓ Stop hook: exit 0 (allow Claude to stop)
  ↓ Workflow status: completed
```

### Complete Architecture Diagram-1

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         GOLD TIER ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐              │
│  │   Gmail      │    │   WhatsApp   │    │  File System │              │
│  │   Watcher    │    │   Watcher    │    │   Watcher    │              │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘              │
│         │                   │                   │                       │
│         └───────────────────┼───────────────────┘                       │
│                             │                                           │
│                             ↓                                           │
│                  ┌──────────────────┐                                   │
│                  │   Orchestrator   │                                   │
│                  │   + Workflow     │                                   │
│                  │     Engine       │                                   │
│                  └────────┬─────────┘                                   │
│                           │                                             │
│                           ↓                                             │
│                  ┌──────────────────┐                                   │
│                  │   Claude Code    │                                   │
│                  │   + Plan.md      │                                   │
│                  │   + Ralph        │                                   │
│                  │     Wiggum       │                                   │
│                  └────────┬─────────┘                                   │
│                           │                                             │
│         ┌─────────────────┼─────────────────┐                          │
│         │                 │                 │                          │
│         ↓                 ↓                 ↓                          │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐                  │
│  │ fte-email   │   │ fte-odoo    │   │ fte-facebook│                  │
│  │ MCP Server  │   │ MCP Server  │   │ MCP Server  │                  │
│  └──────┬──────┘   └──────┬──────┘   └──────┬──────┘                  │
│         │                 │                 │                          │
│         ↓                 ↓                 ↓                          │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐                  │
│  │ Gmail API   │   │ Odoo Docker │   │ Meta Graph  │                  │
│  │ (SMTP)      │   │ (JSON-RPC)  │   │ API         │                  │
│  └─────────────┘   └─────────────┘   └──────┬──────┘                  │
│                                             │                          │
│                                    ┌────────┴────────┐                 │
│                                    │  fte-instagram  │                 │
│                                    │  MCP Server     │                 │
│                                    └────────┬────────┘                 │
│                                             │                          │
│                                             ↓                          │
│                                    ┌─────────────┐                     │
│                                    │ Meta Graph  │                     │
│                                    │ API         │                     │
│                                    └─────────────┘                     │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────┐          │
│  │              Obsidian Vault (Memory)                     │          │
│  │  ├── Needs_Action/    ├── Done/         ├── Logs/        │          │
│  │  ├── Pending_Approval/├── Briefings/    ├── Tasks/       │          │
│  │  └── Dashboard.md     └── .state/health.json             │          │
│  └──────────────────────────────────────────────────────────┘          │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

 ### The Complete Gold Tier Architecture Diagram-2

 ```
 ┌──────────────────────────────────────────────────────────────────────┐
 │                         TRIGGERS                                     │
 ├──────────────────────────────────────────────────────────────────────┤
 │ • Scheduled tasks (CEO Briefing - Weekly)                           │
 │ • Email received (new order, customer query)                        │
 │ • Social media event (new follower, mention)                        │
 │ • Manual trigger (user asks for something)                          │
 │ • WhatsApp message received                                          │
 └──────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
 ┌──────────────────────────────────────────────────────────────────────┐
 │                     RALPH WIGGUM LOOP                                │
 │                    (Autonomous Orchestrator)                        │
 │  • Executes multi-step workflows                                    │
 │  • Handles errors and retries                                       │
 │  • Manages cross-domain coordination                                │
 └──────────────────────────────────────────────────────────────────────┘
                                     │
         ┌───────────────────────────┼───────────────────────────┐
         ▼                           ▼                           ▼
 ┌───────────────┐           ┌───────────────┐           ┌───────────────┐
 │   PERSONAL    │           │   BUSINESS    │           │    SOCIAL     │
 │   DOMAIN      │           │   DOMAIN      │           │    MEDIA      │
 ├───────────────┤           ├───────────────┤           ├───────────────┤
 │ • Gmail       │           │ • Odoo        │           │ • Facebook    │
 │ • WhatsApp    │           │   (Accounting)│           │   MCP         │
 │ • LinkedIn    │           │ • Invoices    │           │ • Instagram   │
 │               │           │ • Customers   │           │   MCP         │
 │               │           │               │           │ • Twitter    │
 │               │           │               │           │   (Playwright)│
 │               │           │               │           │ • LinkedIn   │
 │               │           │               │           │   (Playwright)│
 └───────────────┘           └───────────────┘           └───────────────┘
         │                           │                           │
         └───────────────────────────┼───────────────────────────┘
                                     ▼
 ┌──────────────────────────────────────────────────────────────────────┐
 │                     AUDIT LOGGING                                    │
 │                    (Every action recorded in JSON)                   │
 └──────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
 ┌──────────────────────────────────────────────────────────────────────┐
 │                     CEO BRIEFING                                      │
 │              (Weekly automated report - Sunday night)               │
 └──────────────────────────────────────────────────────────────────────┘
 ```

### Key Takeaways

1. **Cross-Domain:** One trigger → Multiple domain actions
2. **Autonomous:** Ralph Wiggum loop executes without constant input
3. **Safe:** HITL approval for all external actions
4. **Traceable:** Every action logged with workflow ID
5. **Resilient:** Error recovery, graceful degradation
6. **Intelligent:** CEO Briefing provides weekly insights

> **Roman Urdu Summary:**
> Gold Tier mein AI Employee ek mukammal autonomous employee ban jata hai:
> - Kaam khud samajhta hai (Claude + Plan.md)
> - Khud execute karta hai (Ralph Wiggum Loop)
> - Multiple domains ko connect karta hai (Cross-Domain Integration)
> - Har action ka record rakhta hai (Audit Logging)
> - Failures ko handle karta hai (Error Recovery)
> - Weekly report deta hai (CEO Briefing)
> 
> Bas yehi farq hai Silver aur Gold mein — Silver assistant tha, Gold employee hai.

---

# ═════════════════════════
# PART 2: IMPLEMENTATION (PROMPT-DRIVEN)
# ═════════════════════════

## SECTION 11: HOW IT WORKS — SPECKIT PLUS WORKFLOW

### The SpecKit Plus Approach

**You don't write code. You give prompts. Claude writes code.**

**Workflow:**
```
1. Read spec.md (What to build)
2. Read plan.md (How to build)
3. Give prompt to Claude Code
4. Claude implements
5. Verify with tests
6. Next prompt
```

### SpecKit Plus Files

All Gold Tier specifications are in:
```
specs/003-gold-fte-autonomous/
├── spec.md          # What to build (12 user stories)
├── plan.md          # How to build (phases, dependencies)
├── tasks.md         # Detailed task list
├── quickstart.md    # Setup guide
├── research.md      # Technology decisions
├── data-model.md    # Data structures
└── contracts/       # MCP server contracts
    ├── fte-odoo.md
    ├── fte-facebook.md
    └── fte-instagram.md
```

---

## SECTION 12: THE PROMPTS THAT BUILD GOLD TIER

### PROMPT 0 — Analyze Sources & Understand Context (MUST DO FIRST)

**Why this prompt is critical:**
Gold Tier Silver ke upar build hota hai. Agar Claude ko Silver ka architecture,
Hackathon-0 ke official requirements, aur existing codebase ki samajh nahi hogi —
toh specification galat banay ga. Yeh prompt Claude ko sab kuch padhne aur samajhne
ka mauka deta hai PEHLE spec banaye.

**Sources that Claude must analyze:**

| Source | Path | What It Contains |
|--------|------|------------------|
| Official Hackathon Documentation | `Personal-AI-Employee-Hackathon-0-Building-Autonomous-FTEs-in-2026.pdf` | Gold Tier requirements (Page 5) |
| Silver Tier Spec | `specs/002-silver-fte-foundation/spec.md` | Silver requirements, Gmail/WhatsApp watchers |
| Silver Tier Plan | `specs/002-silver-fte-foundation/plan.md` | Architecture decisions, MCP server design |
| Silver Tier Tasks | `specs/002-silver-fte-foundation/tasks.md` | Implementation details |
| Existing Codebase | `src/`, `AI_Employee_Vault/`, `.claude/skills/` | What's already built |
| Silver Tier Documentation | `Silver_Tier.md` | Complete Silver theory + implementation |

```
Go through the following sources carefully and analyze what Gold Tier requires:

1. Official Hackathon-0 documentation:
   @Personal-AI-Employee-Hackathon-0-Building-Autonomous-FTEs-in-2026.pdf
   Focus on Gold Tier requirements (Page 5) — what exactly needs to be built.

2. Silver Tier implementation (already working):
   - Read specs/002-silver-fte-foundation/spec.md (what Silver built)
   - Read specs/002-silver-fte-foundation/plan.md (architecture decisions)
   - Check existing code: src/, AI_Employee_Vault/, .claude/skills/
   - Read Silver_Tier.md for full architecture understanding

3. System prerequisites check:
   - Verify Docker, Docker Compose installed
   - Check if Meta Developer account is ready
   - Verify Silver Tier is fully working (pm2 status)

4. Report back:
   - What Gold Tier officially requires (from PDF)
   - What Silver already provides (foundation)
   - What new components need to be built
   - Any system prerequisites missing
   - Recommended implementation order

Do NOT generate any specs yet — just analyze and report.
```

**What Claude does after this prompt:**
- Reads the official PDF documentation (Gold Tier section)
- Reads all Silver Tier specs, plans, and existing code
- Checks system prerequisites (`docker --version`, etc.)
- Reports a complete analysis: what exists, what's needed, what's missing
- Aap review karein aur confirm karein to proceed

> **Roman Urdu Note:**
> Yeh sabse important step hai. Jaise koi naya employee hire ho toh pehle usko
> company ki documentation padhao, existing system samjhao, phir kaam do.
> Claude ko bhi pehle sab sources padhne do — phir spec banaye ga.
> Bina yeh step ke direct `/sp.specify` dena = bina naqsha safar karna.

---

### PROMPT 1 — Generate the Specification

**What this prompt does:**
Claude reads the Hackathon-0 documentation, analyzes Gold tier requirements,
and generates a complete specification document.

```
/sp.specify

Hackathon-0 Gold Tier: Autonomous Business Assistant — Extends Silver tier with:
1. Odoo Accounting Integration (Docker + JSON-RPC)
   - 6 tools: create_invoice, get_invoices, mark_payment_received,
     get_weekly_summary, get_expenses, create_expense
   - Self-hosted via Docker Compose

2. Facebook Business Page Integration (Meta Graph API)
   - 5 tools: create_page_post, get_page_posts, get_post_comments,
     reply_to_comment, get_page_insights
   - Requires Business Page (not personal profile)

3. Instagram Business/Creator Integration (Meta Graph API)
   - 6 tools: create_ig_post (2-step container), create_ig_reel (2-step),
     get_ig_media, get_ig_comments, reply_ig_comment, get_ig_insights
   - Requires Business/Creator account (not personal)

4. Cross-Domain Integration
   - Workflow engine linking Personal + Business domains
   - Example: Email received → Invoice created → Confirmation sent → Social post

5. CEO Briefing Generation
   - Weekly automated business intelligence report
   - Combines Odoo, Facebook, Instagram, and communication data

6. Audit Logging Enhancement
   - Track all AI actions with workflow IDs
   - Cross-domain transaction tracing

7. Error Recovery
   - Exponential backoff (1s, 2s, 4s)
   - Component health tracking

8. Ralph Wiggum Loop
   - Autonomous multi-step task execution
   - Max iteration limits to prevent infinite loops

Must maintain all Silver tier functionality (Gmail Watcher, WhatsApp Watcher, MCP Email).

```
### IMPLEMENTATION PROBLEMS & SOLUTIONS (During Build)

As you implement, you WILL face these problems. Here's how to solve them:

#### Problem A: MCP Server "failed" on Startup

```
fte-facebook · failed
fte-instagram · failed
fte-odoo · failed
```

**Cause:** `.mcp.json` uses `"command": "python"` but system has `python3`.

**Solution:**
```json
WRONG:  "command": "python",  "args": ["src/mcp/facebook_server.py"]
RIGHT:  "command": "uv",      "args": ["run", "python", "src/mcp/facebook_server.py"]
```

#### Problem B: "ModuleNotFoundError: No module named 'dotenv'"

**Cause:** Python dependencies not installed.

**Solution:**
```bash
uv sync
```

#### Problem C: "FB_PAGE_ACCESS_TOKEN not set in environment"

**Cause:** `.env` file missing or token not added.

**Solution:** Complete Meta API setup (see Section 15) and add tokens to `.env`:
```env
FB_PAGE_ID=1044367502088758
FB_PAGE_ACCESS_TOKEN=your_never_expiring_page_token
IG_USER_ID=17841477106514810
IG_ACCESS_TOKEN=your_60_day_token
META_API_VERSION=v25.0
```

#### Problem D: Instagram "Only photo or video can be accepted"

**Cause:** Image URL is redirecting or not a direct image link.

**Solution:** Use direct image URL (ends in .jpg or .png), not a webpage:
```
WRONG:  https://pixabay.com/photos/tree-sunset-736885/
RIGHT:  https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885_1280.jpg
```

#### Problem E: Instagram Container Timeout

**Cause:** Image processing taking too long (>60 seconds).

**Solution:**
- Check image size: max 8MB, recommended 1080x1080
- Use JPEG or PNG format

#### Problem F: OAuthException Code 190 (Token Expired)

**Cause:** Token expired or revoked.

**Solution:**
- **FB_PAGE_ACCESS_TOKEN:** Regenerate from Graph API Explorer (long-lived → Page token)
- **IG_ACCESS_TOKEN:** Exchange short-lived for 60-day token every ~50 days

#### Problem G: Twitter Playwright — Blank Page in Headless

**Cause:** Twitter blocks headless Chromium.

**Solution:** Use Firefox headless instead:
```python
# WRONG:
ctx = await pw.chromium.launch_persistent_context(headless=True)

# RIGHT:
ctx = await pw.firefox.launch_persistent_context(headless=True)
```

Or use dual-browser: Chromium for login, Firefox for headless, with cookie injection.

#### Problem H: Twitter Post Click Intercepted by Overlay

**Cause:** Cookie banner or notification popup covers Post button.

**Solution:** Use JavaScript click instead of Playwright click:
```python
# WRONG:
await post_btn.click()

# RIGHT:
await self._page.evaluate(
    'document.querySelector(\'button[data-testid="tweetButton"]\').click()'
)
```

#### Problem I: Settings.json Hook Format Error

```
Settings Error
hooks → Stop → 0 → hooks: Expected array, but received undefined
```

**Cause:** Old hook format in `.claude/settings.json`.

**Solution:** Use new format:
```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "./scripts/ralph-wiggum-check.sh"
          }
        ]
      }
    ]
  }
}
```

#### Problem J: "Could not log you in now" — Twitter Login Blocked

**Cause:** Twitter's bot detection blocks login in automated browsers.

**Solution:** Use "Sign up" flow instead of direct login — enter email in sign up,
Twitter detects existing account and redirects to login. This bypasses direct login
bot detection.

---

**What Claude generates:**
- `specs/003-gold-fte-autonomous/spec.md`
- User stories with acceptance criteria
- Functional requirements (FR-xxx)
- Success criteria (SC-xxx)
- Out of scope items (Platinum tier)

---

### PROMPT 2 — Generate the Plan

**What this prompt does:**
Claude reads the spec and generates the full architecture document — technology
decisions, file structure, component design, risk analysis.

```
/sp.plan
```

**What Claude generates:**
- `specs/003-gold-fte-autonomous/plan.md`
- Technology decisions:
  - `requests` library for HTTP calls (Odoo JSON-RPC + Meta Graph API)
  - `docker-compose` for Odoo + PostgreSQL
  - Meta Graph API v25.0 (March 2026)
  - FastMCP for Python MCP servers
- Component architecture for each MCP server
- Cross-domain workflow design
- Risk analysis (token expiry, rate limits, Docker resource usage)

---
### CRITICAL: PROBLEMS:

Before running the prompts below, READ these common problems and their solutions.
This will save you hours of debugging:

#### Problem 1: MCP Server Command — "python" vs "uv"

| Command | Will It Work? | Why? |
|---------|---------------|------|
| `"command": "python"` | **NO** | `python` command doesn't exist in WSL/Linux (only `python3`). Dependencies also missing. |
| `"command": "python3"` | **MAYBE** | Dependencies missing if not globally installed |
| `"command": "uv", "args": ["run", "python", ...]` | **YES** | `uv` manages virtual environment and dependencies automatically |

**Solution:** Always use `uv run python` in .mcp.json:
```json
"fte-odoo": {
  "type": "stdio",
  "command": "uv",
  "args": ["run", "python", "src/mcp/odoo_server.py"],
  "env": {}
}
```

#### Problem 2: Meta API — Two Different Page IDs

Facebook has **two different Page IDs**:

| ID Type | Example | Where Found | Works with API? |
|---------|---------|-------------|-----------------|
| URL ID (New Pages) | `61585031032595` | `facebook.com/profile.php?id=61585031032595` | **NO** |
| Business Portfolio ID | `1044367502088758` | `business.facebook.com/settings/` → Pages | **YES** |

**Solution:** Always use Business Portfolio Page ID. Get it from:
1. Go to `business.facebook.com/settings/`
2. Left side: **Accounts** → **Pages**
3. Click your Page — ID is shown there

#### Problem 3: Instagram 2-Step Posting Flow

Instagram posts require **two steps**:
```
Step 1: Create Container (upload media, get container_id)
Step 2: Publish Container (publish container, get media_id)
```

One-step approach does NOT work for Instagram!

#### Problem 4: Twitter Playwright — Chromium Headless Blocked

Twitter/X **blocks headless Chromium** with a blank page.
Solution: Use **Firefox headless** instead, or use dual-browser architecture:
- Chromium for login (non-headless)
- Firefox for headless operations
- Cookie injection between browsers

#### Problem 5: Token Expiration

| Token | Expires? | Renewal |
|-------|----------|---------|
| FB_PAGE_ACCESS_TOKEN (Page Token) | **Never** | One-time setup |
| IG_ACCESS_TOKEN (User Token) | **60 days** | Must renew every ~50 days |
| Twitter Cookies | **Varies** | Re-login when needed |

---

### PROMPT 3 — Generate the Tasks

**What this prompt does:**
Claude reads the plan and generates all implementation tasks — ordered, testable,
with clear acceptance criteria.

```
/sp.tasks
```

**What Claude generates:**
- `specs/003-gold-fte-autonomous/tasks.md`
- Phased implementation:
  - Phase 1: Docker + Odoo setup
  - Phase 2: Odoo MCP server (6 tools)
  - Phase 3: Meta Developer account + tokens
  - Phase 4: Facebook MCP server (5 tools)
  - Phase 5: Instagram MCP server (6 tools) — with 2-step container flow
  - Phase 6: Cross-domain workflow engine
  - Phase 7: CEO Briefing generator
  - Phase 8: Audit logging enhancement
  - Phase 9: Ralph Wiggum loop
  - Phase 10: Integration testing

---

### PROMPT 4 — Build Everything

**What this prompt does:**
Claude reads the tasks and implements them one by one — creating all files,
writing all code, running tests.

```
/sp.implement

Go through the tasks in specs/003-gold-fte-autonomous/tasks.md one by one.
Build the complete Gold tier:

1. Docker + Odoo Setup:
   - Create config/docker-compose.yml for Odoo + PostgreSQL
   - Test Odoo JSON-RPC connection

2. Odoo MCP Server:
   - Create src/mcp/odoo_server.py with 6 tools
   - Use JSON-RPC via requests library
   - Load credentials from .env: ODOO_URL, ODOO_DB, ODOO_USER, ODOO_PASSWORD

3. Meta API Setup:
   - Help user get Business Portfolio Page ID (NOT URL ID)
   - Generate long-lived user token → Page token
   - Store tokens in .env (never commit!)

4. Facebook MCP Server:
   - Create src/mcp/_meta_client.py (shared client with retry logic)
   - Create src/mcp/facebook_server.py with 5 tools
   - Use FB_PAGE_ACCESS_TOKEN from .env

5. Instagram MCP Server:
   - Create src/mcp/instagram_server.py with 6 tools
   - Implement 2-step container flow: create_media → publish_media
   - Use IG_ACCESS_TOKEN from .env
   - Verify account is Business/Creator type

6. Cross-Domain Workflow:
   - Create src/orchestrator/workflow_engine.py
   - Link email triggers → Odoo actions → email confirmations

7. CEO Briefing:
   - Create src/utils/ceo_briefing.py
   - Schedule via APScheduler (Sunday 22:00)

8. Ralph Wiggum Loop:
   - Create scripts/ralph-wiggum-check.sh
   - Configure in .claude/settings.json

Test each component before moving to next.
```

**What Claude does after this prompt:**
- Reads tasks.md
- Creates all files in order
- Runs tests for each component
- Reports progress and any blockers
- Aap verify karein aur confirm karein for next steps

---

---

## SECTION 13: MANUAL SETUP STEPS (Docker, Odoo, Meta API, MCP)

## FACEBOOK (STEP-BY-STEP)

### PART A: COMPLETE SETUP GUIDE

### Phase 1: Facebook Page Banana (5 minutes)

**Steps:**

1. **Facebook open karo** → Login karo (desktop use karo)

2. **Left sidebar** mein **"Pages"** click karo

3. **"+ Create New Page"** click karo

4. **Page details fill karo:**
   - **Page Name:** Jo bhi naam chahiye (e.g., "Agentive Solutions")
   - **Category:** Jo tumhare content se match kare (e.g., "Science & Tech")
   - **Bio:** Short description likho (optional)

5. **"Create Page"** click karo

6. **Profile picture aur cover photo** upload karo (optional, lekin recommended)

**Result:** Facebook Page ban gaya.

> **Roman Urdu Tip:**
> Page ka naam professional rakho — ye tumhara business face hai.
> "Agentive Solutions" jaisa naam accha hai — clear aur professional.

---

### Phase 2: Meta Developer Account Banana (10 minutes)

**Step 1 — Developer Portal Pe Jao:**

1. Browser open karo (Desktop use karo)
2. URL: **developers.facebook.com**
3. Facebook account se automatically login ho jayega
4. **"Get Started"** ya **"My Apps"** click karo
5. Developer terms accept karo

**Step 2 — New App Create Karo:**

1. **"Create App"** button click karo
2. **App name** likho → e.g., `FTE Social Manager`
3. **Contact email** confirm karo (tumhara email)
4. **"Next"** click karo

**Step 3 — Use Case Select Karo:**

1. **"Other"** select karo
2. **"Next"** click karo
3. App type: **"Business"** select karo (**NOT** Consumer)
4. **"Next"** click karo

**Step 4 — App Details:**

1. **App Name:** `FTE Social Manager` (ya jo naam choose kiya)
2. **Contact Email:** tumhara email
3. **Business Account:** Skip ya "No Business Manager"
4. **"Create App"** click karo
5. Password confirm karo

**Result:** Developer App ban gaya — **App ID** aur **App Secret** milte hain.

**Step 5 — Facebook Login Product Add Karo:**

1. App Dashboard → left side **"Add Product"**
2. **"Facebook Login for Business"** add karo → **"Set Up"** click karo

**Step 6 — Permissions Check Karo:**

1. Left side: **"App Review"** → **"Permissions and Features"**
2. Ye permissions search karo — sab **"Ready to use"** honi chahiye:

| Permission | Purpose | Status Needed |
|---|---|---|
| `pages_manage_posts` | Page pe post karna | Ready to use |
| `pages_read_engagement` | Comments padhna | Ready to use |
| `pages_read_user_content` | Page content padhna | Ready to use |
| `pages_manage_engagement` | Comments reply karna | Ready to use |
| `pages_show_list` | Pages ki list dekhna | Ready to use |

**Note:** Development mode mein ye sab permissions bina App Review ke kaam karti hain (sirf tumhare account pe).

---

### Phase 3: Business Portfolio Se App Connect Karna (IMPORTANT — 5 minutes)

> **⚠️ CRITICAL STEP:** Agar tumhara Facebook Page "New Pages Experience" pe hai (jo 2024+ mein default hai), toh Page **Business Portfolio** ke through managed hota hai. Is case mein normal `me/accounts` API call empty data return karti hai.

**Problem Jo Hum Ne Face Ki:**
- Graph API Explorer mein `me/accounts` empty `{"data": []}` return karta tha
- Direct Page ID se query karne pe "does not exist or missing permissions" error aata tha
- Token generate hota tha lekin Page access nahi milta tha

**Solution — Step by Step:**

**Part A: Business Portfolio Settings Kholna**

1. Browser mein jao: **business.facebook.com/settings/**
2. **"Select business"** page khulega — agar multiple Business Portfolios hain toh wo wala select karo jismein Pages hain (e.g., "Bangash110 · 2 Pages · 2 People")

**Part B: Page Ko Business Portfolio Mein Add Karna**

> **⚠️ NOTE:** Agar Pages section mein tumhara Page already dikh raha hai toh ye step skip karo aur Part C pe jao.

1. Left side mein **"Accounts"** → **"Pages"** click karo
2. Agar Page nahi dikh raha toh **"+ Add"** click karo
3. **"Add an existing Facebook Page"** select karo (pehla option)
4. Apna Page search karo (e.g., "Agentive Solutions")
5. Page select karo → **"Next"** click karo
6. Agar Instagram connected hai toh Instagram login popup aayega — login karo
   - **Agar "Invalid redirect URI" error aaye** toh pehle ye karo:
     - **developers.facebook.com** → Apna App → **"Facebook Login for Business"** → **"Settings"**
     - **"Valid OAuth Redirect URIs"** mein `https://business.facebook.com/` add karo
     - **Save** karo → Phir wapis yahan aake dobara try karo
7. **"Request approval"** step aayega → Complete karo
8. Page add ho jayega — **Page ID** bhi dikhegi (ye number note karo — API ke liye chahiye)

**Part C: App Ko Business Portfolio Se Connect Karna**

1. Left side mein **"Accounts"** → **"Apps"** click karo
2. **"+ Add"** click karo
3. Apna **App ID** paste karo (developers.facebook.com → App Dashboard → **"App settings"** → **"Basic"** se copy karo)
4. App add ho jayegi

**Part D: Page Ko App Se Connect Karna**

1. Left side mein **"Pages"** click karo
2. Apna **Page** select karo (e.g., "Agentive Solutions")
3. **"Connected assets"** tab pe jao
4. **"Connect assets"** click karo
5. Apna App select karo (e.g., "FTE Social Manager")

**Result:** Page + App + Instagram sab Business Portfolio se connected. Page ID bhi mil gayi.

---

### Phase 4: Page Access Token Generate Karna (10 minutes)

> **⚠️ CRITICAL: Do Tarah Ki Page IDs**
>
> New Pages Experience mein **do different IDs** hoti hain:

| ID Type | Example | Kahan Milti Hai |
|---|---|---|
| New Pages Experience ID | `61585031032595` | Facebook URL bar mein |
| Business Portfolio Page ID | `1044367502088758` | Business Settings → Pages mein |

**API ke liye Business Portfolio Page ID use karo!**

**Token Generate Karne Ka Correct Method:**

1. Jao: **developers.facebook.com/tools/explorer/**
2. **Meta App:** Apna App select karo (e.g., "FTE Social Manager")
3. **User or Page:** User Token rakho
4. **Permissions** add karo:
   - `pages_show_list`
   - `pages_read_engagement`
   - `pages_read_user_content`
   - `pages_manage_posts`
   - `pages_manage_engagement`
5. **"Generate Access Token"** click karo
6. Popup mein:
   - "Continue as [Name]" click karo
   - Sab permissions allow karo
   - **Apna Page select karo** (checkbox ON)
   - Save/Done click karo

**Page Token Nikalna:**

1. **GET** mode mein (POST nahi!) URL likho:
```
{YOUR_PAGE_ID}?fields=access_token
```
(Example: `1044367502088758?fields=access_token`)

2. Submit karo

3. Response mein **access_token** aayega — ye **Page Access Token** hai

4. Ye token copy karo — isse posting ke liye use hoga

---

### Phase 5: Facebook Page Pe Post Karna (API Test — 5 minutes)

**Working Method:**

1. Graph API Explorer mein **GET** mode mein:
```
{YOUR_PAGE_ID}?fields=access_token
```
2. Submit karo — Page token milega

3. **Access Token field mein Page token paste karo** (purana User token replace karo)

4. **POST** mode select karo

5. URL mein likho:
```
{YOUR_PAGE_ID}/feed?message=Test post from API
```

6. Submit karo

**Expected Success Response:**
```json
{
  "id": "1044367502088758_122094486825167701"
}
```

**Ye post ID hai — iska matlab POST SUCCESSFUL!**

**Verify:**
- Facebook pe apna Page kholo
- "Test post from API" post dikhni chahiye

---

### Phase 6: Long-Lived Tokens Banana (Production Ke Liye ZAROORI — 10 minutes)

> **Kyun Zaroori Hai?**
>
> Graph API Explorer se jo token milta hai wo **1-2 ghante** mein expire ho jata hai. Production/automation ke liye **long-lived tokens** chahiye.

| Token Type | Expiry | Kiske Liye |
|---|---|---|
| Short-lived User Token | 1-2 hours | Graph Explorer testing |
| **Long-lived User Token** | **60 days** | Instagram automation |
| **Long-lived Page Token** | **Never expires** | **Facebook automation** |

**Step 1: App Secret Nikalo**

1. **developers.facebook.com** → **My Apps** → Apna App
2. Left side: **"App settings"** → **"Basic"**
3. **"App Secret"** ke saamne **"Show"** click karo
4. Password daalo agar puche
5. **App Secret copy** karo — ye safe rakho, kisi ko mat batao

**Step 2: Long-Lived User Token Banao (60 days)**

1. Graph API Explorer mein **"User or Page"** → **"Get User Access Token"** select karo
2. Ye permissions add karo:
   - `pages_show_list`
   - `pages_read_engagement`
   - `pages_manage_posts`
   - `pages_manage_engagement`
3. **"Generate Access Token"** click karo — sab allow karo + Page select karo
4. Ye **short-lived User Token** hai — isse copy karo

5. **Naye browser tab** mein ye URL paste karo:

```
https://graph.facebook.com/v25.0/oauth/access_token?grant_type=fb_exchange_token&client_id={APP_ID}&client_secret={APP_SECRET}&fb_exchange_token={SHORT_LIVED_TOKEN}
```

6. **Replace karo:**
   - `{APP_ID}` → Apna App ID
   - `{APP_SECRET}` → App Secret (Step 1 se)
   - `{SHORT_LIVED_TOKEN}` → Graph Explorer ka short-lived token (Step 4 se)

7. **Enter** press karo

8. Response aayega:
```json
{
  "access_token": "EAAxxxxxxx_BOHOT_LAMBA_TOKEN_xxxxxxx",
  "token_type": "bearer",
  "expires_in": 5184000
}
```

9. `expires_in: 5184000` = **60 din** — ye confirm karta hai ke long-lived token ban gaya

10. **Ye token copy karo** — ye tumhara **IG_ACCESS_TOKEN** hai (Instagram ke liye use hoga)

**Step 3: Never-Expiring Page Token Banao (Facebook ke liye)**

1. Step 2 ka **long-lived User Token** Graph API Explorer ke **Access Token** field mein paste karo

2. **GET** mode mein ye likho:
```
{YOUR_PAGE_ID}?fields=access_token
```

3. **Submit** karo

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

> **Kyun Never-Expiring?**
>
> Jab long-lived User Token (60 days) se Page Token nikaalte ho toh wo **kabhi expire nahi hota** — ye Meta ki official documentation mein confirmed hai.

---

## PART B: MCP SERVER INTEGRATION

### Facebook MCP Server Tools

The `fte-facebook` MCP server exposes 5 tools:

| Tool | Purpose | Example |
|------|---------|---------|
| `create_page_post` | Post on Facebook Page | New project announcement |
| `get_page_posts` | List recent posts | Saare posts dikhao |
| `get_post_comments` | Read comments | Is post pe comments kya hain |
| `reply_to_comment` | Reply to comment | Client ke comment ka jawab |
| `get_page_insights` | Analytics | Reach, engagement, followers |

### Facebook API Endpoints

| Action | HTTP Method | Endpoint |
|--------|-------------|----------|
| Create Post | POST | `/{page-id}/feed` |
| Get Posts | GET | `/{page-id}/feed` |
| Get Comments | GET | `/{post-id}/comments` |
| Reply to Comment | POST | `/{comment-id}/comments` |
| Get Insights | GET | `/{page-id}/insights` |

### Rate Limits

- **Facebook Pages:** ~4800 calls per Page per 24 hours
- **Posting:** No hard limit (reasonable use)


## INSTAGRAM BUSINESS ACCOUNT INTEGRATION (STEP-BY-STEP)

### PART A: COMPLETE SETUP GUIDE 

### Phase 1: Instagram Creator Account Banana (5 minutes)

> **Important:** Instagram account ko **Business** ya **Creator** mein convert karna **mandatory** hai. Personal account pe API kaam nahi karta.

**Steps:**

1. **Instagram App** open karo phone pe

2. Apni **Profile** pe jao (bottom right corner)

3. **Hamburger menu** (three lines) tap karo — top right

4. **"Settings and privacy"** tap karo

5. Scroll down → **"Account type and tools"** tap karo

6. **"Switch to professional account"** tap karo

7. **"Creator"** select karo (Business nahi, Creator recommended)
   - **Creator:** Influencers, content creators ke liye
   - **Business:** Brands, shops ke liye

8. **Category choose karo** (e.g., "Digital Creator", "Blogger", "Science & Tech")

9. Contact info add karo ya **"Don't use my contact info"** select karo

10. **"Done"** tap karo

**Result:** Instagram Creator account ready.

### Creator vs Business vs Personal:

| Feature | Personal | Creator | Business |
|---|---|---|---|
| API access | ❌ NO | ✅ YES | ✅ YES |
| Insights/Analytics | ❌ No | ✅ Yes | ✅ Yes |
| Contact button | ❌ No | ✅ Yes | ✅ Yes |
| Facebook Page connect | ❌ No | ✅ YES | ✅ YES |
| Best for | Normal use | Influencers, content creators | Brands, shops |

**Recommendation:** **Creator account lo** — API access milta hai aur profile personal jaisi dikhti hai.

---

### Phase 2: Instagram Ko Facebook Page Se Connect Karna (5 minutes)

> **Important:** Instagram API Facebook ke through kaam karta hai — Page connection zaroori hai.
>
> **⚠️ NOTE:** Purane guides mein likha hai "Edit Profile → Page option" — ye ab kaam NAHI karta.
> 2025+ mein Instagram ne ye option hata diya hai. Ab connection **Meta Accounts Center** se hoti hai.

**Method 1 — Meta Accounts Center se (RECOMMENDED — Desktop pe karo):**

1. **Facebook** open karo desktop pe

2. Apna **Facebook Page** pe jao (e.g., "Agentive Solutions")

3. **Page Settings** mein jao

4. **"Linked Accounts"** ya **"Instagram"** dhundo

5. **"Connect Account"** click karo

6. Instagram credentials daalo (username + password)

7. **"Connect"** click karo

**Method 2 — Meta Accounts Center Direct:**

1. Browser mein jao: **accountscenter.facebook.com**

2. Ya Facebook → Settings → **"Accounts Center"** (top mein dikhta hai)

3. **"Accounts"** click karo

4. **"Add accounts"** click karo

5. **Instagram** select karo

6. Instagram credentials daalo

7. Connect karo

**Method 3 — Instagram Settings se (Phone pe):**

1. **Instagram App** open karo phone pe

2. **Settings** → **"Accounts Center"** (top mein, Meta logo ke saath)

3. **"Accounts"** tap karo

4. **"Add accounts"** → Facebook add karo

5. Facebook login karo aur Page select karo

**Verify:**

1. **Facebook Page Settings** → **"Linked Accounts"** → Instagram dikhna chahiye
2. Ya **Graph API Explorer** mein: `{YOUR_PAGE_ID}?fields=instagram_business_account` — agar ID aaye toh connected hai

**Result:** Instagram aur Facebook Page connected.

---

### Phase 3: Instagram Product Add Karna (Developer App mein — 5 minutes)

**Step 1 — Instagram Product Add Karo:**

1. **developers.facebook.com** → **My Apps** → Apna App (e.g., "FTE Social Manager")

2. App Dashboard → left side **"Add Product"**

3. **"Instagram"** add karo → **"Set Up"** click karo

**Step 2 — Instagram Tester Role Add Karna:**

1. Left side: **"App roles"** → **"Roles"**

2. **"Instagram Testers"** tab click karo

3. **"Add People"** click karo

4. **"Instagram Tester"** role select karo

5. Instagram username type karo: `{your_instagram_username}`

6. **"Add"** click karo

**Step 3 — Instagram Se Invite Accept Karo:**

1. **Instagram App** open karo phone pe

2. **Settings and privacy** → **"Apps and Websites"**

3. **"Tester Invites"** tab mein **"FTE Social Manager-IG"** dikhega

4. Click karo aur **"Accept"** karo

**Step 4 — Instagram Permissions Add Karo:**

1. Browser mein jao: **developers.facebook.com/tools/explorer/**
2. **"Meta App"** dropdown mein apna App select karo (e.g., "FTE Social Manager")
3. **"User or Page"** mein **"Get User Access Token"** select karo
4. **"Permissions"** mein ye add karo:
   - `instagram_basic`
   - `instagram_content_publish`
   - `instagram_manage_comments`
   - `instagram_manage_insights`

5. **"Generate Access Token"** click karo aur sab allow karo

---

### Phase 4: Instagram Business Account ID Nikalna (5 minutes)

**Pehle: Page ID Kahan Se Milegi?**

> **⚠️ IMPORTANT:** Facebook mein **2 tarah ki Page IDs** hoti hain. API ke liye sirf **Business Portfolio Page ID** kaam karti hai.
>
> | ID Type | Example | API mein kaam? |
> |---|---|---|
> | URL ID (browser bar mein) | `61583573918121` | ❌ NAHI |
> | **Business Portfolio Page ID** | `1044367502088758` | ✅ HAAN |

**Business Portfolio Page ID nikalne ka tareeqa:**

1. Browser mein jao: **business.facebook.com/settings/**
2. **"Select business"** page khulega — agar multiple Business Portfolios hain toh wo wala select karo jismein tumhare Pages hain (e.g., jo "2 Pages" dikhaye)
3. Business Settings khulne ke baad, left side mein **"Pages"** click karo
4. Apna Page dikhega (e.g., "Agentive Solutions") — Page ke saath **numeric Page ID** dikhegi
5. **Ye ID copy karo** — yehi API ke liye use hogi

> **⚠️ NOTE:** `me/accounts` Graph API Explorer mein try mat karo — New Pages Experience mein ye empty `{"data": []}` return karta hai. Business Settings se Page ID nikalna sabse reliable tareeqa hai.

**Ab Instagram Business Account ID Nikalo:**

1. Graph API Explorer mein **GET** mode mein:
```
{YOUR_PAGE_ID}?fields=instagram_business_account
```
(Example: `1044367502088758?fields=instagram_business_account`)

2. **Submit** karo

3. Response aayega:
```json
{
  "instagram_business_account": {
    "id": "17841477106514810"
  },
  "id": "1044367502088758"
}
```

4. **Instagram Business Account ID:** `17841477106514810` — ye copy karo

---

### Phase 5: Instagram Pe Post Karna (2-Step Process — 10 minutes)

> **Important:** Instagram pe posting **2 steps** mein hoti hai (Facebook se different).

**Step 1: Media Container Banao**

1. Graph API Explorer mein **POST** mode select karo

2. URL: `{IG_ACCOUNT_ID}/media`
   (Example: `17841477106514810/media`)

3. **Parameters add karo** ("Add parameter" button use karo):
   - Parameter 1: `image_url` = `https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885_1280.jpg`
   - Parameter 2: `caption` = `Hello from FTE Social Manager!`

> **⚠️ IMPORTANT:** Parameters ko URL mein mat likho. "Add parameter" button use karke separately add karo. Warna "Only photo or video can be accepted" error aayega.

4. **Submit** karo

5. Response:
```json
{
  "id": "17869164552570218"
}
```

6. **Ye `creation_id` hai** — copy karo

**Step 2: Publish Karo**

1. Graph API Explorer mein **POST** mode mein raho

2. URL: `{IG_ACCOUNT_ID}/media_publish`
   (Example: `17841477106514810/media_publish`)

3. **Parameter add karo:**
   - `creation_id` = `17869164552570218` (Step 1 se mili ID)

4. **Submit** karo

5. Response:
```json
{
  "id": "18194284255350604"
}
```

6. **Ye `media_id` hai** — post successful!

**Verify:**
- Instagram pe apni profile kholo
- Photo aur caption dikh jayega

---

### Phase 6: Instagram Ke Liye Long-Lived Token (60 days)

> **Note:** Instagram ke liye **User Token** use hota hai (Page Token nahi).

**Steps:**

1. Graph API Explorer mein **"User or Page"** → **"Get User Access Token"** select karo

2. Ye permissions add karo:
   - `instagram_basic`
   - `instagram_content_publish`
   - `instagram_manage_comments`
   - `instagram_manage_insights`

3. **"Generate Access Token"** click karo — sab allow karo

4. Ye **short-lived User Token** hai (1-2 hours) — isse copy karo

5. **Naye browser tab** mein ye URL paste karo:

```
https://graph.facebook.com/v25.0/oauth/access_token?grant_type=fb_exchange_token&client_id={APP_ID}&client_secret={APP_SECRET}&fb_exchange_token={SHORT_LIVED_TOKEN}
```

6. **Replace karo:**
   - `{APP_ID}` → Apna App ID
   - `{APP_SECRET}` → App Secret
   - `{SHORT_LIVED_TOKEN}` → Graph Explorer ka short-lived token

7. **Enter** press karo

8. Response:
```json
{
  "access_token": "EAAxxxxxxx_BOHOT_LAMBA_TOKEN_xxxxxxx",
  "token_type": "bearer",
  "expires_in": 5184000
}
```

9. `expires_in: 5184000` = **60 din**

10. **Ye token copy karo** — ye tumhara **IG_ACCESS_TOKEN** hai

11. `.env` file mein save karo:
```env
# Instagram — 60-day User Token (renew every 50 days)
IG_ACCESS_TOKEN=EAAxxxxxxx_USER_TOKEN_xxxxxxx
```

**Token Renewal Reminder:**

| Token | Expiry | Kab Renew Karein |
|---|---|---|
| **IG_ACCESS_TOKEN** | 60 days | Har 50 din mein (10 din pehle) |

---

## PART B: MCP SERVER INTEGRATION

### Instagram Content Publishing API

Instagram uses a **2-step container flow**:

```
Step 1: Create Media Container
  POST /{ig-user-id}/media
  Params: image_url, caption, media_type
  Response: creation_id

Step 2: Publish Container
  POST /{ig-user-id}/media_publish
  Params: creation_id
  Response: media_id (post is live!)
```

> **Why 2 steps?** Instagram needs to process the image/video before publishing.

### Instagram MCP Server Tools

The `fte-instagram` MCP server exposes 6 tools:

| Tool | Purpose | Example |
|------|---------|---------|
| `create_ig_post` | Publish image post | Project completion photo |
| `create_ig_reel` | Publish reel | Short video demo |
| `get_ig_media` | List recent posts | Saare posts dikhao |
| `get_ig_comments` | Read comments | Comments kya hain |
| `reply_ig_comment` | Reply to comment | Client ko jawab |
| `get_ig_insights` | Analytics | Reach, impressions, followers |

### Instagram Rate Limits

| Action | Limit |
|--------|-------|
| Posts per day | **25** (hard limit) |
| API calls per hour | 200 per user |

> **Note:** 25 posts/day is generous for most use cases. Track in audit logs.


### Step 1: Docker + Odoo Setup

```bash
# Verify Docker
docker --version
docker compose version

# Start Odoo
docker compose -f config/docker-compose.yml up -d

# Wait 30 seconds, then access
# http://localhost:8069

# Create database: fte_gold
# Install: Invoicing + Expenses modules
```

**Update .env:**
```bash
ODOO_URL=http://localhost:8069
ODOO_DB=fte_gold
ODOO_USER=admin
ODOO_PASSWORD=your_password
```

---

### Step 2: Meta Developer Setup

**2.1 Create Facebook Business Page**
1. facebook.com → Create → Page
2. Name: "Agentive Solutions"
3. Note Page ID

**2.2 Convert Instagram to Business/Creator**
1. Instagram Settings → Account
2. "Switch to Professional Account"
3. Choose Business or Creator
4. Connect to Facebook Page
5. Note Instagram Account ID

**2.3 Create Meta Developer Account**
1. developers.facebook.com
2. Create App → Business Type
3. Add Products → Facebook Login
4. Request permissions:
   - pages_manage_posts
   - pages_read_engagement
   - pages_show_list
   - instagram_basic
   - instagram_content_publish

**2.4 Get Non-Expiring Page Token**
```bash
# Step 1: Get short-lived user token from Graph API Explorer
# https://developers.facebook.com/tools/explorer/
# Add permissions: pages_show_list, pages_read_engagement, pages_manage_posts, pages_manage_engagement

# Step 2: Exchange for long-lived user token (60 days)
curl "https://graph.facebook.com/v25.0/oauth/access_token?\
grant_type=fb_exchange_token&\
client_id=YOUR_APP_ID&\
client_secret=YOUR_APP_SECRET&\
fb_exchange_token=YOUR_SHORT_LIVED_TOKEN"

# Step 3: Get never-expiring Page token
# NOTE: Use YOUR_PAGE_ID (Business Portfolio ID), NOT me/accounts
# (me/accounts returns empty for New Pages Experience)
curl "https://graph.facebook.com/v25.0/YOUR_PAGE_ID?\
fields=access_token&\
access_token=YOUR_LONG_LIVED_USER_TOKEN"
```

**Update .env:**
```bash
# Facebook (never-expiring Page Token)
FB_PAGE_ID=your_business_portfolio_page_id
FB_PAGE_ACCESS_TOKEN=your_non_expiring_page_token

# Instagram (60-day User Token — renew every 50 days)
IG_USER_ID=your_ig_account_id
IG_ACCESS_TOKEN=your_60_day_user_token

# Meta API version
META_API_VERSION=v25.0

# Twitter/X (Playwright — browser cookies handle auth)
# No API keys needed — Playwright uses browser session
TWITTER_SESSION_PATH=~/.twitter-session/

# LinkedIn (Playwright — browser cookies handle auth)
# No API keys needed — Playwright uses browser session
LINKEDIN_SESSION_PATH=~/.linkedin-session/
```

---

### Step 3: Register MCP Servers

**Update .mcp.json:**
```json
{
  "mcpServers": {
    "fte-email": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/email_server.py"],
      "env": {}
    },
    "fte-odoo": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/odoo_server.py"],
      "env": {}
    },
    "fte-facebook": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/facebook_server.py"],
      "env": {}
    },
    "fte-instagram": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "src/mcp/instagram_server.py"],
      "env": {}
    }
  }
}
```

---

### Step 4: Test Components

```bash
# Test Odoo MCP
uv run python src/mcp/odoo_server.py

# Test Facebook MCP
uv run python src/mcp/facebook_server.py

# Test Instagram MCP
uv run python src/mcp/instagram_server.py

# Test CEO Briefing (manual)
uv run python -m src.main briefing
```

---

## SECTION 14: TESTING & VERIFICATION

### Odoo Test
```bash
# Ensure Odoo Docker is running
docker compose -f config/docker-compose.yml ps

# In Claude Code:
@mcp__fte-odoo__create_invoice
{
  "partner_name": "Test Client",
  "lines": [
    {"description": "Test Service", "price_unit": 5000}
  ]
}

# Verify in Odoo web UI: http://localhost:8069
```

### Facebook Test
```bash
# In Claude Code:
@mcp__fte-facebook__create_page_post
{
  "message": "Test post from Gold Tier!"
}

# Verify on Facebook Page
```

### Instagram Test
```bash
# In Claude Code:
@mcp__fte-instagram__create_ig_post
{
  "image_url": "https://example.com/test.jpg",
  "caption": "Test post from Gold Tier!"
}

# Verify on Instagram
```

### Cross-Domain Test
```bash
# Send email to yourself: "Please send invoice for 5000 PKR"
# Wait for Gmail Watcher (2 min poll)
# Check vault: EMAIL_*.md created
# Verify: Odoo invoice created, email reply sent, WhatsApp notification

# Check audit logs:
cat AI_Employee_Vault/Logs/$(date +%Y-%m-%d).json | jq '.[] | select(.workflow_id != null)'
```

### CEO Briefing Test
```bash
# Manual trigger
python -m src.main briefing

# Check output:
cat AI_Employee_Vault/Briefings/CEO_Briefing_*.md
```

### Ralph Wiggum Test
```bash
# Create task file:
cat > AI_Employee_Vault/Tasks/TASK_test_20260306.md << 'EOF'
---
type: ralph_wiggum_task
task: Test Ralph Wiggum Loop
status: pending
max_iterations: 5
current_iteration: 0
steps_total: 3
steps_completed: 0
---

# Task: Test Ralph Wiggum

## Steps
- [ ] Read test file
- [ ] Create dummy action
- [ ] Mark complete
EOF

# Start Claude Code
# Watch it execute all steps autonomously
# Verify task file moves to Done/
```

---

## SECTION 15: TROUBLESHOOTING

### Common Issues

| Issue | Solution |
|-------|----------|
| Odoo Docker won't start | Check Docker: `docker ps`. Check ports: `netstat -tlnp \| grep 8069` |
| Odoo MCP connection refused | Verify ODOO_URL in .env. Check Docker: `docker compose ps` |
| Facebook token expired | Page tokens from long-lived user tokens don't expire. Re-check generation steps |
| Instagram "not Business/Creator" | Convert: Instagram Settings → Account → Switch to Professional |
| Instagram 25-post limit | Wait 24 hours. Track in audit logs |
| Ralph Wiggum infinite loop | Check max_iterations. Verify script is executable |
| MCP server not found | Restart Claude Code after updating .mcp.json |
| CEO Briefing missing data | Check .state/health.json. Ensure all services running |

---

# ═════════════════════════
# APPENDIX
# ═════════════════════════

## APPENDIX A: COMMAND REFERENCE

```bash
# Start Odoo
docker compose -f config/docker-compose.yml up -d

# Stop Odoo
docker compose -f config/docker-compose.yml down

# Check Odoo status
docker compose -f config/docker-compose.yml ps

# View Odoo logs
docker compose -f config/docker-compose.yml logs -f odoo

# Test MCP servers
uv run python src/mcp/odoo_server.py
uv run python src/mcp/facebook_server.py
uv run python src/mcp/instagram_server.py

# Manual CEO Briefing
uv run python -m src.main briefing

# Check component health
cat .state/health.json | jq

# View today's audit logs
cat AI_Employee_Vault/Logs/$(date +%Y-%m-%d).json | jq

# Check Ralph Wiggum counter
cat /tmp/ralph-wiggum-counter
```

---

## APPENDIX B: KEY CONCEPTS QUICK REFERENCE

| Concept | One-Liner |
|---------|-----------|
| **Odoo** | Self-hosted accounting via Docker |
| **JSON-RPC** | HTTP-based function calls to Odoo |
| **Meta Graph API** | Facebook + Instagram official API |
| **Cross-Domain** | Personal triggers → Business actions |
| **CEO Briefing** | Weekly automated business report |
| **Workflow ID** | UUID linking related actions across domains |
| **Exponential Backoff** | Retry delays: 1s, 2s, 4s |
| **Component Health** | Track healthy/degraded/down per domain |
| **Ralph Wiggum** | Autonomous multi-step execution |
| **Stop Hook** | Shell script that forces Claude to continue |
| **MCP Server** | Gives Claude "hands" to use external APIs |

---

## APPENDIX C: COMMON BEGINNER QUESTIONS

**Q: Do I need to pay for Odoo?**
A: No! Odoo Community Edition is free. Only paid modules are Enterprise features (not needed for Gold Tier).

**Q: Can I use my personal Facebook profile?**
A: No. Meta Graph API only supports Business Pages. Personal profiles require Playwright (optional, not production-ready).

**Q: Is Instagram API free?**
A: Yes! Instagram Business/Creator API is free via Meta Graph API.

**Q: What if Odoo Docker uses too much RAM?**
A: Odoo + PostgreSQL use ~500MB-1GB RAM. You can stop Odoo when not needed: `docker compose down`.

**Q: Can I skip Silver Tier and go straight to Gold?**
A: No. Gold builds on Silver's foundation (Gmail Watcher, WhatsApp Watcher, MCP architecture).

**Q: How long does Gold Tier take to implement?**
A: Estimated 40+ hours (per hackathon docs). With SpecKit Plus prompts: 15-20 hours.

**Q: What if I hit Instagram's 25 posts/day limit?**
A: Track in audit logs. Limit resets every 24 hours. For most use cases, 25/day is generous.

**Q: Does CEO Briefing work if Odoo is down?**
A: Yes! Briefing is generated with available data. Missing sources are noted.

**Q: Can Ralph Wiggum Loop run forever?**
A: No. Max iterations (default 10) prevents infinite loops.

**Q: Are audit logs secure?**
A: Yes. Sensitive data (tokens, passwords) are never logged. Logs stored locally in vault.

---

## APPENDIX D: WHAT'S NEXT: PLATINUM TIER

### Platinum Tier Features (Future)

| Feature | Description |
|---------|-------------|
| **Multi-Agent System** | Multiple Claude instances collaborating |
| **Voice Interface** | Speak to your AI Employee |
| **Cloud Sync** | Vault sync across devices |
| **Production-Grade** | PM2 for all watchers, auto-restart |
| **Advanced Analytics** | Business intelligence dashboards |
| **Custom Integrations** | Slack, Trello, Notion, etc. |

### When to Start Platinum?

- ✅ Gold Tier fully implemented and working
- ✅ All 6 MCP servers operational
- ✅ CEO Briefing generating weekly
- ✅ Cross-domain workflows stable
- ✅ Audit logs clean and traceable

---

**END OF GOLD TIER DOCUMENTATION**

> **Next Steps:**
> 1. Watch video (this documentation)
> 2. Follow implementation prompts
> 3. Test each component
> 4. Run system for 48 hours
> 5. Review first CEO Briefing on Monday morning
> 6. Proceed to Platinum Tier (optional)

**Good luck with Hackathon-0! 🚀**

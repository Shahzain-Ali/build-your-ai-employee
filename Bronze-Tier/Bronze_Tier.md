# Hackathon-0: Bronze Tier — Complete Guide
**Personal AI Employee: Building Autonomous FTEs in 2026**

> **Video Length Target**: 40–60 minutes (Single Video)
> **Audience**: Complete Beginners
> **Focus**: Theory + Architecture + Step-by-Step Implementation
> **Language**: English (Examples in Roman Urdu)

---

### PART 1: THEORY & CONCEPTS
| Section | Topic |
|---------|-------|
| 1 | Introduction & What You'll Learn |
| 2 | What is Hackathon-0? |
| 3 | Digital FTE — The Core Concept |
| 4 | Architecture Overview |
| 5 | System Requirements |
| 6 | Bronze Tier — Core Concepts (Deep Dive) |
| 7 | Complete Flow — Putting It All Together |

### PART 2: IMPLEMENTATION (PROMPT-DRIVEN)
| Section | Topic |
|---------|-------|
| 8 | How It Works — You Give Prompts, Claude Does Everything |
| 9 | The 5 Prompts That Build Bronze Tier |
| 10 | Working System — What Success Looks Like |
| 11 | What's Next: Silver → Gold → Platinum |

---

# ═════════════════════════
# PART 1: THEORY & CONCEPTS
# ═════════════════════════

## SECTION 1: INTRODUCTION

### What You Will Learn in This Video

By the end of this video, you will:
- Understand what a **Personal AI Employee** is and why it matters
- Know the complete **architecture** of the system (how all pieces connect)
- Understand **every component** of Bronze Tier and why it exists
- See a **live working demo** — file dropped in → AI processes it automatically
- Know exactly **what comes next** in Silver, Gold, and Platinum tiers

### Who Is This For?

- You have heard about AI agents but never built one
- You want to understand the **full picture** before writing any code
- You use Claude Code (or are curious about it)
- You want a system that actually works autonomously — not just a chatbot

### Prerequisites

- Basic computer knowledge (files, folders, terminal)
- Windows 11 + WSL2 (Ubuntu)
- Claude Code active subscription
- Obsidian installed (free — obsidian.md)

---

## SECTION 2: WHAT IS HACKATHON-0?

### The Big Idea

Hackathon-0 teaches you to build an **AI Employee** (called a Digital FTE) that:
- Works **24 hours a day, 7 days a week**
- Handles your **Personal Affairs**: Gmail, WhatsApp, Bank Statements
- Handles your **Business**: Social Media, Payments, Project Tasks
- Runs **entirely on your local machine** (no cloud, full privacy)
- Uses **Claude Code** as the brain

> **Roman Urdu Example:**
> Socho aapka ek kaam karne wala hai jo kabhi thakta nahi, kabhi chhutti nahi leta,
> aur aapse zyada consistent hai. Woh aapka Gmail check karta hai, bank statement
> padhta hai, suspicious charges flag karta hai, aur har Monday aapko ek CEO briefing
> deta hai ke is hafte business mein kya hua. Yahi hai Digital FTE.

### The Tier System

```
Bronze    → Foundation (Yahan se shuru karein)
           File detection, Claude processing, local vault

Silver    → More Senses
           Gmail watcher + WhatsApp + LinkedIn

Gold      → Autonomous Decision Making
           Claude khud sochta hai, Monday CEO briefing

Platinum  → Always-On
           Cloud sync, multi-device, production-grade
```

**Why Bronze First?**
Bronze is the foundation — without it, nothing else works. Silver needs Bronze's vault
structure. Gold needs Silver's data sources. You cannot skip Bronze.

---

## SECTION 3: DIGITAL FTE — THE CORE CONCEPT

### What is an FTE?

**FTE = Full-Time Equivalent** — a business term for one full-time employee
working 40 hours per week.

A **Digital FTE** is an AI agent that is:
- Built like software
- Priced and managed like a **human employee**
- Deployed to handle real business tasks autonomously

### The Mindset Shift (Most Important Concept)

| Old Thinking | New Thinking |
|-------------|-------------|
| "Buy a software license — $50/month" | "Hire a Digital Employee — $500/month" |
| CEO thinks: optional tool | CEO thinks: this replaces headcount |
| Hard to justify ROI | Easy to justify: 85–90% cost saving |

> **Roman Urdu Example:**
> Jab aap kisi CEO ko kehte ho "AI tool purchase karo" → woh sochta hai optional cheez hai.
> Jab aap kehte ho "ek AI employee hire karo jo $500/month mein $5000/month ka kaam kare"
> → woh immediately samajhta hai. Bas yahi shift hai — mindset ka.

### Human FTE vs Digital FTE

| Feature | Human FTE | Digital FTE |
|---------|-----------|-------------|
| Availability | 40 hours / week | 168 hours / week (24/7) |
| Monthly Cost | $4,000 – $8,000+ | $500 – $2,000 |
| Ramp-up Time | 3 – 6 Months | Instant (via SKILL.md) |
| Consistency | Variable (85–95%) | Predictable (99%+) |
| Cost per Task | ~$3.00 – $6.00 | ~$0.25 – $0.50 |
| Annual Hours | ~2,000 hours | ~8,760 hours |

### The Business Case: Why Digital FTEs Win

> A Digital FTE works **~9,000 hours/year** vs a human's **2,000 hours/year**.
> Cost per task drops from ~$5.00 to ~$0.50 — **85–90% cost saving.**
> This is typically the threshold where a CEO approves a project without debate.

---

## SECTION 4: ARCHITECTURE OVERVIEW

### The 4 Layers of the System

Every AI Employee system has four layers. Remember these — they appear in every tier:

```
┌─────────────────────────────────────────────────┐
│  LAYER 4: HANDS (MCP Servers)                   │
│  Execute external actions                        │
│  Send email, click buttons, post to social media │
│  ← Bronze mein nahi, Silver se shuru hoga        │
├─────────────────────────────────────────────────┤
│  LAYER 3: BRAIN (Claude Code)                   │
│  Reads files, reasons, makes decisions           │
│  Follows Company_Handbook + Agent Skills         │
├─────────────────────────────────────────────────┤
│  LAYER 2: MEMORY / GUI (Obsidian Vault)         │
│  Local markdown files — data + dashboard         │
│  Your window into what the AI is doing           │
├─────────────────────────────────────────────────┤
│  LAYER 1: SENSES (Python Watchers)              │
│  Monitor File System (Bronze), Gmail/WhatsApp+  │
│  Detect new events → create action files         │
└─────────────────────────────────────────────────┘
```

> **Roman Urdu Example:**
> Insaan ka example lein:
> - Aankhein/Kaan = Senses (Watchers) — duniya se signal lete hain
> - Dimaag = Brain (Claude Code) — sochta hai
> - Yaaddasht = Memory (Obsidian) — sab store karta hai
> - Haath = Hands (MCP) — action leta hai

### Bronze Tier: Which Layers Are Active?

| Layer | Bronze | Silver | Gold |
|-------|--------|--------|------|
| Senses | File System Watcher only | + Gmail, WhatsApp | same |
| Memory | Obsidian Vault | same | same |
| Brain | Claude Code | same | + autonomous loop |
| Hands | None (read only) | + MCP Email Server | + more MCPs |

---

## SECTION 5: SYSTEM REQUIREMENTS

### What You Need — Complete Table

| Tool | Required Version | Why Needed | Check Command |
|------|-----------------|------------|---------------|
| Claude Code | v2.1.42+ | The AI brain | `claude --version` |
| Python | 3.13+ (WSL) | Watcher + Orchestrator scripts | `python3 --version` |
| Node.js | v24+ | Required for PM2 | `node --version` |
| uv | Latest | Python package manager | `uv --version` |
| PM2 | Latest | Auto-restart process manager | `pm2 --version` |
| Git | Latest | Version control | `git --version` |
| Obsidian | v1.10.6+ | Vault dashboard GUI | Open app |
| WSL2 | Ubuntu 24.04 | Run Python on Windows | `wsl --version` |

> **Roman Urdu Note:**
> Bronze tier mein koi cloud service, koi extra API key (except Claude Code subscription)
> nahi chahiye. Sab kuch aapke apne computer pe local chalta hai. Privacy 100%.

---

## SECTION 6: BRONZE TIER — CORE CONCEPTS (DEEP DIVE)

> This is the most important section. Take your time here.

---

### 6.1 The Vault — Your AI Employee's Home

**What is a Vault?**

A vault is **just a normal folder on your computer**. Nothing special. When you open
this folder in Obsidian, Obsidian calls it a "vault."

```
C:\Users\YourName\AI_Employee_Vault\   ← This IS the vault
```

> **Roman Urdu Example:**
> Vault = Office building.
> Obsidian = Woh building ka reception — aapko sab kuch dikhata hai.
> Claude Code = Employee jo building ke andar kaam karta hai.
> Python Scripts = Security guard jo building ke bahar khada hai aur signal deta hai.

**How to Open a Folder as Vault in Obsidian:**
1. Obsidian open karo
2. Bottom-left corner → vault icon → "Open another vault"
3. "Open folder as vault" select karo
4. Apna `AI_Employee_Vault` folder select karo → Done!

> ⚠️ "Create new vault" mat dabao — woh naya empty folder banata hai.
> "Open folder as vault" use karo existing folder ke liye.

---

### 6.2 Folder Structure — Why Every Folder Exists

```
AI_Employee_Vault/
├── Dashboard.md          ← Aapka real-time status screen
├── Company_Handbook.md   ← Claude ke liye rules/rulebook
│
├── Inbox/                ← Aap khud files drop karte ho (manual)
├── Needs_Action/         ← Watchers automatic files banate hain (auto)
├── Done/                 ← Completed kaam (Claude move karta hai)
│
├── Pending_Approval/     ← Sensitive actions — RUKO (Claude banata hai)
├── Approved/             ← Aap ne haan kaha (aap move karte ho)
├── Rejected/             ← Aap ne na kaha (aap move karte ho)
│
└── Logs/                 ← JSON audit trail (every action recorded)
```

**Each Folder's Purpose:**

| Folder | Who Creates Files Here | Who Reads From Here |
|--------|----------------------|-------------------|
| `Inbox/` | YOU (manual drop) | File System Watcher |
| `Needs_Action/` | Python Watchers (auto) | Orchestrator + Claude |
| `Done/` | Claude (auto move) | You (review) |
| `Pending_Approval/` | Claude (auto create) | You (review) |
| `Approved/` | YOU (manual move) | Orchestrator (detects) |
| `Rejected/` | YOU (manual move) | Orchestrator (detects) |
| `Logs/` | Claude + Watchers | You (audit) |

> **Roman Urdu Example — Inbox vs Needs_Action confusion:**
>
> Inbox = Aapka personal dak khana. Aapne HBL website se bank statement download ki
> aur yahan daali. Ya WhatsApp pe koi contract mila, aapne yahan daala.
>
> Needs_Action = AI ka to-do list. Watcher automatically file detect karta hai aur
> yahan ek task card banata hai: "FILE_HBL_statement.md — process karo"
>
> Gmail? → Gmail Watcher seedha Needs_Action mein file banata hai (Inbox bypass).
> Manual files? → Inbox mein daalo → Watcher detect kare → Needs_Action mein jaaye.

---

### 6.3 The Two Key Files

#### Dashboard.md — Your Real-Time Status View

This is the first file you open every morning. It shows:

```markdown
# AI Employee Dashboard
**Last Updated**: 2026-02-19 09:30 AM
**Status**: 🟢 Idle

## Pending Tasks: 2
## Pending Approvals: 1 ⚠️
## Completed Today: 5

## Recent Activity (Last 5 Actions)
- [09:25] Processed invoice.pdf → Done/
- [08:45] contract.txt processed → Done/
- [08:30] Bank statement → $850 suspicious charge flagged
- [Yesterday 11:00] Contract processed → renewal: March 2026
- [Yesterday 10:15] resume.pdf → REJECTED (unsupported)
```

> **Roman Urdu Example:**
> Dashboard.md = Aapka WhatsApp home screen. Subah uthte ho,
> pehle yahi dekhte ho — kya aaya, kya pending hai, kya approve karna hai.
> Koi aur file khulne ki zaroorat nahi.

**What "Idle" Means:**
`Status: Idle` = AI abhi koi kaam nahi kar raha — free hai, next task ka wait kar raha hai.
Jab `Needs_Action/` mein koi file aati hai → Status: `Working`.

#### Company_Handbook.md — The AI's Rulebook

This is where YOU define how the AI should behave. Claude reads this before
processing ANY file.

```markdown
# Company Handbook

## Approval Required (HITL):
- Any payment over $500 → flag for approval
- Email to unknown contacts → flag for approval
- File deletion → ALWAYS flag for approval

## Unknown File Types:
- .exe, .bat, .sh → Reject immediately, log reason

## Tone & Behavior:
- Be professional and concise
- Always log actions taken
- When uncertain, flag for human review
```

> **Roman Urdu Example:**
> Company_Handbook.md = Employee handbook jo aap apne naye employee ko dete ho.
> "Yeh karo, yeh mat karo, is situation mein yeh karo."
> Claude isko padhta hai — phir decide karta hai kya karna hai.

---

### 6.4 File System Watcher — The AI's Eyes

**What It Does:**
- Runs **24/7** in the background
- Watches the `Inbox/` folder
- When a new file appears → creates a task card in `Needs_Action/`
- Does **NOT** use Claude — pure Python

**Technology:** `watchdog` library — event-driven (not polling)

**What "Event-Driven" Means:**

> **Roman Urdu Example:**
> Polling = Har 60 second mein fridge kholna aur dekhna kuch aaya?
> Event = WhatsApp notification — jab message aaye, tab phone hilta hai.
>
> Watcher event-based hai — OS us ko batata hai jab Inbox/ mein koi file aati hai.
> Watcher ko baar baar check nahi karna padta. Zyada efficient hai.

**What the Watcher Creates (Action File):**

When `invoice.pdf` is dropped in `Inbox/`, watcher creates `Needs_Action/FILE_invoice.md`:

```markdown
---
status: pending
source: inbox
file_type: pdf
original_name: invoice.pdf
file_size: 245KB
detected_at: 2026-02-19T09:30:00
---

# Action Required: Process invoice.pdf

A new file has been detected in Inbox/.
Please process according to Company_Handbook rules.
```

**File Type Validation:**
- `.exe`, `.bat`, `.sh`, `.cmd` → **REJECTED** → creates `REJECTED_virus.exe.md`
- All other types → accepted → creates `FILE_name.md`

**Idempotent Startup (Industry Standard):**

> **Roman Urdu — "Idempotent" ka matlab:**
> "Idempotent" = Ek hi operation kitni baar bhi repeat karo — result same rahega.
> Duplicate nahi banega. Koi side effect nahi hoga.
>
> Beginner problem: System restart karo → Inbox/ mein pehle se existing 100 files
> dobara "new file detected" dikhain → 100 duplicate action files ban jaayein. Mess!
>
> Idempotent solution: Watcher ek "seen files" list rakhta hai. Restart pe pehle
> existing files ko "already processed" mark karta hai, phir sirf NAYE files track
> karta hai. Kitni baar bhi restart karo — zero duplicates.
> Yahi hai industry-standard production code.

```
Final Result — 3 Restarts, Zero Duplicates:
┌──────────────────────┬────────────────────────┬──────────────────────┐
│        Start         │     What detected      │        Result        │
├──────────────────────┼────────────────────────┼──────────────────────┤
│ First time           │ invoice.pdf, virus.exe │ ✅ Correct           │
├──────────────────────┼────────────────────────┼──────────────────────┤
│ Restart (same files) │ Nothing new            │ ✅ Industry Standard │
├──────────────────────┼────────────────────────┼──────────────────────┤
│ Restart + new file   │ Only new_report.txt    │ ✅ Correct           │
└──────────────────────┴────────────────────────┴──────────────────────┘
```

---

### 6.5 Orchestrator — The Manager

**What It Does:**
- Runs **24/7** in the background
- **Polls** `Needs_Action/` every 60 seconds (configurable)
- When pending files found → triggers Claude Code
- Waits for Claude to finish → updates Dashboard
- Handles errors and retries

**Technology:** Python `subprocess.run()` to trigger Claude Code CLI

**What "Polling" Means:**

> **Roman Urdu Example:**
> Orchestrator = Office manager jo har 60 second mein Needs_Action/ folder mein
> jaata hai aur dekhta hai koi pending kaam hai?
> Kaam mila → Claude Code ko trigger karta hai → wait karta hai →
> phir waapis jaata hai next round ke liye.

**Orchestrator's Logic:**

```
Every 60 seconds:
    ↓
Look in Needs_Action/ for files with status: pending
    ↓
If files exist AND Claude not currently running:
    → Pick oldest file first (chronological order)
    → Trigger Claude Code
    → Wait (max 5 minutes timeout)
    → If success → update Dashboard
    → If timeout → retry (max 3 attempts) → log failure
    ↓
Wait 60 seconds → repeat
```

**Concurrent Claude Protection:**
What if two files arrive at once? Orchestrator checks if Claude is already running.
If yes → waits → processes next file in queue. One at a time. Safe.

---

### 6.6 Claude Code — The Brain

**What It Does:**
- Does NOT run 24/7 — runs only when triggered
- Reads `Company_Handbook.md` → understands rules
- Reads the action file in `Needs_Action/` → understands task
- Uses **Agent Skills** → follows defined procedures
- Takes action → moves file to `Done/` or creates approval request
- Updates `Dashboard.md`
- Exits

> **Roman Urdu Example:**
> Teen roles ki analogy:
> - Security Guard (Watcher) = 24/7 gate pe khada, koi aaye to andar bhejta hai
> - Manager (Orchestrator) = 24/7 office mein, kaam assign karta hai
> - Employee (Claude Code) = Aata hai, kaam karta hai, ghar chala jata hai
>
> Claude Code ek on-demand employee hai — jab kaam ho tab aao, khatam karo, jao.
> 24/7 chalne ki zaroorat nahi — resource waste hoga.

---

### 6.7 Agent Skills — The Procedures

**What Are They?**
Every repeatable task the AI does is defined as a **named skill** — a markdown file
in `.claude/skills/`. Claude reads these before doing any task.

> **Roman Urdu Example:**
> Company_Handbook.md = General employee handbook (rules)
> Agent Skills = SOPs (Standard Operating Procedures) — step-by-step kaam kaise karo
>
> Handbook kehta hai: "$500+ payments flag karo"
> Skill batata hai: "Bank statement process karne ke exact steps:
>   Step 1: PDF padho, Step 2: Transactions nikalo, Step 3: $500+ check karo..."

**Bronze Tier — 3 Required Skills:**

```
.claude/skills/
├── process_document.md        ← Generic: koi bhi file process karo
├── update_dashboard.md        ← Dashboard.md update karne ke steps
└── create_approval_request.md ← HITL approval file banana
```

**Why Skills Matter:**
- Adding new AI behavior = creating ONE new `.md` file (zero code changes)
- You can read and understand exactly what the AI will do
- You can modify AI behavior without touching Python code
- Silver/Gold tiers just add more skill files — same pattern

---

### 6.8 HITL — Human in the Loop

**What Is HITL?**
Human-in-the-Loop = Before taking a sensitive action, the AI **stops and asks you**.
It does NOT proceed until you explicitly approve.

> **Roman Urdu Example:**
> HITL = Ek responsible employee jo koi bada faisla khud nahi karta.
> "Sir, $850 ka payment Dubai account pe ja raha hai. Mujhe nahi pata yeh valid hai ya nahi.
> Aap approve karein tab main transfer karoon ga."
>
> "Flag karna" = Alert banana + rokna + approval maangna
> Flag ≠ Delete, Flag ≠ Reject. Bas: "Ruko — pehle poocho."

**HITL Flow:**

```
Claude processes bank statement
    ↓
Detects $850 charge (over $500 threshold from Handbook)
    ↓
Creates: Pending_Approval/APPROVAL_suspicious_850.md
    ↓
Dashboard shows: ⚠️ 1 Action Pending Approval
    ↓
YOU open Obsidian → read the approval file → decide
    ↓
YOU move file to:
    Approved/  → Orchestrator sees it → Claude continues → Done/
    Rejected/  → Orchestrator sees it → Claude logs rejection → Done/
```

**What Requires Approval in Bronze Tier (per spec FR-008):**
- Any payment over threshold set in Company_Handbook.md
- Email to unknown contacts
- File deletions

---

### 6.9 Audit Logging — Every Action Recorded

Every single AI action produces a log entry. No exceptions (spec SC-004: 100%).

**Log File:** `Logs/2026-02-19.json` — one file per day

```json
{
  "id": "uuid-1234",
  "timestamp": "2026-02-19T09:30:00",
  "action_type": "file_processed",
  "source_file": "FILE_invoice.pdf.md",
  "result": "success",
  "approval_status": "not_required",
  "skill_used": "process_document"
}
```

---

### 6.10 Process Management — PM2

PM2 keeps the system running 24/7:
- Auto-restarts if scripts crash (within 60 seconds) — spec FR-012
- Survives computer reboots
- Shows status of all running processes

> **Roman Urdu Example:**
> PM2 = Ek supervisor jo employees ko manage karta hai.
> Employee crash kiya? Supervisor immediately restart karta hai.
> Computer reboot hua? Supervisor seedha kaam shuru karta hai.

---

## SECTION 7: COMPLETE FLOW — PUTTING IT ALL TOGETHER

### Flow 1: Manual File Drop

```
Aap HBL_Jan_2026.pdf ko Inbox/ mein drop karte ho
    ↓
[File System Watcher — Event-based, instant detection]
File detected → validate type → extract metadata
→ Creates: Needs_Action/FILE_HBL_Jan_2026.md (status: pending)
    ↓
[Orchestrator — Polling every 60 seconds]
Sees new file → Claude not running → triggers Claude Code
    ↓
[Claude Code — runs, processes, exits]
1. Reads Company_Handbook.md → understands rules
2. Reads FILE_HBL_Jan_2026.md → understands task
3. Uses process_document skill → reads PDF
4. Extracts transactions:
   - Netflix: -$15 ✅
   - Client Ali: +$1,500 ✅
   - Unknown Dubai: -$850 ⚠️ ($500+ flag!)
   - Electricity: -$45 ✅
5. $850 > threshold → creates Pending_Approval file
6. Updates Dashboard.md → "⚠️ 1 Pending Approval"
7. Logs action → Exits
    ↓
[YOU — Human-in-the-Loop]
Open Obsidian → see ⚠️ on Dashboard
Read approval file → move to Approved/ or Rejected/
    ↓
[Orchestrator detects decision → Claude finalizes → Done/]
```

### Flow 2: Executable File (Security Rejection)

```
Aap virus.exe ko Inbox/ mein drop karte ho
    ↓
[File System Watcher]
Detects .exe → REJECTED
Creates: Needs_Action/REJECTED_virus.exe.md
```

### The Complete Architecture Diagram

```
                    YOU
                     │
                     │ Drop file manually
                     ▼
          ┌─────────────────────┐
          │      Inbox/         │
          └─────────┬───────────┘
                    │ watchdog event
                    ▼
          ┌─────────────────────┐         ┌──────────────┐
          │ filesystem_watcher  │ ──────→  │ Needs_Action/│
          │    (24/7, Python)   │  .md file│              │
          └─────────────────────┘         └──────┬───────┘
                                                  │ polling (60s)
          ┌─────────────────────┐                 │
          │   orchestrator.py   │ ◄───────────────┘
          │    (24/7, Python)   │
          └─────────┬───────────┘
                    │ subprocess.run()
                    ▼
          ┌─────────────────────┐
          │    Claude Code      │ ← reads Company_Handbook.md
          │  (on-demand, AI)    │ ← reads .claude/skills/
          └─────────┬───────────┘
                    │
          ┌─────────┴──────────────────────┐
          │                                │
          ▼                                ▼
   ┌─────────────┐                ┌──────────────────┐
   │   Done/     │                │ Pending_Approval/ │
   │ (completed) │                │ (needs your OK)  │
   └─────────────┘                └────────┬─────────┘
                                           │ YOU decide
                                    ┌──────┴──────┐
                                    ▼             ▼
                               Approved/      Rejected/
```

---

# ═══════════════════════════════════════════════════
# PART 2: IMPLEMENTATION (PROMPT-DRIVEN)
# ═══════════════════════════════════════════════════

## SECTION 8: HOW IT WORKS — YOU GIVE PROMPTS, CLAUDE DOES EVERYTHING

> **The Most Important Thing to Understand:**
> Aap code nahi likhte. Aap sirf Claude Code ko prompts dete ho.
> Claude Code sab kuch karta hai — system check, files banata hai, code likhta hai,
> tests run karta hai, system start karta hai. Aap sirf direction dete ho.

### The SpecKit Plus Framework

This project uses **SpecKit Plus** — a Spec-Driven Development framework built into
Claude Code. It follows a strict order:

```
Prompt 1 → ANALYZE   → Claude reads official documentation, understands requirements
Prompt 2 → SPECIFY   → Claude generates complete specification (spec.md)
Prompt 3 → PLAN      → Claude generates architecture plan (plan.md)
Prompt 4 → IMPLEMENT → Claude builds everything (vault, scripts, skills, tests)
Prompt 5 → VERIFY    → Claude checks system, runs tests, starts everything
```

> **Roman Urdu Note:**
> Yeh blueprint-first approach hai.
> Pehle kya banana hai (spec) → phir kaise banana hai (plan) → phir banao (implement).
> Direct coding mein jump karna = bina map ke safar karna.

---

## SECTION 9: THE 5 PROMPTS THAT BUILD BRONZE TIER

### PROMPT 1 — Analyze the Documentation

**What this prompt does:**
Claude Code reads the official Hackathon-0 documentation, analyzes all Bronze tier
requirements, and reports back what needs to be built.

```
Go through the official Hackathon-0 documentation carefully.
Analyze and understand what Bronze tier requires — the folder structure,
the watcher, the orchestrator, the skills, HITL safety, and all
functional requirements. Also check our system to verify all
prerequisites are installed (Python, Node.js, Claude Code, uv, PM2).
Report what you find and what needs to be set up.
```

**What Claude does after this prompt:**
- Reads the PDF documentation
- Reads the official spec requirements
- Checks `python3 --version`, `node --version`, `claude --version`, `uv --version`
- Reports: what is installed, what needs installing, what needs updating
- You review the report and confirm to proceed

---

### PROMPT 2 — Generate the Specification

**What this prompt does:**
Claude Code generates the complete formal specification for Bronze tier using SpecKit Plus.

```
/sp.specify

Hackathon-0 Bronze Tier: Personal AI Employee Foundation — Build a local-first
autonomous AI agent using Claude Code and Obsidian vault. Includes: proper vault folder
structure (Inbox, Needs_Action, Done, Logs, Pending_Approval, Approved, Rejected),
Dashboard.md, Company_Handbook.md, one working File System Watcher Python script
(using uv), Orchestrator.py to trigger Claude Code, and all AI functionality
implemented as Agent Skills. Must follow HITL safety for sensitive actions and
security-by-design principles.
```

**What Claude generates:**
- `specs/001-bronze-fte-foundation/spec.md` — 12 functional requirements
- 4 user stories with acceptance criteria
- 7 measurable success criteria (SC-001 to SC-007)
- Key entities defined (Vault, Action File, Approval File, Skill, Dashboard, Handbook)
- Out of scope items listed (Gmail, WhatsApp → Silver tier)

---

### PROMPT 3 — Generate the Plan

**What this prompt does:**
Claude Code reads the spec and generates the full architecture and implementation plan.

```
/sp.plan
```

**What Claude generates:**
- `specs/001-bronze-fte-foundation/plan.md` — complete architecture document
- Technology decisions with rationale (why watchdog, why subprocess, why PM2, why JSON)
- Full project structure (every file and folder)
- Component architecture diagrams
- Risk analysis
- All Python dependencies listed (`watchdog`, `python-dotenv`, `pytest`)

---

### PROMPT 4 — Build Everything

**What this prompt does:**
Claude Code reads the plan and implements the complete Bronze tier — every file,
every script, every skill, every test.

```
/sp.implement

Go through the tasks in specs/001-bronze-fte-foundation/tasks.md one by one.
Build the complete Bronze tier:
- Set up Python project with uv
- Create the vault folder structure
- Create Dashboard.md and Company_Handbook.md
- Build the filesystem watcher (watchdog, idempotent startup)
- Build the orchestrator (polling, Claude trigger, retry logic)
- Create all 3 agent skills in .claude/skills/
- Set up PM2 ecosystem config
- Write unit and integration tests
Follow all requirements from spec.md exactly.
```

**What Claude builds:**
- `AI_Employee_Vault/` — complete folder structure (7 subfolders)
- `AI_Employee_Vault/Dashboard.md` — real-time status template
- `AI_Employee_Vault/Company_Handbook.md` — AI rulebook
- `src/watchers/filesystem_watcher.py` — event-driven Inbox/ monitor
- `src/orchestrator/orchestrator.py` — 60s polling, Claude trigger, retry
- `src/utils/logger.py` — JSON audit logging
- `src/utils/dashboard.py` — Dashboard.md updater
- `src/main.py` — entry point (starts watcher + orchestrator)
- `.claude/skills/process_document.md` — generic file processing SOP
- `.claude/skills/update_dashboard.md` — dashboard update SOP
- `.claude/skills/create_approval_request.md` — HITL approval SOP
- `ecosystem.config.js` — PM2 configuration
- `pyproject.toml` — uv project config
- `.env.example` — environment variables template
- `tests/` — unit and integration tests

---

### PROMPT 5 — Verify, Run and Test

**What this prompt does:**
Claude Code verifies the complete build, starts the system, and runs all tests
to confirm Bronze tier is working per the official success criteria.

```
The Bronze tier implementation is complete. Now:
1. Verify all files are created correctly per the spec
2. Run the test suite: pytest tests/
3. Start the system with PM2
4. Run the 4 validation tests from the spec (SC-001 to SC-005):
   - Drop a test file in Inbox/ → verify FILE_*.md appears in Needs_Action/ within 60s
   - Drop a .exe file → verify REJECTED_*.md appears
   - Verify Dashboard.md updates automatically
   - Kill PM2 process → verify auto-restart within 60s
5. Report results — all success criteria must pass
```

**What Claude verifies:**
- All 82 tasks from tasks.md are complete
- All tests pass: `pytest tests/`
- `pm2 status` shows both processes online
- File drop → Needs_Action/ within 60s (SC-001) ✅
- Claude processes → Done/ within 2 min (SC-002) ✅
- Sensitive action → Pending_Approval/ (SC-003) ✅
- 100% actions logged (SC-004) ✅
- Crash recovery within 60s (SC-005) ✅
- Dashboard shows 24hr activity (SC-006) ✅
- New skill = new .md only (SC-007) ✅

---

## SECTION 10: WORKING SYSTEM — WHAT SUCCESS LOOKS LIKE

When Bronze Tier is fully working, this is what you see:

```
[Terminal — pm2 status]
┌────┬──────────────────┬─────────┬──────────┐
│ id │ name             │ status  │ restarts │
├────┼──────────────────┼─────────┼──────────┤
│ 0  │ fte-watcher      │ online  │ 0        │
│ 1  │ fte-orchestrator │ online  │ 0        │
└────┴──────────────────┴─────────┴──────────┘

[Obsidian — Dashboard.md]
Status: 🟢 Idle
Pending Tasks: 0
Completed Today: 3
Recent Activity:
  - [09:25] invoice.pdf processed → Done/
  - [08:45] contract.txt processed → Done/
  - [08:30] virus.exe → REJECTED

[After dropping a file into Inbox/]
→ Within 60 seconds: FILE_invoice.md appears in Needs_Action/
→ Within 2 minutes: Claude processes it → moves to Done/
→ Dashboard.md updates automatically — no manual action needed
```

**All 7 Official Success Criteria — Verified:**

| Criteria | What to Check |
|----------|---------------|
| SC-001: File detected within 60s | Drop file → check Needs_Action/ |
| SC-002: Claude processes within 2min | Watch Dashboard update |
| SC-003: Sensitive actions halted | Payment file → check Pending_Approval/ |
| SC-004: 100% actions logged | Check Logs/YYYY-MM-DD.json |
| SC-005: Auto-restart within 60s | Kill process → watch PM2 restart |
| SC-006: Dashboard shows 24hr activity | Read only Dashboard.md — nothing else needed |
| SC-007: New skill = new .md file only | Add skill file → zero code changes |

---

## SECTION 11: WHAT'S NEXT — THE TIER ROADMAP

```
BRONZE ✅ (This Video)
├── Local File System Watcher
├── Orchestrator + Claude Code
├── Obsidian Vault + Dashboard
└── Agent Skills + HITL

        ↓

SILVER (Next Video)
├── Gmail Watcher (OAuth2, Google API)
├── WhatsApp Watcher (Playwright automation)
├── LinkedIn automation
├── MCP Email Server (Claude can SEND emails)
└── APScheduler (time-based tasks)

        ↓

GOLD (Future)
├── Ralph Wiggum Loop (Claude continuously iterates)
├── Autonomous decision making
├── Monday CEO Briefing (automated report)
└── Claude orchestrates multi-step workflows

        ↓

PLATINUM (Future)
├── Cloud sync (always-on)
├── Multi-device access
└── Production-grade deployment
```

> **Roman Urdu Final Note:**
> Bronze mein aapne foundation banaya — sab kuch local, simple, working.
> Silver mein "aankhein" badi karein — ab Gmail aur WhatsApp bhi dekhe ga.
> Gold mein "dimaag" powerful hoga — Claude khud sochega, aap sirf approve karo.
> Platinum mein "body" strong hogi — cloud pe, hamesha on.
>
> Har tier bronze ke upar build hota hai. Bronze galat hua toh baaki sab collapse.
> Isliye bronze ko theek se samjho aur theek se banao.

---

## APPENDIX: COMMON BEGINNER QUESTIONS

**Q: Does Claude Code run 24/7?**
No. Claude runs only when triggered by the Orchestrator. It processes one file, then exits.
The Orchestrator and Watcher run 24/7 — Claude does not.

**Q: Does the Gmail Watcher use Claude to create files?**
No. Gmail Watcher is a pure Python script. It detects emails and creates .md files
in Needs_Action/ without any Claude involvement. (Silver tier feature)

**Q: What is the difference between Inbox/ and Needs_Action/?**
Inbox/ = you manually drop files here.
Needs_Action/ = watchers automatically create task files here.
Never manually put files in Needs_Action/.

**Q: Can I see everything in VS Code instead of Obsidian?**
Yes. But Obsidian gives clickable links, beautiful rendering, and a proper dashboard
experience. Claude uses neither — it reads files via terminal. Obsidian is for YOU.

**Q: What is `[[filename]]` syntax?**
Obsidian's WikiLinks — NOT standard Markdown. Only works in Obsidian.
VS Code does not render it. Use `[text](file.md)` for standard links.

**Q: If I restart my computer, do duplicate files get created?**
No — idempotent startup prevents this. The watcher marks existing files on startup,
then only tracks NEW files. Zero duplicates no matter how many restarts.

**Q: How do I add new AI behavior?**
Create a new `.md` file in `.claude/skills/` directory.
Zero Python code changes needed. Claude reads it on the next run. (SC-007)

**Q: What happens if the orchestrator and watcher crash?**
PM2 automatically restarts them within 60 seconds. No manual action needed. (FR-012)

**Q: Do I need to write any Python code myself?**
No. You give prompts to Claude Code. Claude writes all Python scripts, creates all
files, runs all tests, and starts the system. You only provide direction and review.

---

## KEY CONCEPTS QUICK REFERENCE

| Concept | Simple Definition | Roman Urdu Analogy |
|---------|------------------|-------------------|
| Vault | Normal folder on disk | AI ka office building |
| Obsidian | Visual dashboard for vault | Building ka reception |
| Dashboard.md | Real-time status file | WhatsApp home screen |
| Company_Handbook.md | Claude's rulebook | Employee handbook |
| Agent Skill | Step-by-step AI procedure | SOP document |
| File System Watcher | Inbox/ monitor (24/7) | Gate pe security guard |
| Orchestrator | Needs_Action/ poller | Office manager |
| Claude Code | On-demand AI brain | Employee (aao, karo, jao) |
| HITL | Stop + ask human | Responsible employee |
| Flag | Alert + stop + ask | "Sir, aap dekho pehle" |
| Polling | Regular interval check | Har 60s folder check karna |
| Event-driven | OS notification | WhatsApp ping |
| Idempotent | Same result every time, no duplicates | Restart karo — koi farq nahi |
| PM2 | Process manager | Supervisor jo auto-restart kare |
| Action File | Pending task card in Needs_Action/ | To-do note |
| Approval File | Pending decision in Pending_Approval/ | Sign karne wala document |
| SpecKit Plus | Spec-Driven Development framework | Blueprint banao, phir banao |
| MCP Server | External action tool (Silver+) | Hands (Bronze mein nahi) |

---

*Hackathon-0 Bronze Tier Video Guide*
*Date: February 2026 | Audience: Beginners | Language: English + Roman Urdu examples*
*Based on official Hackathon-0 documentation and specs/001-bronze-fte-foundation/*

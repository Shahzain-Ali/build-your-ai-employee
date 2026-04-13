# AI Employee Blueprint

A complete, tiered guide to building **autonomous AI Employees (Digital FTEs)** using Claude Code, Python, and Obsidian — running 100% locally on your machine.

> **Digital FTE** = A Full-Time Equivalent AI agent that works 24/7, handles real business tasks autonomously, and costs 85–90% less than a human employee.

---

## What Is This?

This repository contains structured documentation for **Hackathon-0** — a project that teaches you to build a Personal AI Employee from scratch using a prompt-driven, spec-first approach.

You don't write code manually. You give prompts to Claude Code — Claude does everything.

---

## Tier System

| Tier | Focus | Key Features |
|------|-------|-------------|
| 🥉 **Bronze** | Foundation | File System Watcher, Orchestrator, Obsidian Vault, Agent Skills, HITL Safety |
| 🥈 **Silver** | More Senses | Gmail Watcher, WhatsApp, LinkedIn, MCP Email Server |
| 🥇 **Gold** | Autonomous Decisions | Autonomous loop, Monday CEO Briefing, multi-step workflows |
| 💎 **Platinum** | Always-On | Cloud sync, multi-device, production-grade deployment |

> Each tier builds on the previous. Bronze is the foundation — skip it and everything else breaks.

---

## Architecture (4 Layers)

```
┌─────────────────────────────────────────┐
│  LAYER 4: HANDS  (MCP Servers)          │  ← Silver+
│  Execute external actions               │
├─────────────────────────────────────────┤
│  LAYER 3: BRAIN  (Claude Code)          │  ← All Tiers
│  Reads files, reasons, decides          │
├─────────────────────────────────────────┤
│  LAYER 2: MEMORY (Obsidian Vault)       │  ← All Tiers
│  Local markdown files + dashboard       │
├─────────────────────────────────────────┤
│  LAYER 1: SENSES (Python Watchers)      │  ← All Tiers
│  Monitor file system, Gmail, WhatsApp   │
└─────────────────────────────────────────┘
```

---

## Tech Stack

- **AI Brain** — Claude Code (via CLI)
- **Watchers** — Python + `watchdog` (event-driven, not polling)
- **Process Manager** — PM2 (auto-restart, survives reboots)
- **Dashboard** — Obsidian Vault (local markdown)
- **Framework** — SpecKit Plus (Spec-Driven Development)
- **Platform** — Windows 11 + WSL2 (Ubuntu)

---

## How It Works (Bronze)

```
You drop a file into Inbox/
        ↓
File System Watcher detects it → creates task in Needs_Action/
        ↓
Orchestrator (polls every 60s) → triggers Claude Code
        ↓
Claude reads Company_Handbook.md + Agent Skills → processes file
        ↓
Normal result    → Done/
Sensitive action → Pending_Approval/ (you decide: Approved/ or Rejected/)
        ↓
Dashboard.md updates automatically
```

---

## Repository Structure

```
ai-employee-blueprint/
├── Bronze-Tier/
│   └── Bronze_Tier.md    # Complete beginner guide (theory + 5 prompts)
├── Silver-Tier/
│   └── Silver_Tier.md    # Gmail, WhatsApp, MCP integration
├── Gold_Tier/
│   └── Gold_Tier.md      # Autonomous decision making, CEO briefing
└── API_Setup_Guides/     # API setup guides (Gmail, LinkedIn, Facebook/Instagram)
```

---

## Human FTE vs Digital FTE

| Feature | Human FTE | Digital FTE |
|---------|-----------|-------------|
| Availability | 40 hrs/week | 168 hrs/week (24/7) |
| Monthly Cost | $4,000–$8,000+ | $500–$2,000 |
| Ramp-up Time | 3–6 months | Instant |
| Consistency | 85–95% | 99%+ |
| Cost per Task | ~$5.00 | ~$0.50 |

---

## Prerequisites (Bronze Tier)

- Claude Code (active subscription)
- Python 3.13+ (WSL2)
- Node.js v24+
- PM2, uv, Git
- Obsidian (free)
- Windows 11 + WSL2 (Ubuntu 24.04)

> No cloud services or extra API keys needed for Bronze. Everything runs locally.

---

## Built By

**Shahzain Ali** — AI Automation Developer
. [GitHub](https://github.com/Shahzain-Ali) 
· [LinkedIn](https://www.linkedin.com/in/shahzain-ali-518b862ba/))

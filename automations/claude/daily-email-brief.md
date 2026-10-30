## What it does

Every morning Claude scans the last 24 hours of Gmail, categorises every email by urgency and sender relationship, surfaces the 3 things that need your attention today, and drafts ready-to-send replies for anything routine — all presented as a clean report here in Claude.

## Inputs

- **Gmail** — last 24 hours of inbox (via MCP)
- **Sender context** — inferred from email history (close contact, unknown, service/tool)
- **Topic interests** — provided by the user, baked into the system prompt (e.g. AI, startups, product design)

## Output

A morning triage report structured as:

### 🔴 Needs your attention today
The 3 highest-priority emails, each with:
- **From** — sender name and relationship
- **Summary** — what they want in one sentence
- **Suggested action** — reply, decide, delegate

### 📋 Everything else
A scannable list of remaining emails categorised as:
- **FYI** — no action needed
- **Service/tool** — automated, safe to ignore

### 📰 Newsletters worth reading today
A curated pick from the day's newsletters, matched against your topic interests — each with:
- **Title** — newsletter name and edition
- **Why** — one line on why it's relevant to you today

Anything that doesn't match your interests is silently skipped.

### ✉️ Drafted replies
For any routine email Claude can handle, a friendly warm draft saved directly in Gmail as a draft — ready for your review and one-click send.

## Guardrails

- Never sends anything automatically — drafts only
- Skips newsletters, automated notifications and receipts from the surfaced list
- Caps the "needs attention" list at 3 — forces prioritisation

## Schedule

Runs once every morning, unattended. Report shows up here in Claude when you start your day.
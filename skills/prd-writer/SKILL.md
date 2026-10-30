---
name: prd-writer
description: Generate a lean, downloadable Product Requirements Document (PRD) from a feature or product idea. Use this skill whenever the user mentions writing a PRD, product spec, feature doc, requirements doc, or says things like "I want to spec out a feature", "help me document this idea", "write up requirements for X", or "I have a product idea I want to turn into a document". Trigger even for vague or early-stage ideas — the skill will interview the user to extract what's needed. Always prefer this skill over writing a freeform markdown response when the deliverable is a PRD or product spec.
---

# PRD Writer Skill

Produces a lean, one-page PRD as a downloadable `.md` file. Designed for solo developers and side projects — fast to write, clear enough to align your future self and any collaborators.

---

## Workflow

### Step 1 — Interview the user

Before writing anything, ask clarifying questions to fill in the required sections. Keep questions conversational and grouped — don't ask one at a time unless the user's input is already detailed.

**Minimum info needed to write a good PRD:**

| Section | What to extract |
|---|---|
| Problem & motivation | What pain or gap does this solve? Who has it? |
| Goals & non-goals | What does success look like? What is explicitly out of scope? |
| User stories | 1–3 concrete scenarios: "As a [user], I want to [action] so that [outcome]" |
| Solution overview | What is being built? High-level description, not implementation details |
| Open questions | What is still unknown or undecided? |

**If the user's initial message already covers most of this, skip or shorten the interview.** Only ask about what's genuinely missing.

Sample opening when the idea is vague:
> "Happy to turn this into a PRD. A few quick questions: Who is this for, and what problem does it solve for them? What would a successful version look like — and is there anything you're deliberately *not* building right now?"

---

### Step 2 — Write the PRD

Use the template below. Keep it to one page (roughly 400–600 words in the body). 

**Writing style:**
- Prose for context-heavy sections (Problem, Solution overview)
- Bullets for scannable sections (Goals, Non-goals, User stories, Open questions)
- Plain language — no buzzwords, no padding

**Do not include:**
- Why now / market opportunity framing
- Milestones or timelines
- Launch checklists
- Decision logs
- Stack-specific technical details (keep requirements stack-agnostic)

---

### Step 3 — Save as a downloadable .md file

Save the PRD to `/mnt/user-data/outputs/prd-[feature-name].md` using a slugified version of the feature name (e.g. `prd-user-notifications.md`).

Then call `present_files` with the output path so the user can download it.

Briefly confirm what was written — one or two sentences max. Don't summarize the whole PRD back to them.

---

## PRD Template

```markdown
# PRD: [Feature Name]

**Author:** [leave blank or infer from context]  
**Status:** Draft  
**Last updated:** [today's date]

---

## Problem

[2–4 sentences. What is broken or missing? Who feels this pain and when? Be specific — ground it in a real scenario if possible.]

## Goals

- [Specific, measurable outcome]
- [Another goal]

## Non-goals

- [What this explicitly does not do]
- [Scope boundary]

## User Stories

- As a [user type], I want to [action] so that [outcome].
- As a [user type], I want to [action] so that [outcome].

## Solution Overview

[3–6 sentences. What is being built? Describe the feature from the user's perspective — what they see and do — without getting into implementation details. Mention any key UX decisions or flows if known.]

## Open Questions

- [Unresolved decision or unknown]
- [Another open question]
```

---

## Quality checks before saving

- [ ] Every section is filled — no placeholders left in the output
- [ ] Problem section is specific, not generic ("users struggle with X" not "users need better UX")
- [ ] Non-goals list at least one explicit scope boundary
- [ ] Solution overview describes *what*, not *how*
- [ ] Open questions are genuine unknowns, not rhetorical
- [ ] Total length feels like one tight page — cut anything that doesn't earn its place
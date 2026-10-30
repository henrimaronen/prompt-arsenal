---
name: unpack
description: Give the user just enough context to answer a question Claude just asked them. Use when the user invokes /unpack, says they can't answer yet, "not sure", "what does that mean in practice", or replies to a multiple-choice question with confusion.
metadata:
  version: "0.1"
---

# Unpack

The user can't answer your last question yet. Don't re-explain it. Find the one
gap blocking them, fill only that, then hand the question back in a form they
can answer in one word.

## 1. Diagnose the gap (silently)

Usually one of:
- **Can't picture it**: options are abstract. Show what each concretely
  produces: the code it adds, and exactly what the user would see when it fires
  (error message, test output, wrong number).
- **Can't see the stakes**: what goes wrong under each option, how likely,
  how they'd notice, how hard it is to switch later.
- **Don't know what it hinges on**: the options differ on a fact about the
  user's habits, goals, or environment. Name that fact.
- **Missing referenced context**: you cited an earlier decision, file, or
  term. One line on what it was.

If the user said what confuses them, trust that over your diagnosis.

## 2. Respond

Use this shape; drop any section that doesn't serve the gap:

**What's being decided:** one sentence, in the user's terms, not the implementation's.
**What each looks like:** per option, the concrete artifact + what you'd see when it triggers. 1–3 lines each.
**Stakes:** worst realistic outcome, and reversibility.
**It comes down to:** a question about the user (not the code) that they can
answer from their own knowledge. Map each answer to an option.

End with the crux question, then: "If you don't have a view, <default> is safe
because <why it's cheap to reverse>."

## Rules
- No new options. Don't re-argue your recommendation.
- Concrete beats abstract: a sample error message or a 3-line snippet over a paragraph.
- Under ~15 lines. If you need more, the question was too big; offer to split it.
- Don't invent facts about the user's setup. If the crux depends on something
  you can't see, that *is* the crux question.
- If the honest answer is "it barely matters", say so and recommend moving on.

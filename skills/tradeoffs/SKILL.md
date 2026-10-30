---
name: tradeoffs
description: Surface hidden costs, blind spots, and tradeoffs in technical decisions. Skill is used mid-conversation and needs to evaluate a technical decision, architecture choices, technology selection, implementation approaches, database design, infrastructure decisions, API design, etc. Even if the user seems to have already made up their mind, use this skill to stress-test their reasoning. The goal is to counter default effect, side-effect blindness, absence blindness, and other common decision-making biases that engineers fall into.
---

# Tradeoffs Skill

## Core Biases to Guard Against

Check for these in every analysis (they shape the reasoning, they are not output sections):

1. Default effect — Is the "obvious" or status quo option being favored without scrutiny?
2. Side-effect blindness — What downstream consequences aren't immediately visible?
3. Absence blindness — What option isn't even on the table?
4. Who bears the cost — Does the tradeoff fall on future devs, ops, or users rather than the person deciding now?
5. Reversibility — How hard is this to undo in 6 months? One-way door?
6. Complexity debt — Does this feel simple but quietly add long-term cognitive load?

## Output Format

Keep it tight. Structure every response like this:

Write it in this order. The reader should get the answer in the first line and be able to stop there.

1. The verdict. One line. Your actual lean and the single reason for it. No hedging, no "it depends" as the opener.
2. The because. 2–4 sentences of real reasoning. This is where the bias-guarding lives — name the hidden cost or the overlooked option in plain prose. Don't list, don't label, just think out loud like a senior engineer.
3. The comparison. Two modes — pick based on the decision:

Default to a decision table when the options compete on shared dimensions (cost, lock-in, effort, fit). Rows = options, columns chosen to fit the decision. Always include a reversibility/lock-in column. Keep cells under ~10 words — the constraint forces sharp analysis.

| Option | The real cost | Effort | Locks you in? |
| ------ | ------------- | ------ | ------------- |
| A      | ...           | ...    | ...           |

Fall back to one line per option when the options aren't comparable on a shared axis (different in kind, not degree). Format: Option — the one thing that carries or kills it. Use this when a table would have empty or forced cells.

4. The hinge. Close with the single question that flips the decision, written as if/then. Example: "If the site stays under ~100 pages, either works; past that, chunking wins."

---

## Hard Rules

- Skip the obvious upsides. The user already knows why each option is appealing. Spend words on what they're not seeing.
- Skimmable beats complete. A reader skimming only the bold parts should still get the decision.
- Keep the whole output skimmable. No long prose. If the decision context is thin, ask one clarifying question before analyzing, don't pad with assumptions.

## Framing Challenges

If the framing itself seems off (e.g., the user is asking X vs Y but the real question is whether to do either), add a brief **"Worth questioning"** note at the end. Keep it short — one or two sentences. Don't lead with it unless the framing is clearly wrong.

## Tone

Think senior engineer doing a quick design review — direct, no hand-holding, no false balance. Don't validate both sides equally just to seem neutral. If one option has a clearly worse hidden cost, say so.

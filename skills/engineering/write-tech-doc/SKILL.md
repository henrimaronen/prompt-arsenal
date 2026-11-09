---
name: write-tech-doc
description: Write and improve technical documentation inside a real codebase using the Diátaxis framework's small-step workflow. Read the code and existing docs, classify each piece as tutorial, how-to, reference or explanation, find content in the wrong mode at the sentence level, and ship one verified improvement at a time. Use this whenever the user asks to document code, add or update docs for a feature, clean up or reorganise a docs folder, fix confusing docs, audit documentation, or write a README section, guide or reference page in a repository.
---

# Write tech doc

Diátaxis (Daniele Procida, diataxis.fr) has two halves. One is a **model**: four kinds of documentation for four reader needs. The other is a **way of working**: "small, responsive iterations from which overall patterns emerge" rather than top-down plans. Most applications of the framework keep the model and skip the way of working. This skill uses both, and adds what the framework explicitly leaves out: checking that the docs are *true*.

## The model in one table

| | Reader at study (acquiring skill) | Reader at work (applying skill) |
|---|---|---|
| **Guides action** | **Tutorial**: a lesson. One safe path, visible results, "we". | **How-to**: directions to a goal for a competent user. "If you want x, do y." |
| **Informs cognition** | **Explanation**: discussion answering *why*. Context, trade-offs, opinions. | **Reference**: austere description of the machinery, mirroring its structure. |

Two questions decide the type of any page, section or sentence: **action or cognition? study or work?** Tutorial vs how-to is study vs work, *not* easy vs advanced.

## Workflow

### 1. Orient (do this once per task)

- Find the existing docs (`docs/`, `README*`, `*.md`, docstrings, OpenAPI specs, `--help` text) and the code they describe.
- Note the repo's conventions: file layout, front matter, heading style, docs tooling (MkDocs, Sphinx, Docusaurus and so on). Follow them. Don't impose a new tree.
- If the task covers several pages, make a quick inventory: one line per page, giving its current dominant type and whether it mixes modes. Keep it in your working notes, or show it to the user if they asked for an audit.

### 2. Run the loop

This is Procida's loop, applied to whatever piece the task points at:

1. **Choose** one piece: a page, a section, or a paragraph. If the user named something, that's it. Don't go looking for unrelated problems.
2. **Assess** it with the site's four questions:
   - What user need does this represent?
   - How well does it serve that need?
   - What can be added, moved, removed or changed to serve that need better?
   - Do its language and logic meet the requirements of this mode?
3. **Decide** on the "single next action" that "will produce an immediate improvement here".
4. **Do it** completely, so the change could ship on its own. Then go back to step 1 for the next piece the task needs.

For new documentation, the loop is the same, but step 1 is "the gap". Name the reader need the new page serves, write that one page well, and link it from where readers will look.

When content belongs to a different type, **move it** to a page of the right type (create the page if needed) and leave a link. Don't delete knowledge, and don't leave it in the wrong mode.

### 3. Check for mode drift, sentence by sentence

These phrases show a sentence has drifted into the wrong mode:

| In a... | These signal drift | Usually belongs in |
|---|---|---|
| Tutorial | "Alternatively", "you could also", "there are several ways", background paragraphs, option tables, "In this tutorial you will learn" | explanation / reference / how-to; rewrite the opener as "In this tutorial, we will..." |
| How-to | "Let's", "first we need to understand", history or rationale, full option lists, steps phrased as UI operations without the goal | tutorial / explanation / reference |
| Reference | "we recommend", "you should consider", "the reason is", "best practice", marketing adjectives, step sequences | explanation / how-to |
| Explanation | numbered command steps, parameter tables, exact syntax blocks longer than a few lines | how-to / reference |

A short "because" clause with a link is fine in a tutorial or how-to. A paragraph is not.

### 4. Verify what the docs claim

Diátaxis "cannot address functional quality". It improves fit and flow, not truth. Close that gap yourself:
- Check every name, flag, default, type, path and error message against the source.
- Run tutorial and how-to steps when the environment allows it, and paste the real output. A tutorial "ought to be so well constructed that things can't go wrong."
- Where docs are generated from code, fix the source (docstring, schema, help text) rather than the generated output.
- Anything you couldn't verify gets `TODO(verify): <what>` and a mention in your report.

### 5. Report

Tell the user what changed, which type each touched piece now is, what you verified and how, and the next single improvement you'd make. That last item leaves a clear way to continue without implying the docs are "finished". Diátaxis says docs are never finished, but can always be "complete": useful, right for their stage, and structurally healthy.

## Writing rules per type (short form)

**Tutorial.** The title names a concrete outcome. Open with "In this tutorial, we will...". Each step is an exact action followed by its expected output ("The output should look something like..."). Add "Notice that..." where something is worth seeing, and "If you don't see X, you have probably forgotten Y" where failure is predictable. Never offer options. Explanation is one clause plus a link. End with what we built.

**How-to.** Titled "How to <goal>", never just a noun phrase. Open with "This guide shows you how to...". Action only, written around the reader's goal, with conditional forks. Assume competence. Link to reference for options and to explanation for reasons. Start and end where a real task starts and ends.

**Reference.** Titled with the thing's name. Order and nesting mirror the code (module → class → method; command → subcommand → flag). Use an identical layout across sibling entries: description, signature, parameters, returns, errors, constraints ("You must... Never..."), and one short example. No advice, rationale or narrative.

**Explanation.** The title reads naturally after "About". Anchor it on a why-question and stop once it's answered. Cover context, design decisions, history, constraints, alternatives, and a stated view where it's warranted. Take rationale from ADRs, commits, comments or the user, never from invention. No steps and no option tables.

## Boundaries

- **Don't scaffold empty type folders.** "Don't do that. It's horrible." A four-way top-level split is fine *once there is content to fill it*.
- **Landing pages introduce; they don't just list.** Write a sentence of context per group of links. Keep unordered lists to about seven items. This comes from Procida's earlier, now-removed "complex hierarchies" page.
- **Genres outside the four types:** README, changelog, release notes, quickstart, troubleshooting. Write them in their own genre, but keep the modes separate inside them and link out. For example, a README gives a one-paragraph what-it-is, install, a minimal example, then links to the tutorial, how-tos, reference and explanation. A quickstart must decide whether it's a tutorial (newcomer, one path) or a how-to (expert, fast path).
- **Out of scope:** proposals, design specs, reports and compliance documents (Procida: "they have a different purpose"). Write them without Diátaxis framing.

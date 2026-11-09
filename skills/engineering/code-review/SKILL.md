---
name: code-review-v3
description: 'Review the changes since a fixed point (commit, branch, tag, or merge-base) along four axes: Standards (does the code follow this repo''s documented coding standards?), Spec (does the code match what the originating issue/spec asked for?), Tests (are the automated tests in the diff good tests?), and Edge cases (what situations did the spec never mention and the implementer never notice?). Runs all four reviews in parallel sub-agents and reports them side by side. Use when the user wants to review a branch, a PR, work-in-progress changes, or asks to "review since X".'
metadata:
  version: "3"
  credits: "Matt Pocock"
---

Four-axis review of the diff between `HEAD` and a fixed point the user supplies:

- **Standards**: does the code conform to this repo's documented coding standards?
- **Spec**: does the code faithfully implement the originating issue / spec?
- **Tests**: would the automated tests in the diff fail when the behaviour they cover breaks?
- **Edge cases**: what does the code do in situations the spec never mentions and the implementer likely never considered?

All four axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.

The issue tracker should be known, if this is not the case, default to Github Issue list.

## Process

### 1. Pin the fixed point

Whatever the user said is the fixed point (a commit SHA, branch name, tag, `main`, `HEAD~5`, etc.). If they didn't specify one, ask for it.

Capture the diff command once: `git diff <fixed-point>...HEAD` (three-dot, so the comparison is against the merge-base). Also note the list of commits via `git log <fixed-point>..HEAD --oneline`.

Before going further, confirm the fixed point resolves (`git rev-parse <fixed-point>`) and the diff is non-empty. A bad ref or empty diff should fail here, not inside the parallel sub-agents.

### 2. Identify the spec source

Look for the originating spec, in this order:

1. Issue references in the commit messages (`#123`, `Closes #45`, GitLab `!67`, etc.).
2. A path the user passed as an argument.
3. A spec file under `docs/`, `specs/`, or `.scratch/` matching the branch name or feature.
4. If nothing is found, ask the user where the spec is. If they say there isn't one, the **Spec** sub-agent will skip and report "no spec available". The **Edge cases** sub-agent still runs, against an inferred intent (see step 5).

### 3. Identify the standards sources

Anything in the repo that documents how code should be written, such as `CODING_STANDARDS.md` or `CONTRIBUTING.md`.

On top of whatever the repo documents, the Standards axis always carries the **smell baseline** below: a fixed set of Fowler code smells (_Refactoring_, ch.3) that applies even when a repo documents nothing. Two rules bind it:

- **The repo overrides.** A documented repo standard always wins; where it endorses something the baseline would flag, suppress the smell.
- **Always a judgement call.** Each smell is a labelled heuristic ("possible Feature Envy"), never a hard violation. Like any standard here, skip anything tooling already enforces.

Each smell reads _what it is_ → _how to fix_; match it against the diff:

- **Mysterious Name**: a function, variable, or type whose name doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code**: the same logic shape appears in more than one hunk or file in the change. → extract the shared shape, call it from both.
- **Feature Envy**: a method that reaches into another object's data more than its own. → move the method onto the data it envies.
- **Data Clumps**: the same few fields or params keep travelling together (a type wanting to be born). → bundle them into one type, pass that.
- **Primitive Obsession**: a primitive or string standing in for a domain concept that deserves its own type. → give the concept its own small type.
- **Repeated Switches**: the same `switch`/`if`-cascade on the same type recurs across the change. → replace with polymorphism, or one map both sites share.
- **Shotgun Surgery**: one logical change forces scattered edits across many files in the diff. → gather what changes together into one module.
- **Divergent Change**: one file or module is edited for several unrelated reasons. → split so each module changes for one reason.
- **Speculative Generality**: abstraction, parameters, or hooks added for needs the spec doesn't have. → delete it; inline back until a real need shows.
- **Message Chains**: long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method on the first object.
- **Middle Man**: a class or function that mostly just delegates onward. → cut it, call the real target direct.
- **Refused Bequest**: a subclass or implementer that ignores or overrides most of what it inherits. → drop the inheritance, use composition.

### 4. Identify the test sources

The test files added or changed in the diff, plus anything in the repo that documents how tests should be written, such as `TESTING.md` or a testing section in `CONTRIBUTING.md`.

On top of whatever the repo documents, the Tests axis always carries the criteria in [AUTOMATED_TESTS.md](AUTOMATED_TESTS.md). A documented repo testing convention overrides those criteria, and anything tooling already enforces is skipped.

If the diff touches no test files, the **Tests** sub-agent will skip and report "no tests in diff".

### 5. Identify the edge-case sources

The Edge cases axis carries the criteria in [EDGE_CASES.md](EDGE_CASES.md): a blast-radius step, a nine-category checklist, a freeform pass, and a fixed finding format. It owns only behaviour the spec never mentions; edge cases the spec lists belong to Spec, and test quality belongs to Tests.

This axis always runs. With no spec, the sub-agent infers the change's intent from commits, PR description, and diff, and states it at the top of its report.

### 6. Spawn the sub-agents in parallel

**Standards sub-agent prompt** should include:

- The full diff command and commit list.
- The list of standards-source files you found in step 3, **plus the smell baseline from step 3** pasted in full (the sub-agent has no other access to it).
- The brief: "Report, per file/hunk where relevant, (a) every place the diff violates a documented standard: cite the standard (file + the rule); and (b) any baseline smell you spot: name it and quote the hunk. Distinguish hard violations from judgement calls: documented-standard breaches can be hard, but baseline smells are always judgement calls, and a documented repo standard overrides the baseline. Skip anything tooling enforces. Under 400 words."

**Spec sub-agent prompt** should include:

- The diff command and commit list.
- The path or fetched contents of the spec.
- The brief: "Report: (a) requirements the spec asked for that are missing or partial; (b) behaviour in the diff that wasn't asked for (scope creep); (c) requirements that look implemented but where the implementation looks wrong. Quote the spec line for each finding. Under 400 words."

**Tests sub-agent prompt** should include:

- The diff command and commit list.
- The test files from step 4 and any repo testing docs found, **plus [AUTOMATED_TESTS.md](AUTOMATED_TESTS.md)** pasted in full (the sub-agent has no other access to it).
- The brief: "Report, per test added or changed in the diff, every test that fails the criteria: name the bad-test category (e.g. Tautological, Over-mocked), quote the test, and say which of the three questions it fails. Cite the repo doc (file + the rule) where a documented testing convention is breached; a documented repo convention overrides the criteria. Skip anything tooling enforces. Under 400 words."

**Edge cases sub-agent prompt** should include:

- The diff command and commit list.
- The path or fetched contents of the spec, or "no spec available" plus the commit messages and PR description to infer intent from.
- **[EDGE_CASES.md](EDGE_CASES.md)** pasted in full (the sub-agent has no other access to it).
- The brief: "Find behaviour the spec never mentions that the code must still handle. Ignore edge cases the spec lists (Spec axis) and test quality (Tests axis). First map the blast radius by exploring the repo read-only: callers, consumers, input sources, other writers of the same data, existing stored state. Then walk every checklist category against that picture, then add freeform domain cases. Report at most 5 findings in the EDGE_CASES.md format (scenario, category, `file:line` evidence, verdict Breaks/Undecided, likelihood), ranked Breaks before Undecided and realistic before rare-but-severe, followed by a '+N more in categories …' line if you cut any. Drop anything not tied to a real code path. End with the categories ruled out and why. If there is no spec, open with the inferred intent in 2–3 lines and default findings to Undecided unless the code clearly breaks. Do not run code or create files. Under 400 words."

If the spec is missing, skip the Spec sub-agent; if the diff has no tests, skip the Tests sub-agent. Note either in the final report. The Edge cases sub-agent is never skipped.

### 7. Aggregate

Present the four reports under `## Standards`, `## Spec`, `## Tests`, and `## Edge cases` headings, verbatim or lightly cleaned. Do **not** merge or rerank findings, because the axes are deliberately separate (see _Why four axes_).

End with a one-line summary: total findings per axis, and the worst issue _within each axis_ (if any). Don't pick a single winner across axes: that's the reranking the separation exists to prevent.

## Why four axes

A change can pass one axis and fail another:

- Code that follows every standard but implements the wrong thing → **Standards pass, Spec fail.**
- Code that does exactly what the issue asked but breaks the project's conventions → **Spec pass, Standards fail.**
- Code that is correct and clean but whose tests can't fail (tautological, over-mocked) → **Standards and Spec pass, Tests fail.**
- Code that is clean, matches the spec, and has good tests, but crashes on legacy data nobody mentioned → **Standards, Spec, and Tests pass, Edge cases fail.** Every other axis judges what is on the page; this one looks for what is missing from it.

Reporting them separately stops one axis from masking another.

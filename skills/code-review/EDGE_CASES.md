# Edge cases: review criteria

The target is **WYSIATI** ("What You See Is All There Is"): the implementer built from what the spec said and never asked what it left out. The reviewer is exposed to the same trap: reading only the spec and the diff, it judges them by what is on the page. This file forces looking at what is *not* there.

An edge case here is behaviour the spec never mentions, in situations the code must still handle. Edge cases the spec does list belong to the Spec axis; test quality belongs to the Tests axis.

## Step 1: Blast radius (before the checklist)

For every public function, endpoint, schema, event, or config the diff changes, list:

- **Callers and consumers**: who calls it, who parses its output, what runs downstream.
- **Input sources**: where its inputs come from (users, other services, stored data, queues, config).
- **Other writers**: other entry points that write the same data (cron jobs, webhooks, admin tools, migrations, scripts).
- **Existing state**: data already stored that may not match the new assumptions (legacy rows, old statuses, nulls written before a column became required).

Explore the repo to answer these. Stay read-only: do not run code or create files. Walk the checklist against this wider picture, not just the diff.

## Step 2: Checklist (walk every category)

For each category, ask "does this apply to this change?" If yes, find the code path that decides the outcome.

1. **Input boundaries**: empty, null or missing, zero, negative, max size, unicode or odd encoding, duplicates.
2. **State and lifecycle**: first run with no data, existing or legacy stored data, partially migrated state, deleted or archived entities.
3. **Concurrency and ordering**: double submits, races, retries, events arriving out of order, idempotency.
4. **Failure of dependencies**: timeouts, partial failure midway through a multi-step operation, downstream service down, rollback that does not happen.
5. **Actors and permissions**: other roles, a user without access, a session expiring mid-flow, multi-tenant leakage.
6. **Time**: time zones, DST, month and year ends, clock skew, expiry while in use.
7. **Scale**: one item vs 10k items, pagination, slow paths with large N.
8. **Compatibility**: old clients or API versions, feature flag off, the deploy window when old and new code run side by side.
9. **Environment and locale**: locale formats, mobile vs desktop, offline, configuration that differs between environments.

## Step 3: Freeform

After the checklist, add domain-specific cases it missed: what would someone who knows this domain ask that nobody wrote down?

## Finding format

Each finding has:

- **Scenario**: concrete inputs or state → trigger → what happens. E.g. "User with an existing `draft` order (legacy status, pre-migration) opens checkout → `status` switch falls to `default` → throws 500."
- **Category**: from the checklist, or "freeform".
- **Evidence**: `file:line` of the code path that decides the outcome, plus the caller or data source from the blast radius.
- **Verdict**:
  - **Breaks**: the code fails, corrupts data, or leaks access.
  - **Undecided**: the code does something plausible, but nobody chose that behaviour. Phrase it as a question for the spec owner.
  - **Handled**: not a finding; mention only in the ruled-out list.
- **Likelihood**: *realistic* or *rare-but-severe*.

Drop anything you cannot tie to a real code path. Speculation without evidence is not a finding.

## Ranking and cap

Report at most **5** findings, ranked: Breaks before Undecided, then realistic before rare-but-severe. Summarise the rest in one line: "+N lower-likelihood cases in categories X, Y." Never cut silently: a truncated list that hides its truncation is its own WYSIATI.

## Ruled out

End with the categories that did not apply or were handled, each with a few-word reason. This is the evidence that every category was actually examined.

## No spec

If there is no spec, infer the change's intent from commit messages, the PR description, and the diff. State it in 2–3 lines at the top of the report. Default every finding to **Undecided** unless the code clearly **Breaks**: with no spec, nothing was decided.

# File Naming Guidelines

A file name should say what the file is about and what kind of code it holds, without opening it. Use one casing per repo, follow the language's own conventions where they exist, and never rename files that a framework or tool owns.

---

## 1. Default: kebab-case
Files and folders are lowercase words joined by `-`.

```
playlist-membership.service.ts
generate-mock-data.ts
docs/research/matching-concepts.md
```

Why:
- macOS and Windows filesystems are case-insensitive, so `ListView.tsx` → `listView.tsx` renames break git and CI.
- Works unchanged in URLs, shells, and imports.
- One rule for every file type: `.ts`, `.tsx`, `.css`, `.md`, `.sh`, `.yaml`.

React components are kebab-case too (`triage-card.view.tsx`); the exported symbol stays `TriageCard`.

---

## 2. Language conventions win
Where the language or toolchain defines file names, follow it instead of rule 1.

| Language | Convention | Example |
|----------|------------|---------|
| Python   | `snake_case.py`, tests `test_<module>.py` | `repository.py`, `test_repository.py` |
| Go       | `snake_case.go`, tests `<name>_test.go`, fixtures in `testdata/` | `store_test.go` |
| Java / Kotlin | `PascalCase` matching the public class | `StravaWebhookController.java` |
| Shell    | kebab-case, extension optional for executables on `PATH` | `release.sh`, `gtree` |

---

## 3. Optional: `<domain>.<role>.<ext>`
For larger TypeScript apps, add a role segment so the name also says how the file may be used.

```
triage.service.ts       domain: triage,  role: service
spotify.gateway.ts      domain: spotify, role: gateway
highlight-row.view.tsx  domain: highlight-row, role: view
```

Rules:
- The role vocabulary is a closed list, documented in the repo (`docs/coding-standards.md`). Add a role there before using it.
- Keep it short (5–10 roles). Starter set:

| Role | Contains |
|------|----------|
| `view` | React component for one part of one screen |
| `component` | Reusable UI building block |
| `service` | Orchestrates I/O across stores/gateways |
| `store` / `repo` | Database access behind a typed interface |
| `gateway` / `client` | Talks to one external system |
| `engine` | Pure, deterministic domain logic, no I/O |
| `schema` / `types` | Data shapes and parsers |
| `server` / `client` | Code restricted to one runtime (enforce with tooling where possible) |
| `util` | Small pure helper, named for its domain (`era.util.ts`) |

- Variants trail the role: `spotify.gateway.fake.ts`, `spotify.gateway.real.ts`.
- Don't use roles in Python or Go (dots are invalid in Python module names; Go reserves suffixes).

---

## 4. Name after the domain, not the mechanism
- `owner-session.ts`, not `allowlist-helper.ts`.
- No catch-all buckets: `utils.ts`, `helpers.ts`, `common.ts`, `misc.ts`. Exception: paths a tool generates (e.g. shadcn `lib/utils.ts`).
- If a good name is hard to find, the module boundary is probably wrong.

---

## 5. Tests sit beside the code
| Kind | Name |
|------|------|
| Unit | `<name>.test.ts` |
| Integration (real DB/network) | `<name>.integration.test.ts` |
| End-to-end (Playwright) | `e2e/<flow>.spec.ts` |
| Benchmarks | `<name>.bench.ts` |
| Fixtures | `__fixtures__/` or `testdata/` (Go), kebab/snake-case files |

---

## 6. Framework- and tool-owned names stay as-is
Don't rename these to fit the rules above:
- Routing files: `page.tsx`, `layout.tsx`, `route.ts`, `[id]/`, `(group)/`
- Entry points: `index.ts`, `main.go`, `__init__.py`, `__main__.py`
- Config: `vite.config.ts`, `tsconfig.json`, `.oxlintrc.json`, `pyproject.toml`, `go.mod`
- Infra: `Dockerfile`, `Makefile`, `fly.toml`, `compose.yaml`
- Generated: keep the generator's name (`routeTree.gen.ts`); if you choose the name, mark it with `.gen.` or `.generated.`

`index.ts` marks a package's public API only. Don't add barrel files to every folder.

---

## 7. Ordered files get a sortable prefix
- Migrations: use the migration tool's format (`V3__strava_connections.sql`, `20261005195035_app_meta/`). If you write your own, use `YYYYMMDDHHMMSS_<description>`.
- ADRs: `docs/adr/NNNN-<decision>.md` (`0002-neon-for-postgres.md`).

---

## 8. Markdown and docs
- Root files that agents and GitHub look up by name are UPPERCASE: `README.md`, `AGENTS.md`, `CLAUDE.md`, `CONTEXT.md`, `LICENSE`, `CHANGELOG.md`, `SKILL.md`.
- Everything else, including files in `docs/`, is kebab-case: `docs/coding-standards.md`, not `docs/CODING_STANDARDS.md`.

---

## 9. Enforce it
Put the rules in a linter so they don't drift:
- [`ls-lint`](https://ls-lint.org): works with any language and checks file and folder names.
- Or `eslint-plugin-check-file` in JS/TS repos.

---

## Quick Tests
- Does the name say what domain the file serves?
- Is every file in the repo the same casing, apart from language and framework exceptions?
- Would renaming a single letter's case break anything? (If yes, it isn't kebab-case.)
- Is there a `utils`/`helpers` bucket that should be split by domain?

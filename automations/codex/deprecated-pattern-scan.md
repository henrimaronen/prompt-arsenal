
## Deprecated API & Pattern Migration Scanner

**Purpose**
Continuously detect deprecated APIs, outdated patterns, and migration opportunities within the codebase.

**Description**
This automation runs on a scheduled basis and scans the repository for deprecated APIs, legacy framework patterns, and internally deprecated utilities. It uses a maintained rule set that defines patterns to detect, along with suggested replacements or migration guidance.

The scanner identifies:
- Framework-level deprecations (e.g., outdated rendering APIs)
- Deprecated third-party library usage
- Internal APIs marked as deprecated
- Obsolete architectural patterns

Results are grouped by urgency (Must Migrate, Recommended, Internal Deprecations) and compiled into a structured report. When safe and deterministic, the automation can generate suggested diffs or open a migration pull request with automated replacements.

The goal is to prevent technical debt accumulation, reduce future upgrade friction, and ensure the codebase evolves alongside its dependencies and frameworks.

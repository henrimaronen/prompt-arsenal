## Feature Ideation Automation

**Purpose**
Continuously generate high-quality, context-aware feature ideas based on the current codebase and its documentation.

**Description**
This automation runs on a scheduled basis and analyzes the project's feature documentation, product specifications, README files, changelogs, and relevant architectural notes. It builds an understanding of:

- Existing features and capabilities
- Target users and use cases
- Product positioning and constraints
- Recently shipped improvements
- Stated roadmap goals (if available)

Using this context, the automation identifies gaps, opportunities, and adjacent capabilities that could provide meaningful value to users. Instead of producing generic suggestions, it generates ideas grounded in the actual product scope and technical reality.

Each proposed feature includes:

- **Feature Name**
- **Problem Statement**
- **Target User**
- **Proposed Solution**
- **Why Now (Strategic Rationale)**
- **Expected Impact**
- **Implementation Complexity (Low / Medium / High)**
- **Dependencies or Risks**
- **Suggested First Step (MVP Definition)**

Ideas are grouped into categories such as:
- Incremental Improvements
- Monetization Opportunities
- Retention & Engagement
- Developer Experience
- Automation & Intelligence
- Platform Expansion

The automation may optionally:
- Compare current capabilities against competitor positioning (if configured)

**Output**
The result is a structured "Feature Opportunity Report" delivered as a Markdown document or internal proposal, ready for product review. The report prioritizes ideas based on expected impact and implementation effort, enabling product teams to quickly shortlist candidates.

**Goal**
The goal of this automation is to:

- Prevent product stagnation
- Surface opportunities that teams overlook due to familiarity bias
- Turn documentation into a living strategic asset
- Create a continuous, structured ideation pipeline
- Support product managers with well-framed, actionable proposals

Rather than replacing human product thinking, this automation augments it — acting as a strategic co-pilot that continuously scans for ways to increase user value.

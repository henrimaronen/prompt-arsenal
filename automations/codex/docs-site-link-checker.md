## Docs / Site Link Checker

**Purpose**
Continuously monitor the documentation and marketing site for broken links, structural issues, and obvious content problems.

**Description**
This automation runs on a scheduled basis and crawls the documentation and/or marketing website. It detects broken internal and external links (404s, 500s, DNS errors), redirect chains, missing anchors, and invalid references. It also performs lightweight content checks such as duplicate titles, multiple H1 tags, missing image alt attributes, empty sections, and mixed HTTP/HTTPS resources.

After completing the crawl and validation process, the automation generates a structured fix checklist grouped by severity (Critical, Warning, Suggestion). The report can be published as a Markdown summary, opened as a GitHub issue, or committed as part of a maintenance pull request.

The goal is to ensure content integrity, prevent SEO degradation, and maintain a high-quality developer and customer experience without requiring manual audits.
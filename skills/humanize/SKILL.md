---
name: humanize
description: Defines human-readable output and how to write it. Use whenever writing text a person will read, such as a summary, a plan, or a report.
---

# Human-readable output

## Overview

Write output that is human-readable: text presented concisely, that conveys significant information with minimal cognitive complexity, and can be read and understood quickly.

## Intent first

- Lead with the intent: the goal or purpose, and the problem being solved or the behavior being enabled.
- Follow it with the key points that carry the intent, each framed by why it matters.
- The intent framing replaces a mechanical list of points rather than adding to it.

## Guidelines

- Less is more: write the bare minimum needed to convey the point.
- Separate key points from fine-grained details, and convey only the key points.
- Decide what counts as a key point based on what the reader will need. Describing purely behavior vs referencing code logic is determined based on what is requested.
- Convey each key point in 1-3 sentences.
- Enumerate key points as bulleted or numbered lists, unless a point needs paragraph prose.
- Group many key points under short headings, with each item still held to 1-3 sentences.

## Code examples

- Use a code example only when specifically asked for one, which in practice means a technical summary.
- A code example you write demonstrates the point in the fewest lines possible.
- A code example read from a file keeps only the lines that matter to the key point, marking skipped lines with a comment such as `// ...`.

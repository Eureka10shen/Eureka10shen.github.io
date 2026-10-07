---
name: reviewing-technical-posts
description: Use when reviewing, revising, proofreading, or polishing a mathematical or technical blog post in this repository's _posts directory.
---

# Reviewing Technical Posts

## Overview

Review the requested post for web-safe mathematics and clear academic exposition. Preserve its mathematical meaning and obtain approval before changing the file.

## Workflow

1. Confirm that the requested file is under `_posts/`.
2. Read `README.md` as the authoritative source for Markdown, Kramdown, and MathJax rules. Read the complete post before judging local passages.
3. Review:
   - front matter correctness without changing its existing structure or fields;
   - inline and display math formatting;
   - section order, transitions, and argument flow;
   - notation, terminology, assumptions, equation references, citations, and cross-references for internal consistency;
   - grammar, concision, and academic tone;
   - whether the ending contains a compact, plain conclusion.
4. Preserve claims, definitions, equations, and intended meaning. Do not verify claims against external sources unless the user separately requests it. Flag a suspected substantive error instead of silently correcting it.
5. Report proposed changes using the output contract below, then stop. Do not edit the post until the user explicitly approves.
6. After approval, edit only the requested post and any additional file the user explicitly authorizes.
7. Validate the edited source against `README.md`. Run the repository's available Jekyll build. When feasible, inspect the rendered page to confirm inline formulas and centered display formulas actually render; distinguish completed checks from checks that were unavailable.

## Review Output

Present the pre-edit review in this order:

1. **Required Fixes** — rendering problems, contradictions, undefined notation, broken structure, or missing required metadata. Write `None` if empty.
2. **Recommended Improvements** — meaning-preserving improvements to organization, language, and logic.
3. **Proposed Conclusion** — include a replacement only when the current conclusion is absent or weak. Keep it to one short paragraph covering the problem, main method, and key takeaway.
4. **Approval Request** — state exactly which file would change and wait for approval.

Attach file and line references to findings whenever practical. Separate mathematical-format defects from stylistic preferences.

## Editing Rules

- Keep inline math delimiters tight unless the original notation requires spacing.
- Do not replace standard TeX with renderer-specific workarounds.
- Do not end a display equation between `$$` delimiters with a period or comma. Remove `.` or `,` immediately before the closing `$$`; this rule does not change punctuation in prose or after inline math.
- Preserve the existing front matter structure, field order, and fields. Flag a problem instead of reorganizing or rewriting the header.
- Preserve the `References` section near the beginning of the post. Do not move it to the end or another location.
- Define notation before use and use one symbol for one concept.
- Keep headings descriptive and order sections so prerequisites precede results.
- Prefer concise transitions over repeated summaries.
- Preserve the existing bibliography style and reference placement.
- Do not invent a conclusion that claims more than the post establishes.

## Common Mistakes

- Editing before approval.
- Reorganizing the front matter or relocating the opening `References` section during structural editing.
- Leaving a period or comma at the end of a display equation.
- Treating a successful Jekyll build as proof that MathJax rendered correctly.
- Improving prose while accidentally changing a condition, quantifier, sign, index, or mathematical claim.
- Applying notation rules mechanically without checking their rendered context.
- Adding a long conclusion that repeats the post section by section.

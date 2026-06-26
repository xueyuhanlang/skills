---
name: bib-formatter
description: "Formats, cleans, audits, and standardizes LaTeX .bib files for academic papers."
version: 1.0.0
metadata:
  short-description: "Clean and audit BibTeX files"
  author: "Yang Liu (https://xueyuhanlang.github.io)"
  
---

# BibTeX Formatter and Auditor

Use this skill to clean, standardize, correct, and audit LaTeX bibliography files (`.bib`). The assistant should preserve BibTeX validity, minimize unnecessary changes, and produce a clear audit trail so the author can verify every modification.

This skill is for careful bibliography maintenance, not stylistic rewriting of paper text.

## Core Principles

- Preserve valid BibTeX syntax.
- Preserve comments and human annotations.
- Make the smallest change that fixes the issue.
- Prefer established macros and local bibliography conventions.
- Flag uncertainty instead of inventing missing metadata.
- Keep a detailed revision log for human verification.

## Mandatory Workflow

1. Read the full `.bib` file before editing.
2. Detect existing local conventions:
   - indentation style;
   - field ordering;
   - `@string` macros;
   - capitalization style;
   - URL or `\href` conventions;
   - comment placement.
3. Apply the cleanup rules below.
4. Validate the resulting BibTeX syntax as far as the available tools allow.
5. Produce or update a `bibrev.md` audit log when file edits are made or when the user requests an audit.

## Preservation Rules

- Do not remove, modify, or reposition comments that start with `%`.
- Do not change citation keys unless the user explicitly asks or the key is clearly invalid and unusable.
- Do not remove fields merely because they are uncommon.
- Do not alter protected capitalization inside existing braces unless it is clearly wrong.
- Do not rewrite `\href{url}{text}` content unless the link or displayed title is being intentionally corrected.
- Preserve existing line endings and indentation style when practical.

## Cleanup Rules

### 1. Journal and Conference Abbreviation Mapping

Check the `@string` macro preamble for established short names of journals and conferences, for example:

```bibtex
@string{TOG = "ACM Transactions on Graphics"}
```

Then scan `journal` and `booktitle` fields. If a field exactly or confidently matches an existing macro value, replace the string literal with the macro name without quotes or braces.

Example:

```bibtex
journal = "ACM Transactions on Graphics"
```

becomes:

```bibtex
journal = TOG
```

Do not create new macros unless the user asks.

### 2. Peer-Reviewed Version Audit for Preprints

For entries of type `@misc`, especially arXiv preprints:

- check whether the work has since appeared in a peer-reviewed venue when network access or local metadata is available;
- if a peer-reviewed version is found, report it in `bibrev.md`;
- upgrade the entry type and fields only when the publication match is high confidence;
- preserve the arXiv link or note when it remains useful.

If the match is uncertain, do not upgrade automatically. Flag it for human review.

### 3. Author Name Standardization and Audit

Scan each `author` field.

Apply capitalization fixes only when the correction is obvious:

- `alex liu` -> `Alex Liu`
- `john chen` -> `John Chen`

Flag entries for human review when:

- the author field contains `other`, `others`, or `et al.`;
- initials or particles may be ambiguous;
- names appear machine-truncated;
- author ordering may have been corrupted.

Do not guess missing authors.

### 4. Preservation of Acronyms and Proper Nouns

Title capitalization rules can break technical acronyms, method names, datasets, and proper nouns. Protect case-sensitive terms with braces.

Examples:

```bibtex
3D -> {3D}
CNN -> {CNN}
AI -> {AI}
ResNet -> {ResNet}
PointNet -> {PointNet}
```

Common terms to protect include:

- dimension markers such as `2D`, `3D`, `4D`;
- model names such as `ResNet`, `PointNet`, `NeRF`, `CLIP`, `BERT`, and `GPT`;
- dataset names;
- acronyms such as `CNN`, `GAN`, `SDF`, `RGB`, `RGB-D`, `SLAM`, `AI`, and `ML`;
- proper nouns that BibTeX styles may lowercase incorrectly.

When a term appears inside `\href{url}{text}`, avoid adding nested braces unless necessary and syntactically safe.

### 5. Title Capitalization

Standardize title capitalization only when the target style is clear from the bibliography or user request.

Default target style: academic Title Case.

Rules:

- Capitalize the first word of the title.
- Capitalize the first word after a colon.
- Capitalize nouns, pronouns, verbs, adjectives, and adverbs.
- Lowercase articles, coordinating conjunctions, and short prepositions unless they begin the title or subtitle.
- Preserve protected acronyms and proper nouns with braces.
- Do not change capitalization inside already protected LaTeX groups unless clearly needed.

When the venue or bibliography style expects sentence case, preserve sentence case and only protect required acronyms.

### 6. Duplicate Entry Detection

Detect likely duplicates using normalized title and author fields.

If duplicates are found:

- keep the most complete entry;
- prefer the entry cited by the LaTeX source when source files are available;
- preserve useful fields from removed duplicates when merging is safe;
- report removed or merged keys in `bibrev.md`.

Do not remove a duplicate if the entries may refer to distinct versions, such as a preprint and the final journal version, unless the relationship is clear.

### 7. Link Audit

Check whether entries include a reliable link through one of:

- `doi`;
- `url`;
- `eprint`;
- `archivePrefix`;
- `title` containing `\href`.

For entries without a link:

- look up an official publication page, DOI, project page, or arXiv URL when the user requests link completion and network access is available;
- prefer DOI or publisher pages for peer-reviewed publications;
- prefer arXiv for preprints;
- record missing or uncertain links in `bibrev.md`.

Do not fabricate URLs.

### 8. Required Field Audit

Flag entries with missing or suspicious fields:

- missing `author`;
- missing `title`;
- missing `year`;
- missing `journal` or `booktitle` for published papers;
- inconsistent `pages`, `volume`, `number`, or `doi`;
- suspicious capitalization;
- malformed braces;
- invalid or duplicate citation keys.

## Output Requirements

Adapt the output to the user's request.

### When Editing Files Directly

If the user asks to modify a local `.bib` file or the task clearly implies direct editing:

- update the `.bib` file in place;
- create or update `bibrev.md` beside the `.bib` file unless the user asks for a different location;
- summarize the key changes in the final response;
- mention any entries that require human verification.

### When Returning Text Only

If the user asks for text output rather than file edits, return two clearly labeled Markdown code blocks:

1. **Modified `.bib` File**
   - Include the complete corrected bibliography in one `bibtex` code block.
   - Preserve syntactically valid indentation and trailing commas.
   - Preserve original comments exactly.

2. **`bibrev.md` Revision Log**
   - Include the complete audit log in one `markdown` code block.

## `bibrev.md` Structure

The revision log should contain:

```markdown
# BibTeX Revision Log

## Summary
- Number of entries scanned:
- Number of entries modified:
- Number of entries flagged for review:

## Change Log
- Citation key:
  - Change:
  - Reason:

## Peer-Reviewed Version Audit
- Citation key:
  - Finding:
  - Action:

## Missing Link Audit
- Citation key:
  - Issue:
  - Suggested link:
  - Confidence:

## Incomplete Author Flags
- Citation key:
  - Issue:
  - Required action:

## Duplicate Entry Audit
- Citation keys:
  - Decision:
  - Reason:

## Additional Recommendations
- Citation key:
  - Recommendation:
```

Omit empty sections only when the output would otherwise be noisy.

## Verification Checklist

Before finalizing:

- YAML or BibTeX syntax is not introduced into the `.bib` file accidentally.
- Braces are balanced.
- Entries remain separated cleanly.
- Citation keys are unique.
- Comments are preserved.
- Protected capitalization is syntactically valid.
- Macro replacements use existing `@string` names.
- Every substantive edit is recorded in `bibrev.md`.

## Voice

Use a precise, conservative, audit-oriented voice. Be explicit about uncertainty. Do not overstate verification when links or publication status could not be checked.

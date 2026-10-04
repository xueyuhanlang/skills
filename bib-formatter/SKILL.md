---
name: bib-formatter
description: "Formats, cleans, audits, and standardizes LaTeX .bib files for academic papers."
metadata:
  version: "1.1.0"
  short-description: "Clean and audit BibTeX files"
  author: "Yang Liu (https://xueyuhanlang.github.io)"
---

# BibTeX Formatter and Auditor

Maintain `.bib` files conservatively: preserve valid syntax and local conventions, make the smallest reliable correction, and record substantive changes for human verification. Do not invent metadata or rewrite manuscript prose.

## Workflow and Output

1. Read the full bibliography. Identify indentation, field order, macros, capitalization, links, comments, and the project's BibTeX or biblatex backend.
2. Apply the relevant cleanup rules subject to the preservation constraints.
3. Validate syntax and references as far as available tools and sources allow. State limits; do not imply unchecked publication status or links were verified.
4. Return the output appropriate to the request:
   - **File edit:** update the `.bib` in place and create/update `bibrev.md` beside it unless another location is requested. Summarize key changes and unresolved entries.
   - **Audit only:** leave the bibliography unchanged; return findings and proposed changes in chat unless a saved log is requested.
   - **Corrected text only:** return the complete corrected bibliography in one `bibtex` code block and the complete revision log in one `markdown` code block. Preserve original comments and valid indentation/trailing commas.

## Preservation Constraints

- Do not remove, modify, or reposition `%` comments.
- Preserve `@comment`, `@preamble`, `@string`, and concatenated expressions; do not flatten them during formatting.
- Preserve citation keys unless a change is explicitly requested or a key is clearly invalid and unusable. Apply the reference checks below before removal or renaming.
- Preserve uncommon fields and protected capitalization unless clearly incorrect.
- Preserve `\href{url}{text}` unless intentionally correcting the link or displayed title.
- Preserve line endings and indentation when practical.

## Cleanup Rules

### Journal and Conference Macros

Replace a `journal` or `booktitle` literal with an existing `@string` name only for an exact or confident match. Use the macro bare, without quotes or braces. Do not create macros unless requested.

```bibtex
@string{TOG = "ACM Transactions on Graphics"}
```

With that definition, replace `journal = "ACM Transactions on Graphics"` with `journal = TOG`.

### Preprint Publication Status

For `@misc` entries, especially arXiv preprints, check for a peer-reviewed version when network access or local metadata is available. Report the finding; upgrade type and fields only for a high-confidence match. Preserve useful arXiv links or notes. Flag uncertain matches instead of upgrading.

### Author Names

Fix capitalization only when obvious, e.g. `alex liu` -> `Alex Liu`. Flag `other`, `others`, `et al.`, ambiguous initials/particles, machine-truncated names, or potentially corrupted ordering. Do not guess missing authors.

### Protected Terms and Title Case

Protect case-sensitive acronyms, proper nouns, model names, and datasets:

```text
3D -> {3D}
CNN -> {CNN}
ResNet -> {ResNet}
PointNet -> {PointNet}
```

Other examples include NeRF, CLIP, BERT, GPT, GAN, SDF, RGB-D, SLAM, AI, and ML. Inside `\href{url}{text}`, avoid additional nesting unless necessary and safe.

Normalize title case only when the user or local conventions establish the target. If neither does, preserve case and protect only clearly case-sensitive terms. Preserve sentence case when the venue/style expects it.

For requested academic Title Case: capitalize the first word and the first word after a colon, plus nouns, pronouns, verbs, adjectives, and adverbs. Lowercase articles, coordinating conjunctions, and short prepositions except at the start of the title/subtitle. Do not change existing protected groups unless clearly needed.

### Duplicate Entries and Key References

Detect candidates using normalized titles and authors; confirm they represent the same work before merging.

- Prefer an already cited key and retain the most complete compatible metadata and useful fields.
- Before removing or renaming a key, check available citation commands and bibliography dependencies (`crossref`, `xref`, `xdata`).
- If multiple keys are referenced, retain them unless updating all affected references is explicitly in scope.
- If usage cannot be checked, report duplicates instead of deleting keys.
- Do not merge potentially distinct versions unless their relationship is clear; do not drop attached comments.
- Log removed/merged keys and the reason.

### Links

Check for a DOI, URL, identifiable archive `eprint`, or title containing `\href`. An `archivePrefix` without an `eprint` names an archive, not a work.

For missing links, search only when link completion is requested and network access is available. Prefer DOI/publisher pages for published work and arXiv for preprints; official publication or project pages are also usable. Record missing/uncertain links; never fabricate URLs.

### Required Fields

Use entry-type and backend requirements. An editor-only book may be valid without `author`; biblatex may accept `date` instead of `year`.

For ordinary research papers, check missing author/title/year and journal/booktitle where applicable; inconsistent pages, volume, number, or DOI; suspicious capitalization; malformed braces; and invalid or duplicate keys.

## Revision Log

Record every substantive edit by citation key with its change and reason. Report audit findings in the same structure, but distinguish proposals from applied changes. Omit empty sections when noisy.

```markdown
# BibTeX Revision Log

## Summary
- Entries scanned:
- Entries modified:
- Entries flagged for review:

## Change Log
- Citation key: change; reason.

## Peer-Reviewed Version Audit
- Citation key: finding; action.

## Missing Link Audit
- Citation key: issue; suggested link; confidence.

## Incomplete Author Flags
- Citation key: issue; required action.

## Duplicate Entry Audit
- Citation keys: decision; reason.

## Additional Recommendations
- Citation key: recommendation.
```

## Final Checks

- Valid BibTeX: balanced braces, clean entry separation, and unique keys; no Markdown fences, YAML frontmatter, or audit prose inside the file.
- Comments and protected capitalization preserved; replacements use existing macros.
- Removed/renamed keys leave no unresolved citations or bibliography dependencies in checked sources.
- Every substantive edit logged; unresolved issues and verification limits stated explicitly.

Use a precise, conservative, audit-oriented voice.

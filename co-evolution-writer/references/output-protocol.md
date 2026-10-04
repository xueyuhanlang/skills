# Output and Editing Protocol

Load this reference for rewrites, LaTeX edits, response formatting, bibliography handoff, and TeX verification.

## Writing Preferences

These apply to every rewrite, including Pure Rewrite:

- Use direct, precise, professional prose with clear transitions.
- Preserve meaning, claim scope, terminology, and useful author voice; avoid gratuitous vocabulary changes.
- Remove filler, cliches, slogan sentences, standalone AI aphorisms, and unsupported intensifiers such as "genuinely" or "truly."
- Describe findings rather than slipping into instructional imperatives.
- Avoid excessive em dashes, especially double-em-dash asides.
- Keep each sentence focused without mechanically splitting closely related ideas.

## LaTeX Editing Protocol (Mandatory)

Apply this protocol to LaTeX input or requested LaTeX output. Do not convert plain text or Markdown into LaTeX merely because this reference is loaded.

### Step 1: Revision Notes

Explain consequential changes and their reasons briefly. In Pure Rewrite, omit revision notes unless the mode's critical-warning exception applies.

### Step 2: Revised Text

Provide LaTeX-ready text with added or revised wording wrapped in `\textblue{...}` by default. Leave unchanged text unmarked. If the user explicitly requests clean text, submission-ready text, or no markup, omit revision colors and editorial annotations.

#### Revision Markup

- Mark the smallest coherent changed span, not an entire paragraph unless it has been rewritten throughout.
- Mark warnings and unresolved issues with `\textred{...}`, for example `\textred{[Author check: Supporting evidence has not yet been provided.]}`. Keep them visibly editorial, not part of the scientific argument.
- Do not color an unsupported claim as though it were verified; qualify or remove it and identify the missing evidence.
- Record deletions in revision notes rather than adding strikethrough or retaining rejected text in the manuscript.
- Preserve existing markup during iterative edits; avoid nested or duplicate color wrappers.
- Wrap prose spans only where the macros are syntactically safe. Do not enclose environments, sectioning commands, labels, verbatim content, or display-math delimiters in a text macro. For changes that cannot be safely wrapped, identify their locations in revision notes.
- In Pure Rewrite, return marked revised text without diagnostic blocks. Include a red warning only for a critical issue permitted by that mode; ordinary warnings belong in modes that allow diagnosis.

#### Preamble Setup

Before editing files, inspect the main document's preamble, document class, and included definitions for `\textblue`, `\textred`, and color support. Reuse existing macros without overriding their definitions or changing package options.

If the required macros are missing, add only the missing definitions to the preamble, after color support is available and before `\begin{document}`:

```latex
% Add this package only if the document or class does not already provide color support.
\usepackage{xcolor}

\providecommand{\textblue}[1]{\textcolor{blue}{#1}}
\providecommand{\textred}[1]{\textcolor{red}{#1}}
```

Do not load `xcolor` again if it is already loaded, or add it unnecessarily when existing color support provides `\textcolor`. If the preamble is unavailable, provide this setup as a separate conditional snippet; do not insert package declarations into a section fragment or claim to have checked unseen definitions.

For clean-text output, remove revision wrappers while retaining their text and omit editorial annotations within the requested scope. Do not remove semantic colors, alter unrelated content, or add unused color macros or packages.

### Step 3: Original (Conditional)

Outside Pure Rewrite, show the original text only when:

- the revision is substantial or controversial;
- the author explicitly requests comparison;
- the change alters scientific meaning.

For routine clarity edits, omit the original to reduce clutter.

An explicit comparison request permits showing the original; a substantial rewrite alone does not override Pure Rewrite's text-only output.

## Output Format

Output depth is governed by the active execution mode and Priority Override. The blocks below are available labels, not required headings. Omit empty or redundant blocks and combine related findings when clearer.

### Core Blocks (Always Available)

```text
[Revised Text]

[High-Level Diagnosis]
- real problem
- true contribution
- reviewer concern

[Editor's Note]
- writing improvements
- reasoning lesson for the author (brief unless teaching is prioritized)
```

### Extended Blocks (Conditional)

Use these only when they serve the assessment, including in Full Co-Evolution Pass. Kill-Shot Diagnosis requires submission-readiness assessment, a critical structural weakness, or an explicit rejection-risk request.

```text
[Kill-Shot Diagnosis]
- rejection risk
- core weakness
- what to cut

[Reality Check]
- Problem Reality: R0-R4
- Direction Legitimacy: D0-D4

[Hierarchy Check]
- problem layer
- contribution layer
- assumption layer
- mechanism layer
- evidence layer
- risk layer

[Novelty Profile]
- problem novelty
- representation novelty
- mechanism novelty
- optimization novelty
- systems novelty
- insight novelty
- evaluation novelty
- what is truly central vs. peripheral

[Structure and Story Check]
- opening clarity
- target problem visibility
- impact clarity
- narrative flow
- reader attention / momentum
- where the story weakens

[Technical Note]
- contribution level
- overclaim
- logical gaps
- risks

[Optional]
- alternative framing
- suggested experiments
```

### Suppression Rules

- **Pure Rewrite:** suppress all blocks except revised text (+ optional 1-line note).
- **Quick Pass:** suppress all extended blocks unless a critical issue is detected.
- **Diagnostic Pass:** include only blocks relevant to the diagnosed issues.
- **Full Co-Evolution Pass:** analyze deeply but report selectively; no requirement to include all blocks.
- **Iterative turns:** suppress previously delivered diagnoses unless they change.

## Bibliography

Use the `bib-formatter` skill to polish `.bib` files when it is available.

## TeX Verification

For the edited material and available project context:

- Check balanced revision wrappers, safe contents, required definitions, and distinguishable editorial warnings.
- Check duplicate labels and unresolved references; unused labels alone are not errors.
- Check that relevant mathematical symbols and parameter settings are explained in the main text or appendix.
- Use the project's existing TeX build when available and appropriate. Report what was actually checked; do not claim compilation from visual inspection.

Prefer existing TeX/BibTeX tools for mechanical checks. Do not introduce a generic parser or use a generic script to insert revision colors blindly: includes, custom macros, and scientific meaning require context-sensitive editing.

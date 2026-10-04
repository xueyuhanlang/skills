# Section Guidance

Load this reference when reviewing or revising a specific paper section. Use it together with the diagnostic framework whenever the task includes assessment rather than pure rewriting.

## Iteration Awareness

When working on repeated revisions of the same content:

- Track resolved issues and do not reopen them without new evidence.
- Focus on the next limiting factor and changed findings instead of repeating full diagnoses.
- Shift from structural critique to precision tuning as the draft matures.
- Escalate only if new structural issues emerge.

## Contribution-Level Detection

Levels:

- **Level 1:** incremental.
- **Level 2:** non-trivial improvement.
- **Level 3:** new formulation.
- **Level 4:** foundational.

Use these as rough descriptors, not a universal ranking of research value. Calibrate claims to the demonstrated contribution and evidence; a new formulation is not automatically more valuable than a well-supported improvement.

## Section Guidance

### Title

- Keep the title precise and faithful to the problem, contribution, and demonstrated scope.
- After a Full Co-Evolution Pass, or when requested, suggest a small set of stronger titles with brief reasons if useful. Retain an effective title; defer alternatives when Priority Override requires fixing the scientific framing first.

### Naming Check (Near-Final Manuscript)

When reviewing a nearly complete manuscript for submission, or earlier on explicit request:

- Check proposed method names and acronyms for prior use in papers, methods, datasets, or software. With search tools available, search exact names and common variants; cite relevant matches and explain likely confusion, especially in related fields.
- Flag confusing brand associations and obvious offensive or inappropriate meanings; suggest alternatives where needed. A naming concern is not automatically a legal prohibition.
- If searching is unavailable, mark prior-use checks as unverified. No matches do not establish uniqueness; do not claim legal clearance or exhaustive multilingual screening.

Do not run this check during every Full Pass or Pure Rewrite. Recheck settled names only when they change, new evidence appears, or the user requests it.

### Abstract

Check that the abstract communicates, within its length and venue constraints:

- real problem;
- why it is difficult;
- key idea;
- method;
- evidence;
- takeaway;
- concrete statement of impact.

### Introduction

A useful structure, not a required paragraph sequence:

```text
problem -> limitation -> gap -> insight -> evidence
```

The introduction should:

- state the target problem early;
- clarify why the problem matters;
- reveal the core contribution before excessive detail;
- make the impact legible to a first-pass reader.

Separate:

- core contributions;
- supporting contributions;
- non-contributions.

### Related Work

- First assess whether the section covers the relevant research directions and positions the paper clearly.
- Do not produce a chronological paper list. Organize the discussion by meaningful dimensions such as assumptions, representations, mechanisms, capabilities, or failure modes.
- Clarify which assumptions the paper shares with prior work, which it changes, and how those differences affect capability or scope.
- Check whether comparisons are fair, specific, and necessary for establishing the paper's contribution.

#### External Literature Audit (Explicit Trigger)

Activate only when the user explicitly requests a search for missing or misrepresented related work and external search or retrieval tools are available.

- Search for important omissions, prioritizing foundational work, close technical neighbors, recent developments, and papers that could challenge the novelty or positioning claim.
- Verify central citations against accessible primary sources. Do not judge a paper solely from its title, a search snippet, or another paper's description.
- Check whether the manuscript represents each central work's contribution, assumptions, limitations, and relationship to the current paper accurately and fairly.
- Distinguish among missing literature, inaccurate characterization, weak comparison, and poor organization.
- Clearly separate source-verified findings from plausible leads that still require the author's confirmation.
- State material limits in search coverage or source access; never imply that a bounded search is comprehensive.

The author should remain responsible for writing the final descriptions and comparisons. The skill should audit understanding, challenge positioning, and propose structure rather than replace the author's engagement with the literature.

### Method

For each component:

- What does it do?
- Why is it needed?
- What assumption does it encode?
- Does it support the core mechanism, or is it only auxiliary?

### Experiments

For early drafts, help design evidence for the paper's argument; for mature drafts, evaluate the completed evidence.

- Identify the central hypothesis and a plausible alternative, then propose the smallest useful test that distinguishes them.
- Make expected outcomes conditional: explain what would support, weaken, or leave the claim unresolved, and identify material confounders or controls.
- Keep proposed tests and anticipated results separate from completed observations. Let the researcher decide what to run; do not turn planning into an autonomous experiment loop.

As relevant to the claim, check:

- baselines;
- ablations;
- robustness;
- generalizability;
- efficiency;
- claim-metric alignment;
- evidence coverage for each major claim.

Prioritize suggested experiments as **must-have**, **high-value**, or **optional** when that helps the author decide. Prefer tests that resolve the main uncertainty over a checklist of experiments unrelated to the contribution.

When figures or tables are supplied, assess scientific fidelity: comparability of settings and baselines, axes and encodings, uncertainty where relevant, and whether captions and conclusions match the displayed evidence. Treat missing display information as a reporting gap, not proof of a flawed experiment.

### Conclusion and Future Work

This section should do more than repeat the abstract:

- compress claims to their true level;
- make limitations explicit;
- highlight real unresolved problems;
- be insightful to the community.

#### Conclusion Requirements

The conclusion must:

- restate the core contribution at its true level;
- avoid new claims, interpretations, or scope expansion;
- explicitly reflect:
  - what is achieved;
  - under what assumptions;
  - within what scope;
- include honest qualification.

#### Common Problems to Eliminate

- Repeating abstract-level claims with stronger wording.
- Upgrading contribution without evidence.
- Using vague phrases such as "opens new directions", "broad applicability", or "significant impact" unless justified.

#### Limitations (Mandatory)

Limitations must be explicit and concrete:

- failure cases;
- instability or sensitivity;
- restrictive assumptions;
- computational cost or scalability;
- mismatch with real-world settings;
- aspects not addressed.

Do not:

- hide limitations in vague language;
- dilute them with generic phrasing;
- offset them with optimistic speculation.

A strong paper defines where it fails.

#### Future Work (Strict Rules)

When future work is included, it should:

- derive from actual limitations;
- reflect structural gaps such as representation, ambiguity, modeling limits, optimization barriers, control, interpretability, or robustness;
- remain intellectually honest;
- explain why a proposed extension addresses a real limitation.

Avoid generic extensions, scaling statements, or community trends without a specific unresolved question. Additional datasets or efficiency work can be valuable when they test scope or address a documented bottleneck.

#### High-Level Evaluation

Ask:

- Does the conclusion match the true contribution level?
- Does it reduce rhetorical inflation?
- Does future work reflect real unresolved issues?
- Is the section honest about what is not solved?

#### Strong vs. Weak Future Work

Weak when offered without a research rationale:

- extend to more datasets;
- improve efficiency;
- combine with other models.

Strong:

- identifies a specific limitation;
- connects to a structural problem;
- explains why it is non-trivial.

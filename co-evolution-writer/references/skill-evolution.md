# Skill Evolution Protocol

Load this reference only when a Skill Improvement Note may be warranted.

## Usage-Guided Skill Evolution (Externalized, Strict Scope)

This skill supports co-evolution through reflection, not autonomous scope expansion.

After meaningful interactions, the skill may optionally produce a short **Skill Improvement Note** that is separate from the main writing response.

**How to use `IMPROVEMENT-LOG.md`:**

- `IMPROVEMENT-LOG.md` is a **read-only template** that defines the structure for improvement entries. Do not modify it.
- When a Skill Improvement Note is warranted, propose it separately. Create or append to a log in the working directory (e.g., `improvement-notes.md`) only when the user has requested logging or approved the file action. A writing request alone is not permission to create an extra log.
- Follow the template's sections, including Proposed Edit to Core Skill and Drift Warning when relevant; omit empty sections rather than invent observations.
- Separate entries with a horizontal rule (`---`).
- The author reviews accumulated entries periodically and decides what to promote into the core skill.

**Trigger conditions** — Emit a Skill Improvement Note only if:

- a pattern repeats across ≥2 interactions; OR
- a failure mode significantly impacts output quality; OR
- a missing rule leads to incorrect reasoning.

These are eligibility conditions, not an obligation to emit a note. Suppress notes during Pure Rewrite or when the user requests only manuscript text.

The note should identify:

- recurring user preferences relevant to technical writing;
- recurring failure modes in the interaction;
- missing instructions that would improve future co-evolution;
- candidate refinements to the skill;
- whether the issue appears transient or stable.

Strict rules:

- Do not modify the core mission of the skill.
- Do not expand into generic research assistance, retrieval, project management, or broad productivity support.
- Do not promote one-off user preferences into global rules.
- Only propose an improvement if it clearly strengthens:
  - scientific judgment,
  - technical writing rigor,
  - claim-evidence alignment,
  - mechanism clarity,
  - structure and narrative quality,
  - or the author's learning.

When suggesting an improvement, classify it as:

- **retain as local preference**
- **log for repeated observation**
- **candidate core-skill update**

A candidate core-skill update should be proposed only if:

- it recurs across multiple interactions;
- it aligns with the co-evolution philosophy;
- it does not broaden the skill beyond its intended scope.

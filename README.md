# Co-Evolution Skills

![Version](https://img.shields.io/badge/version-1.1.0-blue) ![License](https://img.shields.io/badge/license-MIT-green)

**Author:** [Yang Liu](https://xueyuhanlang.github.io)

A collection of agent skills for academic research writing and scientific thinking, compatible with any AI agent that supports the open [Agent Skills specification](https://agentskills.io/specification).

## Contents

- [Background](#background)
- [Available Skills](#available-skills)
- [Using `co-evolution-writer`](#using-co-evolution-writer)
- [Using `bib-formatter`](#using-bib-formatter)
- [Installation](#installation)
- [Design Philosophy](#design-philosophy)
  - [Dual-Level Operation](#dual-level-operation)
  - [Diagnosis Before Generation](#diagnosis-before-generation)
  - [Problem Reality](#problem-reality)
  - [Priority Override](#priority-override)
  - [Minimal High-Leverage Intervention](#minimal-high-leverage-intervention)
  - [Honest Positioning over Rhetorical Inflation](#honest-positioning-over-rhetorical-inflation)
  - [Teaching as a First-Class Goal](#teaching-as-a-first-class-goal)
  - [Scope](#scope)
- [Skill Self-Improvement Mode](#skill-self-improvement-mode)

## Background

AI tools for academic research are advancing rapidly. Automated pipelines now assist with idea generation, literature search, method development, experiment implementation, paper writing, and review response — and these capabilities are increasingly hard to ignore.

But automation at every stage carries a quiet cost. When AI handles the reasoning, the researcher stops building it. Problem framing becomes vague because it is never tested under pressure. Contribution claims inflate because no one calibrates them against evidence. Mechanisms get described without anyone asking whether they correspond to a real underlying process. Evaluation grows to cover weaknesses rather than expose them.

The result is not necessarily a weaker paper — reviewers can be fooled, and benchmarks can be won. But the researcher may understand their own work less deeply than they should. Repeated over time, this erodes the scientific judgment that makes original research possible.

Real research quality depends on a researcher's internal model: the ability to distinguish a real problem from a benchmark-constructed one, to identify the actual contribution rather than the most impressive-sounding claim, to recognize when evidence does not support a conclusion. These capacities are built through practice, pressure, and honest feedback — not through outsourcing.

Most academic AI tools today work in the opposite direction. They draft complete papers, simulate peer review panels, and orchestrate the entire pipeline end to end. The researcher provides a topic; the agent produces output. These tools can be useful for narrow tasks, but they automate exactly the steps where scientific judgment is formed.

This is the gap these skills address. Based on my multi-year research experience and daily use of AI for writing and thinking, I built them to use AI as a genuine co-pilot: a partner that sharpens reasoning rather than replacing it, identifies what is actually wrong before rewriting, and transfers judgment rather than just text.

The name *co-evolution* is deliberate: every interaction should make both the paper and the researcher stronger.

---

## Available Skills

| Skill | Description |
|-------|-------------|
| [co-evolution-writer](./co-evolution-writer/) | A senior academic co-writer that sharpens scientific reasoning and paper quality through diagnosis-first critique. |
| [bib-formatter](./bib-formatter/) | Cleans and audits BibTeX with conservative edits and explicit revision logs. Preserves syntax, local conventions, and comments. |

---

## Using `co-evolution-writer`

Use when you need scientific co-writing support, not just editing. It provides feedback that is honest and sometimes uncomfortable — it will tell you what is actually wrong, not what you want to hear.

**Best for:**
- abstract/introduction framing
- contribution calibration
- method clarity
- claim–evidence consistency
- submission-risk diagnosis

**Mode guide:**

| Mode | When to use |
|------|-------------|
| Quick Pass | Local edits with brief warnings |
| Pure Rewrite | Revised text only, claim scope unchanged |
| Diagnostic Pass | Medium-depth diagnosis plus targeted edits |
| Full Co-Evolution Pass | Full hierarchy, risk, and teaching-oriented critique |

**Recommended prompts:**
```text
Run a Diagnostic Pass on this introduction. Identify the main framing weakness and rewrite only the key paragraph.
Do a Full Co-Evolution Pass on this draft and prioritize the biggest rejection risk first.
Pure rewrite only for this paragraph; keep the claim scope unchanged.
```

**Recommended workflow and tips:**
- Start with a **Full Co-Evolution Pass** (even on an incomplete draft). The core issues it surfaces tend to be accurate and uncomfortable — worth sitting with, rethinking, and fixing before moving to rewrites. Use targeted passes afterward to refine writing and sharpen reasoning incrementally.
- **Write the draft yourself first.** Use AI to interact with what you wrote — to identify framing weaknesses, calibrate contribution level, and surface what you may be wrong about. *The draft is yours; the AI is a critic, not a ghostwriter.*
- **Write related work yourself.** You may use AI to surface references you were unaware of, but write the descriptions and comparisons yourself. Then use AI to validate or debate your understanding of existing work and your positioning against it. Well-written related work — like that in many SIGGRAPH papers — builds field knowledge that stays with you; AI-generated summaries rarely do.
- **Try it on a published paper.** If you want to calibrate the skill's judgment against your own, run a Full Co-Evolution Pass on a paper you have already published (provide the LaTeX source). Seeing what it finds in work you already know well is instructive.

*Note: This README is itself improved with `co-evolution-writer`.*

---

## Using `bib-formatter`

Use when maintaining a `.bib` file for correctness, consistency, and traceability.

**Best for:**
- field normalization and capitalization protection
- macro-aligned journal/booktitle cleanup
- duplicate detection and merge decisions
- missing-link and incomplete-metadata audits

**Working style:**
- Preserves BibTeX validity, comments, and local conventions
- Makes the smallest reliable change; does not invent metadata
- Flags uncertainty explicitly rather than guessing
- Keeps a human-verifiable revision log (`bibrev.md`)

**Typical use:**
1. Ask for a conservative cleanup pass.
2. Review flagged uncertainties and duplicate decisions.
3. Keep or update `bibrev.md` as a compact audit trail.

---

## Installation

### Option A — GitHub CLI (recommended, requires `gh` v2.90.0+)

The `--agent` flag routes the skill to the correct directory for your agent:

```sh
# GitHub Copilot (default)
gh skill install xueyuhanlang/skills co-evolution-writer --scope user
gh skill install xueyuhanlang/skills bib-formatter --scope user

# Claude Code
gh skill install xueyuhanlang/skills co-evolution-writer --agent claude-code --scope user
gh skill install xueyuhanlang/skills bib-formatter --agent claude-code --scope user

# Gemini CLI
gh skill install xueyuhanlang/skills co-evolution-writer --agent gemini --scope user
gh skill install xueyuhanlang/skills bib-formatter --agent gemini --scope user

# Codex
gh skill install xueyuhanlang/skills co-evolution-writer --agent codex --scope user
gh skill install xueyuhanlang/skills bib-formatter --agent codex --scope user
```

Or browse interactively:
```sh
gh skill install xueyuhanlang/skills
```

### Option B — Manual

Clone the repo and copy skill folders to your agent's skills directory:

| Agent | Mac / Linux | Windows |
|-------|-------------|---------|
| GitHub Copilot | `~/.copilot/skills/` | `%USERPROFILE%\.copilot\skills\` |
| Claude Code | `~/.claude/skills/` | `%USERPROFILE%\.claude\skills\` |
| Gemini CLI | `~/.gemini/skills/` | `%USERPROFILE%\.gemini\skills\` |
| Universal | `~/.agents/skills/` | `%USERPROFILE%\.agents\skills\` |

**Mac / Linux:**
```sh
git clone https://github.com/xueyuhanlang/skills.git
TARGET_DIR=~/.copilot/skills   # adjust for your agent (see table above)
cp -r skills/co-evolution-writer $TARGET_DIR/
cp -r skills/bib-formatter $TARGET_DIR/
```

**Windows (PowerShell):**
```powershell
git clone https://github.com/xueyuhanlang/skills.git
Copy-Item -Recurse skills\co-evolution-writer "$env:USERPROFILE\.copilot\skills\co-evolution-writer"
Copy-Item -Recurse skills\bib-formatter "$env:USERPROFILE\.copilot\skills\bib-formatter"
```

After install, reload inside your agent session — `/skills reload` works for Copilot CLI, Claude Code, and Gemini CLI.

### Verifying Installation

```sh
/skills info co-evolution-writer
/skills info bib-formatter
```

### Invoking Skills

The agent picks up a skill automatically when your prompt matches its purpose. To invoke explicitly:

```sh
/co-evolution-writer
/bib-formatter
```

### Updates

```sh
gh skill update --all
```

---

## Design Philosophy

> *Co-evolve the researcher's judgment, not just the manuscript.*

### Dual-Level Operation

The skill operates simultaneously at two levels:

- **High-level field reasoning** — problem legitimacy, representation assumptions, positioning, real contribution, paper structure, and story clarity.
- **Low-level technical rigor** — correctness in math, formulation, implementation, and evaluation.

Polishing words while preserving weak positioning is a waste of effort. Structure and logic take priority over surface clarity.

### Diagnosis Before Generation

Structural weaknesses are diagnosed before any rewriting begins. Local fixes applied to a broken framing make the paper worse, not better.

The skill asks first:
- Is the problem real, or constructed from benchmarks and trends?
- Is the contribution identified correctly, or buried under implementation details?
- Is the idea → method → evidence chain intact?
- What is the single change that would most improve this paper?

### Problem Reality

A benchmark or dataset does not justify a problem. The skill evaluates whether a problem exists outside the paper and is motivated by genuine need — not convenience or trend. Problems with low reality require claim narrowing and honest repositioning, not stronger rhetoric.

### Priority Override

When one issue dominates paper quality — an invalid problem, incorrect claim, broken mechanism, or missing evidence — everything else is deferred. The skill diagnoses that issue first, with at most one or two secondary notes.

This mirrors how strong advisors behave: identify the one thing that matters most, not produce twenty comments.

### Minimal High-Leverage Intervention

The focus is the smallest intervention that resolves the core issue — the structural problem, not all observable symptoms. What is already working is left alone.

### Honest Positioning over Rhetorical Inflation

Contribution claims are calibrated to the evidence, not to the ambition of the framing. Claims that outrun what the method actually shows are corrected. Scientific work should stand on clarity, correctness, and evidence.

### Teaching as a First-Class Goal

When making a strong critique, the skill explains the structural reason, exposes the faulty assumption, and teaches the general principle. Each critique is aimed at both the current draft and the reasoning behind it.

Teaching depth is calibrated:
- **Structural or repeated issues** → full explanation with a reusable principle.
- **Local or minor issues** → brief note embedded in revision.
- **Late-stage polishing** → minimal explanation; focus on iteration speed.

### Scope

This skill is intentionally narrow. It does not handle **reviewer-politics optimization**, **autonomous research pipelines**, **literature retrieval**, or **generic writing assistance** — these are outside co-evolution-writer's own scope.

In practice, agents running this skill may have access to other tools or skills (web search, retrieval, bib-formatter) and can perform those tasks when explicitly instructed. That is fine — but treat them as separate steps. Do the external work, then bring the result back to co-evolution-writer for evaluation: critique the positioning, assess the evidence, check the reasoning. The skill evaluates what you bring to it; it does not conduct research on your behalf.

---

## Skill Self-Improvement Mode (For Advanced Users)

`co-evolution-writer` includes a built-in mechanism for evolving its own instructions from real usage. This is an advanced feature the author uses to upgrade the skill over time.

### How It Works

After a meaningful interaction, the skill may produce a **Skill Improvement Note** — written separately from the main response — capturing:

- recurring patterns in what was useful or ineffective;
- failure modes observed during the interaction;
- missing instructions that would improve future co-evolution;
- candidate refinements, classified by stability.

Notes follow the structure defined in `IMPROVEMENT-LOG.md` (a read-only template included in the skill) and are appended to `improvement-notes.md` in the working directory — never written to the core skill directly.

### Trigger Conditions

A note is emitted only if:
- a pattern repeats across ≥2 interactions, **or**
- a failure mode significantly impacts output quality, **or**
- a missing rule leads to incorrect reasoning.

Otherwise it is suppressed — high-quality signal matters more than frequent output.

### Candidate Classifications

| Classification | Meaning |
|----------------|---------|
| `local preference` | Specific to the current user or context; not a global rule |
| `log for repeated observation` | Potentially useful but needs more evidence |
| `candidate core-skill update` | Recurring, scope-aligned, and justified for promotion |

A candidate update is only proposed if it recurs across multiple interactions, aligns with the co-evolution philosophy, and does not broaden the skill beyond its intended scope.

### The Promotion Cycle

The author reviews accumulated `improvement-notes.md` entries periodically and decides which candidates to promote into `SKILL.md`. This is the loop that has driven the skill from draft to its current state — every promoted change validated through actual co-evolution sessions.

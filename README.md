# Co-Evolution Skills

> **We do not learn to surpass others or AI. We learn to transcend our own limitations and deepen our understanding of the world.**
>
> 为学非为争先，乃为拓己之未至，见所未见，知所未知。

![Version](https://img.shields.io/badge/version-1.2.0-blue) ![License](https://img.shields.io/badge/license-MIT-green)

**Author:** [Yang Liu](https://xueyuhanlang.github.io)

A collection of agent skills for academic research writing and scientific thinking, compatible with any AI agent that supports the open [Agent Skills specification](https://agentskills.io/specification).

## Contents

- [Background](#background)
- [Available Skills](#available-skills)
- [Using `co-evolution-writer`](#using-co-evolution-writer)
- [Using `co-evolution-idea`](#using-co-evolution-idea)
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
- [Skill Self-Improvement Mode](#skill-self-improvement-mode-for-advanced-users)

## Background

AI tools for academic research are advancing rapidly. Automated pipelines now assist with idea generation, literature search, method development, experiment implementation, paper writing, and review response — and these capabilities are increasingly hard to ignore.

But automation at every stage carries a quiet cost. When AI handles the reasoning, the researcher stops building it. Problem framing becomes vague because it is never tested under pressure. Contribution claims inflate because no one calibrates them against evidence. Mechanisms get described without anyone asking whether they correspond to a real underlying process. Evaluation grows to cover weaknesses rather than expose them.

The result is not necessarily a weaker paper — reviewers can be fooled, and benchmarks can be won. But the researcher may understand their own work less deeply than they should. Repeated over time, this erodes the scientific judgment that makes original research possible.

Real research quality depends on a researcher's internal model: the ability to distinguish a real problem from a benchmark-constructed one, to identify the actual contribution rather than the most impressive-sounding claim, to recognize when evidence does not support a conclusion. These capacities are built through practice, pressure, and honest feedback — not through outsourcing.

Most academic AI tools today work in the opposite direction. They draft complete papers, simulate peer review panels, and orchestrate the entire pipeline end to end. The researcher provides a topic; the agent produces output. These tools can be useful for narrow tasks, but they automate exactly the steps where scientific judgment is formed.

This is the gap these skills address. Based on my multi-year research experience and daily use of AI for writing and thinking, I built them to use AI as a genuine co-pilot: a partner that challenges reasoning rather than replacing it, helps identify weaknesses before rewriting, and explains its judgments rather than just producing text.

The name *co-evolution* is deliberate: the aim is to improve the work while helping the researcher develop stronger judgment. That is a design goal, not a guarantee that the agent's advice is correct.

---

## Available Skills

| Skill | Description |
|-------|-------------|
| [co-evolution-writer](./co-evolution-writer/) | A senior academic co-writer that sharpens scientific reasoning and paper quality through diagnosis-first critique. |
| [co-evolution-idea](./co-evolution-idea/) | Helps develop research ideas into testable questions and keeps the reasoning in durable notes. |
| [bib-formatter](./bib-formatter/) | Cleans and audits BibTeX with conservative edits and explicit revision logs. Preserves syntax, local conventions, and comments. |

---

## Using `co-evolution-writer`

Use when you need scientific co-writing support, not just editing: framing a contribution, explaining a method, planning experiments, checking evidence, or assessing submission readiness. It challenges what may be wrong and explains its reasoning; its advice still needs your judgment.

**Mode guide:**

| Mode | When to use |
|------|-------------|
| Quick Pass | Local edits with brief warnings |
| Pure Rewrite | Revised text only, claim scope unchanged |
| Diagnostic Pass | Medium-depth diagnosis plus targeted edits |
| Full Co-Evolution Pass | Deep assessment focused on the most important findings |

**Recommended prompts:**
```text
Run a Diagnostic Pass on this introduction. Identify the main framing weakness and rewrite only the key paragraph.
Do a Full Co-Evolution Pass on this draft and prioritize the biggest rejection risk first.
This is an early draft with no results yet. Identify the central hypothesis and the smallest experiment that could distinguish it from a plausible alternative.
```

**Recommended workflow and tips:**
- Start with a **Full Co-Evolution Pass** for a broad review, then use targeted passes to refine the draft. Judgments based on missing context remain provisional. In early drafts, use the review to plan evidence, not to treat untested hypotheses as results.
- **Write the draft yourself first.** Use AI to interact with what you wrote — to identify framing weaknesses, calibrate contribution level, and surface what you may be wrong about. *The draft is yours; the AI is a critic, not a ghostwriter.*
- **Write related work yourself.** On request, the agent can search for missing work and check central citations against accessible primary sources. Use that help to examine your comparisons, not replace your reading.
- **Review LaTeX changes in color.** Revised wording is blue; unresolved author checks are red. Ask for clean text to omit revision markup and editorial annotations.
- **Try it on a published paper.** If you want to calibrate the skill's judgment against your own, run a Full Co-Evolution Pass on a paper you have already published (provide the LaTeX source). Seeing what it finds in work you already know well is instructive.

*Note: This README is itself improved with `co-evolution-writer`.*

Title suggestions, near-final naming checks, and editing conventions are described in the [writer instructions](co-evolution-writer/SKILL.md) and their references.

---

## Using `co-evolution-idea`

Use when you want to work through a rough research idea or preserve useful thinking in a note. It helps clarify the problem, question the key assumption, and find a useful next test without taking over the idea.

Formerly `co-evolution-note`, it retains literature, meeting, experiment, synthesis, and quick-capture notes. Asking to organize a thought does not automatically invite a full critique or research proposal. A thinking conversation need not end in a note.

Your reasoning stays separate from AI suggestions, and uncertainty is preserved rather than polished away. Before creating or changing note files, the agent proposes the structure and location for your approval.

**Recommended prompts:**
```text
Turn this AI conversation into a durable research note. Separate verified facts from suggestions that need checking.
Structure these meeting notes, preserving decisions, rationale, disagreements, and research implications.
Help me examine the main assumption behind this idea and choose one small test. Do not turn it into a full proposal yet.
```

---

## Using `bib-formatter`

Use for conservative bibliography cleanup: capitalization, venue macros, duplicates, missing links, and incomplete metadata. It preserves comments and local conventions, checks citation usage before removing keys, and records edits in `bibrev.md`.

Ask for a cleanup or an audit-only pass, then review uncertain entries and merge decisions. Unlike the two co-evolution skills, this is a focused maintenance tool.

---

## Installation

You can ask your AI agent to install the skills:

```text
Install co-evolution-writer, co-evolution-idea, and bib-formatter from
https://github.com/xueyuhanlang/skills for this agent at user scope.
Include all supporting files, and ask before replacing existing skills.
```

Or use a recent GitHub CLI with `gh skill` support:

```sh
gh skill install xueyuhanlang/skills --all --scope user
```

This installs all three for GitHub Copilot. For another agent, add `--agent claude-code`, `--agent gemini-cli`, or `--agent codex`. To install just one skill, replace `--all` with its name.

For manual installation, download or clone this repository and copy the complete skill folders into your agent's documented skills directory. Keep supporting files, including the writer's references.

Reload skills or restart your agent after installation. In Copilot CLI, use `/skills reload` and `/skills info co-evolution-writer` to check. Skills can be selected automatically from your request; you can also invoke them explicitly with `/co-evolution-writer`, `/co-evolution-idea`, or `/bib-formatter` in Copilot CLI.

If you installed `co-evolution-note` previously, install `co-evolution-idea` and remove or disable the old skill after preserving any local customizations. Updating alone may not remove the old installation.

### Updating

Updates are manual; the skills do not check for new versions during use. For CLI-managed installations:

```sh
gh skill update --all
```

This updates all skills managed by `gh`, not just this collection. To try the development branch instead:

```sh
gh skill install xueyuhanlang/skills --all --scope user --pin dev
```

Preserve local customizations before updating. For manual installations, pull or download the desired version and copy the complete skill folders again. You can also ask your agent to help update them, then reload skills or restart the session.

---

## Design Philosophy

> *Co-evolve the researcher’s judgment, taste, and capabilities—not just another manuscript.*

This philosophy guides both `co-evolution-writer` and `co-evolution-idea`. The writer examines a paper's argument and evidence; the idea skill helps develop questions and preserve the reasoning behind them.

Challenge the AI's suggestions—and the guidance in these skills—with the same care you apply to your own claims. Ask what evidence supports a recommendation, whether its assumptions fit your work, and when it should be rejected or revised. Developing that independent judgment is one of the goals of co-evolution, not an obstacle to using AI well.

### Dual-Level Operation

Both skills connect the larger research question to the details that support it:

- **High-level reasoning** — whether the problem matters, what the idea contributes, and how it relates to existing work.
- **Technical rigor** — whether the assumptions, derivations, observations, and experiments support the interpretation.

Polished prose or a tidy note should not hide a weak argument.

### Diagnosis Before Generation

Before developing an idea or revising an argument, the agent should understand the purpose and identify the main reasoning gap. Local edits cannot resolve an unsupported conclusion. Pure Rewrite and quick capture remain available when you need a narrow task rather than a discussion.

### Problem Reality

A benchmark or dataset alone does not justify a problem. Both skills question whether a direction addresses a genuine need rather than convenience or trend. Early ideas may need a clearer question; mature papers may need narrower claims, not stronger rhetoric.

### Priority Override

When one issue dominates—an unclear problem, unsupported claim, hidden assumption, or missing evidence—the agent should concentrate on that issue rather than bury it among minor comments.

This mirrors how strong advisors behave: identify the one thing that matters most, not produce twenty comments.

### Minimal High-Leverage Intervention

The focus is the smallest intervention that resolves the core issue: a better test, a clarified assumption, or a targeted edit. What is already working is left alone; a request to organize a note should not become a research proposal.

### Honest Positioning over Rhetorical Inflation

Claims should match the evidence, not the ambition of the framing. A promising idea is not yet a demonstrated contribution, and an AI suggestion is not the researcher's established conclusion. The agent's own critiques need the same discipline.

### Teaching as a First-Class Goal

An explanation or a focused question is useful when it helps the researcher make a better decision next time. Structural and recurring problems deserve more discussion than routine wording changes. Co-evolution does not require a lesson or an interview in every interaction.

### Scope

These skills are not designed to maximize paper acceptance or tell authors what "Reviewer 2" wants to hear. They should help address valid criticism and challenge unsupported objections, not tailor claims to reviewer preferences or make weak evidence sound convincing.

The longer-term goal of co-evolution is to develop the researcher's own taste and scientific values: a sense of which questions are worth pursuing, what counts as convincing evidence, and when to revise a belief or narrow a claim. Those judgments should become more independent—not more dependent on approval from an AI or a reviewer.

Neither co-evolution skill is an autonomous research pipeline or a project manager. Literature retrieval is a separate, explicitly requested step; the writer also supports a limited prior-name search near submission. Interpretation, experimental decisions, and final claims remain the researcher's responsibility.

---

## Skill Self-Improvement Mode (For Advanced Users)

The writer may suggest an improvement note when repeated use or a significant failure reveals a problem with its instructions. Notes are optional, saved only when requested or approved, and never change the skill automatically. The author decides which observations justify a lasting change.

See the [skill-evolution protocol](co-evolution-writer/references/skill-evolution.md) and [read-only log template](co-evolution-writer/IMPROVEMENT-LOG.md) for the details.

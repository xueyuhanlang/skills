# Diagnostic Framework

Load this reference for diagnosis, critique, reviewer-comment assessment, or scientific evaluation. Use its reasoning checks where relevant; do not turn them into mandatory output sections.

## Core Execution Rules

### 0. Global Understanding (Adaptive)

- If full paper or multiple sections are provided: build a strong global model before editing.
- If only partial context is available: build a **local-global approximation**:
  - infer the likely role of the fragment;
  - identify dependencies on unseen sections;
  - mark global assumptions explicitly.

Do not delay useful local improvements due to missing global context.

Distinguish draft maturity from input completeness. In an early draft, treat untested claims as hypotheses and turn important evidence gaps into proposed tests, not automatic submission-level faults. Still flag claims written as established results without support. In a mature draft, assess the evidence actually obtained; planned experiments never count as completed support.

When sufficient context exists:

- infer the real problem, scope, assumptions, core idea, and contribution level;
- identify the most consequential scientific concern;
- identify what the author may be misunderstanding about their own work;
- evaluate whether the paper structure supports fast comprehension of the main problem and contribution.

### 0.1. Partial-Context Rule (Mandatory)

If the user provides only a fragment (paragraph, single section, or incomplete draft):

- Do **not** pretend to have a full global model.
- Explicitly state:
  - what can be assessed locally with confidence;
  - what requires more context for reliable judgment;
  - which diagnoses are provisional and may change with full-paper context.
- Proceed with best-effort local editing, but label uncertain judgments.
- Do not refuse to help; do not hallucinate missing context.
- If a serious issue is visible even locally, flag it clearly.

#### False Precision Guard (Mandatory)

Avoid presenting inferred structure, contribution, or intent as certain when evidence is incomplete.

Distinguish:
- explicit in text
- strongly implied
- speculative inference

Rules:
- Label speculative interpretations clearly.
- Do not refine ambiguity into artificial precision.
- Prefer exposing uncertainty over resolving it prematurely.

### 0.2. Adaptive Teaching

Control how much reasoning explanation is provided, balancing learning value with iteration speed.

Determine teaching depth based on issue type and interaction stage:

**When to TEACH (expand reasoning):**
- structural issues (problem, contribution, assumptions, mechanism)
- repeated errors across turns
- incorrect mental model or overclaim
- misalignment between claim and evidence
- when the author would benefit from a reusable principle

**When to MINIMIZE teaching (stay concise):**
- local clarity or wording improvements
- one-off minor issues
- late-stage polishing iterations
- when teaching would not change future decisions

**Teaching Levels:**
- **Full:** explain underlying principle and generalizable reasoning
- **Focused:** brief explanation tied to the current issue
- **Minimal:** no explicit teaching; fix only

**Rules:**
- Default to **Focused** teaching.
- Escalate to **Full** only when it improves the author's future reasoning.
- De-escalate to **Minimal** when iteration speed is more valuable than explanation.
- Do not repeat the same teaching across turns once learned.
- Prefer embedding teaching inside revision notes rather than long standalone blocks.
- If a dominant issue exists (Priority Override), prioritize teaching that issue only.
- When a central ambiguity or recurring weakness warrants active reasoning, ask one focused question that helps the author examine the premise or evidence before supplying an interpretation. Skip it if the answer would not change the assessment; do not impose an interview or interrupt Pure Rewrite.

### 0.3. Reviewer Comment Evaluation (Mandatory when assessing received reviews)

When the user provides received reviewer comments for assessment, apply the same critical hierarchy used for paper claims. Do not treat reviewer authority as a substitute for evidence.

For each reviewer comment, classify it before advising revision:

- **Valid:** The comment identifies a genuine error, missing information, or reproducibility gap that can be verified against the paper content.
- **Notation/Presentation:** The paper's implementation may be correct but the exposition is unclear. The fix is clarification, not correction.
- **Debatable:** The comment asserts a field convention, terminology preference, or standard practice. Verify independently. If the paper's usage is defensible by existing literature, flag the disagreement and suggest a response rather than compliance.
- **Weak:** The comment is unsubstantiated, reflects personal taste, or contradicts the paper's actual content. Flag explicitly.

Specific rules:
- Never accept a reviewer's claim about field terminology or standard practice without cross-checking against the paper's existing usage and field knowledge.
- Distinguish between "the algorithm is wrong" and "the notation does not make the algorithm explicit." These require different responses.
- Reviewer claims about what "should" be done (formula form, method choice, notation style) require the same evidence standard as paper claims.
- When a reviewer comment is classified as Debatable or Weak, draft a response that defends the paper's position with evidence, rather than recommending blind compliance.

Throughout critique, distinguish an unreported detail from a demonstrated error. A reporting gap may prevent assessment or reproduction without proving that the underlying method is invalid. State what is missing, what conclusion it prevents, and what would resolve it.

### 0.4. High-Level Mode

Always ask:

- What structural limitation is being addressed?
- What assumption or representation is challenged?
- Is this a structural problem or a local symptom?
- Does the method matter beyond the paper setup?
- Does the paper state the target problem early and clearly?
- Is the impact of the work made explicit rather than implied?
- Does the narrative keep reader attention by moving cleanly from problem -> limitation -> insight -> evidence?

### 0.5. Problem Reality and Direction Legitimacy

- Does it exist outside this paper?
- Is it motivated by a real need or constructed from benchmarks/trends?
- Would it matter without current models or datasets?

Problem Reality Level (R):

- **R0:** fabricated / paper-only.
- **R1:** weak / convenience-driven.
- **R2:** real but narrow.
- **R3:** clearly real.
- **R4:** foundational.

Direction Legitimacy (D):

- **D0:** method-looking-for-problem.
- **D1:** weakly justified.
- **D2:** reasonable but limited need.
- **D3:** clearly justified.
- **D4:** deeply meaningful.

Use these levels as qualitative aids, not objective scores or acceptance predictions. Missing motivation in a fragment is not evidence that the underlying problem is unreal. Low levels require narrow claims and honest repositioning when supported by sufficient context.

### 0.6. Benchmark Skepticism

A benchmark or dataset does not justify a problem. Ask:

- Would the problem matter without this dataset?
- Does it exist beyond current trends?

#### Benchmark Illusion Escalation

If a problem is benchmark-driven:

- Re-evaluate:
  - Problem Reality (R)
  - Direction Legitimacy (D)
  - Contribution Level

- If Problem Reality ≤ R1:
  - enforce claim narrowing
  - prevent generalization claims

Explicitly state when applicable:
"This contribution may not transfer beyond the current benchmark."

### 0.7. Kill-Shot Diagnosis

Use Kill-Shot Diagnosis only when:

- evaluating a section for submission-readiness;
- a critical structural weakness is detected;
- the user requests rejection-risk assessment.

Avoid repeating kill-shot framing in early-stage drafting or iterative refinement.

When activated, identify:

- primary rejection risk;
- core intellectual weakness;
- what should be removed instead of fixed.

Be frank and evidence-based. Strong critiques should remain precise, respectful, and constructive.

### 0.8. Hierarchical Reasoning (Mandatory)

Reason hierarchically before making local edits. Build an internal model of the paper using these layers:

1. **Problem Layer**
   - What real problem is being solved?
   - What makes it difficult?
   - What prior structural limitation exists?

2. **Contribution Layer**
   - What is the core contribution?
   - What is enabling but secondary?
   - What is merely implementation detail?
   - What can be cut without changing the core scientific claim?

3. **Assumption Layer**
   - What is explicit?
   - What is hidden?
   - What is fragile?
   - What is unrealistic or too restrictive?

4. **Mechanism Layer**
   - What is the actual mechanism?
   - Why should it work?
   - What assumption does each component encode?
   - Which parts are essential vs. decorative?

5. **Evidence Layer**
   - Which claim is backed by theorem or derivation?
   - Which claim is backed by experiment?
   - Which claim is only conjectural?
   - Where is evidence missing, misaligned, or too weak?

6. **Risk Layer**
   - What is the main reviewer attack path?
   - What collapse happens if one assumption fails?
   - What claim is most vulnerable?

Use this hierarchy to avoid sentence-level patching of structural problems.

#### Mechanism Reality Check (Trigger)

When a method claims to model or explain a process:

Ask:
- does the mechanism correspond to a real underlying process?
- or is it only a functional approximation?

If the claimed explanation exceeds what the mechanism establishes:
- narrow or qualify the explanatory claim;
- identify the derivation, empirical test, or comparison needed to support it;
- assess the actual contribution separately. A functional approximation can still be valuable; do not automatically downgrade it because it is not a faithful process model.

Do not accept architectural complexity as evidence of mechanism validity.

#### Fix Classification (Mandatory)

For any issue, classify before acting:

- **Structural:** problem, contribution, assumption, or mechanism level
- **Local:** wording, clarity, ordering

Rules:
- Match intervention scope to issue level: do not apply local fixes to structural problems, or structural changes to local ones.

### 0.9. Novelty Decomposition (When Assessing Contribution)

Decompose novelty into types; evaluate which are present.

Possible novelty types:

- **Problem novelty:** a real new problem or a newly legitimized formulation.
- **Representation novelty:** a genuinely new abstraction, parameterization, or factorization.
- **Mechanism novelty:** a new causal or algorithmic mechanism.
- **Optimization novelty:** a new solution strategy, objective, solver, or training principle.
- **Systems novelty:** a new integration of components that changes capability meaningfully.
- **Insight novelty:** a new explanation, interpretation, or understanding.
- **Evaluation novelty:** a new way to test realism, limitations, or practical value.

For each type, ask:

- Is it truly new, or only recombined?
- Is it central or peripheral?
- Is it conceptual or merely implementation-level?
- Does the claimed novelty match the evidence?

Then determine the paper's real novelty profile. Do not let broad claims hide that novelty exists in only one narrow dimension.

### 0.10. Structure and Storytelling Check (Mandatory)

Evaluate whether the paper is easy to follow and its narrative scientifically coherent.

Check:

- Does the opening establish the target problem quickly?
- Is the motivation concrete rather than generic?
- Is the impact of the work stated clearly?
- Does each section answer the natural next question in the reader's mind?
- Is the contribution introduced before technical detail overload?
- Are transitions logical and momentum-preserving?
- Does the structure help sustain reader attention rather than scatter it?
- Is the paper front-loaded with what matters most?

If the structure is weak, diagnose whether the problem is:

- ordering;
- missing motivation;
- buried contribution;
- delayed evidence;
- excessive setup before payoff;
- fragmented narrative.

Do not only fix sentences; repair the reading path.

When paragraph flow is weak, optionally use a compact reverse outline: assign each paragraph its argumentative role and identify redundancy, unsupported transitions, or misplaced evidence. Show it only if it clarifies the proposed repair.

### 1. Precision Over Fluency

- Eliminate ambiguity.
- Align claims with evidence.
- Avoid vague language.

#### Claim Severity Calibration (Mandatory)

When diagnosing issues, explicitly calibrate severity:

- **Critical:** invalidates the core scientific claim
- **Major:** weakens contribution or credibility significantly
- **Moderate:** affects clarity, positioning, or partial correctness
- **Minor:** local issue without structural impact

Rules:
- Do not label an issue as Critical unless it directly affects the core claim.
- Prioritize the dominant issue without lowering the severity of other well-supported findings to fit an output budget.
- Ensure severity labeling matches evidence strength.
- Separate severity from confidence. For an uncertain issue, state its potential consequence conditionally and identify the missing evidence; do not present a possible critical flaw as a confirmed minor one.

### 2. Mathematical Rigor

- Correct faulty notation or derivations without silently changing the intended claim; flag unresolved reasoning.
- **Existing results:** For central or claimed-new lemmas and theorems, check supplied references and available libraries for equivalent, stronger, or closely related results, including different formulations. Compare assumptions and conclusions; recommend citation or reuse where appropriate. If coverage is insufficient, propose a bounded external search and obtain approval before proceeding. Neither a library search nor a lack of matches establishes publication novelty.
- **Tool-assisted verification:** For consequential proofs or nontrivial derivations, consider whether symbolic computation, numerical checks, or a proof assistant such as Lean would meaningfully improve confidence. Use the smallest useful check and existing project tools; obtain approval before substantial formalization. Distinguish algebraic or numerical checks from formal proof, and ensure any formalized statement matches the manuscript's assumptions and conclusion. Report what was actually checked, including unexecuted code, unresolved obligations (such as Lean `sorry`), and added assumptions or axioms; never treat an assumed conclusion as proved.

### 3. Knowledge Separation

Distinguish:

- facts;
- assumptions;
- observations;
- hypotheses;
- interpretations.

### 4. Intellectual Sparring

- Challenge weak novelty.
- Expose assumptions.
- Reposition if needed.
- Reveal what the author may be overestimating.

### 5. Claim-Evidence Alignment

Match the support to the claim:

- Mathematical conclusions require a valid derivation under stated premises.
- Empirical findings require observations or experiments within the stated scope.
- Comparative claims require fair baselines and comparable settings.
- Causal or explanatory claims need evidence that distinguishes plausible alternatives, not correlation alone.
- Assumptions are premises, not empirical evidence. Hypotheses and interpretations must remain labeled until supported.

For central or disputed claims, identify the supporting source and relevant section, equation, table, figure, or experiment run when available. Do not invent locators or require a registry for every claim.

When multiple manuscript sections or displays are supplied, check central results, settings, terminology, and claim scope for contradictions. Flag discrepancies and their locations; do not silently normalize conflicting values.

### 6. Limitations

Identify material:

- failure modes;
- instability;
- sensitivity;
- what is not solved.

### 7. Terminology Consistency

Keep terminology stable and standard.

## Tone and Voice

- Frank, evidence-based, and non-evasive.
- Strong critiques must remain precise, respectful, and constructive.
- Advisor-like but intellectually demanding.
- Supportive through rigor, not comfort.
- Never adversarial; always oriented toward improvement.

Voice: expert-level, self-critical, technically rigorous.

## Self-Critical Double-Check (Mandatory Before Any Assessment Output)

Before delivering any assessment — of the paper, of reviewer comments, or of a revision plan — apply the following self-check to the draft output:

1. **Evidence audit:** Is every classification (error, notation gap, missing detail, convention claim) backed by specific evidence from the paper or verifiable field knowledge? Label uncertain items explicitly.

2. **Error-type consistency:** Have algorithmic errors, notation ambiguities, reproducibility gaps, field convention claims, and reviewer opinions been correctly distinguished and not conflated?

3. **Authority deference check:** Has any claim been accepted solely on the basis of reviewer or perceived field authority, rather than evidence? If so, reclassify or flag.

4. **Symmetric rigor:** Are reviewer claims held to the same evidentiary standard as paper claims?

5. **Own overclaim check:** Are any of the agent's own severity labels (critical, important, minor) stronger than the evidence supports?

If any check fails, revise before delivering. Explicitly correct an earlier communicated assessment when it changes the author's understanding; do not narrate internal draft corrections.

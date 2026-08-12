# Supervisor Prompt Alignment — Design Spec

**Date:** 2026-08-12
**Status:** Approved for planning
**Classification:** UNCLASSIFIED — this document contains no CUI. Content becomes CUI only when an end user enters a specific employee's performance data into a chat session.

## 1. Purpose

Bring `supervisor_prompt.txt` into compliance with the 2026 AcqDemo/CCAS program guide, and bring `assessment_review_prompt.txt` and `README.md` into agreement with it. This resolves the second of the three divergences tracked in `docs/superpowers/specs/2026-07-14-assessment-package-template-design.md` §6.

The core defect: `supervisor_prompt.txt` requires every factor narrative to open with a concurrence phrase ("I concur with the employee's self-assessment"). The guide requires it to open with a lead-in statement equal to the recommended numerical score. A supervisor following the current prompt produces a non-compliant appraisal.

### Source material (authoritative, in priority order)

1. `2026guide.pdf` — *AcqDemo Business Rules for United States Space Force Pay Pools, 2026 CCAS*, signed 21 May 2026. Governing sections:
   - **7.5.4** — supervisory assessments; mandatory lead-in statement equal to the recommended numerical score.
   - **7.5.4.1** — *Meeting expected contributions* = scoring at EOCS. Narrative must explain why the factor is met with clear and precise specifics (not flowery words) and **must include contributions the employee did not provide in their self-assessment**.
   - **7.5.4.2** — *Exceeding expected contributions* = scoring above EOCS. Same specificity requirement; must include **significant** contributions the employee did not report.
   - **7.5.4.3** — *Partially meeting* / *Not meeting expected contributions* = scoring below EOCS. Narrative must clearly describe inadequate contributions or unmet expectations, and the supervisor must have documented feedback sessions or other supporting evidence throughout the cycle ("no surprises").
   - **7.5.5** — each factor assessment must also include one to two sentences addressing how the employee's contributions align with DAF guidance at 1.0. References (c) and support the recommended PAQL score.
   - **9.1.2** — Very High scores are awarded only to employees whose EOCS is 96–100 (NH), 79–83 (NJ), or 57–61 (NK), and the supervisory written assessment must state specifically how the employee exceeds the top of the broadband factor(s).
   - **9.1.4** — VHS coding exception: when coding a VHS requires scoring one or two factors below EOCS, the lead-in for the associated factor states the employee is *"meeting or exceeding expected contributions."*
   - **1.0. References (c)** — *Department of the Air Force (DAF) AcqDemo Performance Scoring Guidelines for Supervisors, September 2025*. Referenced by 7.5.5; **not present in this repository**.
   - **Acronyms (Attachment G)** — PAQL = Performance Appraisal Quality Level; EOCS = Expected Overall Contribution Score. These are distinct from the broadband factor score bands.
2. `templates/assessment_package_template.md` — already reflects the guide's Annual Supervisor Response lead-ins and the DAF-alignment sentence. The prompt is being brought up to the template, not the reverse.
3. `wri_prompt.txt` — the most recently revised prompt in the repo; supplies the house conventions this file adopts (plain-text output for CAS2Net, PATTERN-not-script labeling on example lists, affirmative-inclusion rules, verification steps in `<thinking_process>`).

### Explicitly out of scope

- **Midpoint and closeout supervisory assessments.** Decided: annual only. Midpoint supervisor response (guide 7.3.3–7.3.4: no W-R-I, no scores, documented discussion date/method) is already served by `templates/assessment_package_template.md`. Closeout (7.4) is served by neither and remains unaddressed.
- **`contribution_plan_prompt.txt`.** Its Attachment C divergence (2 unlabeled narrative objectives vs. 3+ labeled JA1/CT1/MS1 contributions) is the third tracked item in the 2026-07-14 spec §6 and is deliberately held pending SME input.
- **Deriving or recommending numeric scores, score ranges, or PAQL values.** Removed from the prompt entirely; see §3.2.
- **Obtaining Reference (c).** The DAF Performance Scoring Guidelines are not in the repo and will not be fetched; §3.3 defines how the required sentence is produced without them.

## 2. Approach

Surgical revision of `supervisor_prompt.txt` in place, preserving its existing `<role>` / `<task>` / `<reference_data>` / `<rules>` / `<clarifying_protocol>` / `<thinking_process>` / `<output_format>` skeleton and all three career-path descriptor tables verbatim.

Rejected alternatives: a full rewrite modeled on `wri_prompt.txt` (re-derives ~400 lines of correct verbatim descriptor data for stylistic uniformity, risking transcription error in the one part of the file that is quoted guide content); and a rules-only patch (leaves the clarifying protocol interviewing supervisors about concurrence while the rules require lead-ins — internally contradictory).

## 3. `supervisor_prompt.txt` Changes

### 3.1 Intake — `<clarifying_protocol>`

Asked once, before the per-factor questions:

- Employee's career path (NH, NJ, or NK) and broadband level — existing behavior.
- **Employee's EOCS** — new and required. The four lead-ins are defined relative to EOCS, and Very High eligibility is gated on it (9.1.2). If the supervisor does not provide it, the prompt asks once; if still unavailable, the prompt proceeds and notes the omission in the delete-before-pasting section.

Asked for each of the three factors:

1. Which lead-in applies to this factor: Meeting, Exceeding, Partially meeting, or Not meeting expected contributions.
2. What contributions, if any, the employee did not report in their self-assessment. The question states plainly that the guide requires these in the narrative for Meeting and Exceeding factors.
3. **Only when the supervisor selects Partially meeting or Not meeting:** what documented feedback sessions or other supporting evidence from during the cycle support that position (7.5.4.3).

Retained from the current protocol, unchanged in intent:

- **Low-evidence handling.** Where combined employee and supervisor evidence is insufficient, ask one targeted follow-up for that factor; if the supervisor declines, produce a shorter narrative grounded in descriptor language for the career path and level, fabricating nothing.
- **One round only.** No second round of clarifying questions unless the supervisor's response introduces substantially new or incomplete information.

Changed:

- **Skip protocol.** Currently "assume full concurrence," which is meaningless once concurrence is gone. Becomes: assume *Meeting expected contributions* for all three factors, produce the best output from the information given, and state that assumption in the delete-before-pasting notes so the supervisor must consciously accept or change it.

### 3.2 Rules

**Replaced:**

- **Rule 8 — concurrence phrases → lead-in statements.** The first sentence of every factor narrative must be exactly one of the following, reproduced verbatim with no additions, qualifiers, paraphrase, or substitutions:
  - `Meeting expected contributions`
  - `Exceeding expected contributions`
  - `Partially meeting expected contributions`
  - `Not meeting expected contributions`

  The rule states explicitly that the retired concurrence phrasing ("I concur with the employee's self-assessment," "I partially concur…," "I do not concur…") is **no longer compliant** and must not be produced even if the supervisor phrases their input that way. If a supervisor answers in concurrence language, the prompt maps it to a lead-in by asking, not by guessing.

- **Rule 4 — score-range recommendation → no scoring.** The model does not recommend or state a numeric factor score, a score range, an OCS, or a PAQL number. The supervisor's lead-in already encodes the score's relationship to EOCS. The descriptor tables remain in the file solely as vocabulary for writing narratives. This rule governs values the model would *originate*; echoing the EOCS the supervisor supplied back in the output header (§3.3) is not a recommendation and is permitted.

**Added:**

- **DAF-guidance / PAQL alignment sentence (7.5.5).** Each factor narrative ends with one to two sentences addressing how that factor's contributions align with DAF guidance and support the recommended PAQL score. The sentences are constructed from the factor descriptor and discriminator language for the employee's career path and broadband level, already present in `<reference_data>`. **Prohibited:** inventing citations, paragraph or section numbers, dates, page references, or quotations from the DAF AcqDemo Performance Scoring Guidelines for Supervisors, which the model does not have. The document may be named; it may not be quoted.
- **Lead-in obligations (7.5.4.1–7.5.4.3).** For Meeting and Exceeding factors, contributions the employee did not self-report must appear in the narrative when the supervisor provides them. For Partially meeting and Not meeting factors, the narrative must clearly describe the inadequate contributions or unmet expectations and reference the supervisor-provided documented feedback or evidence; if the supervisor provides none, the model asks rather than writing an unsupported negative narrative.
- **Specificity.** Narratives use clear and precise specifics, not flowery words (the guide's own phrasing at 7.5.4.1–.2). Complements, does not replace, the existing AFH 33-337 style rule.
- **Very High (9.1.2, 9.1.4).** Very High applies only when the employee's EOCS falls in the eligible band for their career path (NH 96–100, NJ 79–83, NK 57–61). When a Very High factor is asserted, the narrative must state specifically how the employee exceeds the top of the broadband for that factor. The 9.1.4 exception permits a fifth lead-in, `meeting or exceeding expected contributions`, used only for factors scored below EOCS as an artifact of coding a VHS in CAS2Net.
- **Plain-text output.** No Markdown bold, italics, headers, horizontal rules, or bullets anywhere in the narrative block, since the text is pasted directly into CAS2Net. Mirrors `wri_prompt.txt` Rule 16.

**Corrected:**

- `<paql_score_ranges>` is renamed to reflect what it holds: broadband factor score ranges, not PAQL values. A short note defines PAQL as the 1–5 Performance Appraisal Quality Level and EOCS as the Expected Overall Contribution Score, so the 7.5.5 sentence targets the right concept.
- `<role>` and `<task>` drop "PAQL-aligned" as a description of the narrative and describe the output as a guide-compliant supervisory annual assessment.

**Retained unchanged:** the NH, NJ, and NK descriptor tables in full; the 4,000-character per-factor CAS2Net limit; the no-fabrication rule; AFH 33-337 (Tongue and Quill) style; the evidence-based rule requiring every claim to trace to a self-assessment statement or explicit supervisor input; and the closing reminder that the tool assists but does not replace supervisory judgment.

### 3.3 Output format

Two blocks, visually separated. Everything in the first block is paste-ready plain text; everything in the second is advisory and marked for deletion.

Block 1 — the assessment:

```
Career Path and Level: [NH/NJ/NK and level]        Expected OCS: [EOCS]

Job Achievement and/or Innovation

[Lead-in statement, verbatim, as the first sentence.] [Narrative: contributions
the employee did not report, followed by contributions mapped to the descriptor
and discriminator language for this career path and level, in specifics.]
[One to two sentences on alignment with DAF guidance supporting the recommended
PAQL score.]

Communication and/or Teamwork

[Same three-part structure.]

Mission Support

[Same three-part structure.]

Review this assessment against the employee's actual performance before
finalizing in CAS2Net. This tool assists but does not replace supervisory
judgment.
```

Block 2 — advisory:

```
Notes (delete before pasting into CAS2Net):
- [Character count per factor against the 4,000-character limit]
- [Factors with thin evidence and what future documentation would strengthen]
- [Any assumption made under the skip protocol, including an assumed lead-in]
- [EOCS omission, if applicable]
```

Structural changes from the current output format:

- **The Overall Assessment section is removed.** Its function was to recommend an overall score range, which the model no longer does.
- **The per-factor structure collapses from four elements to three.** The concurrence element is gone; missing contributions merge into the narrative body per 7.5.4.1 rather than standing as a separate paragraph; the DAF/PAQL sentence becomes the closing element.
- **Character-count reporting moves out of the pasteable block** into the advisory notes.

### 3.4 Gemini hardening

Applied per the failure modes confirmed in live testing on 2026-07-27 (see `wri_prompt.txt` Rules 5 and the clarifying protocol for the precedent):

- **Verbatim strings labeled as such.** The four lead-ins (and the 9.1.4 fifth) are marked exact required text, with paraphrase, qualifiers, and additions explicitly forbidden.
- **Example lists labeled PATTERN, not script.** The `<clarifying_protocol>` low-evidence follow-up examples are currently fully-formed, ready-to-ask questions — the precise shape that caused Gemini to run example questions verbatim on topics the user never raised. They are relabeled "PATTERN only, not a script," with verbatim reuse forbidden and questions about topics absent from the supervisor's own input forbidden.
- **Affirmative inclusion, not just prohibition.** Rules stating that supervisor-provided unreported contributions MUST appear in that factor's narrative, and that supervisor-provided figures MUST appear rather than being dropped for generic phrasing under the 4,000-character constraint. Prohibiting fabrication does not, on its own, make Gemini include real detail.
- **Matching verification steps in `<thinking_process>`:** lead-in is verbatim and is the first sentence of each factor; the DAF/PAQL sentence is present in all three factors; every supervisor-provided contribution and figure appears; no Markdown anywhere; each factor is within 4,000 characters; no numeric score, score range, or PAQL value is stated.

## 4. `assessment_review_prompt.txt` Changes

The review prompt currently flags any deviation from the three concurrence phrases as CRITICAL, which would fail every guide-compliant appraisal produced this cycle. Changes:

- **CHECK 1 — "Supervisor Concurrence Statements" → "Supervisor Lead-In Statements."** Enforces the four exact lead-ins from 7.5.4 as the required opening of each supervisor factor narrative. The three retired concurrence phrases move into the non-compliant examples list, alongside the existing examples, since supervisors reusing last cycle's habit will be the most common real-world failure. For Partially meeting and Not meeting, verify the narrative describes the inadequate contributions or unmet expectations.
- **CHECK 5 — required elements.** Drop the concurrence element. The four required elements become: lead-in statement; contributions the employee did not report; contributions mapped to descriptors and discriminators; and the 7.5.5 DAF-guidance/PAQL alignment sentence. Flag a missing DAF/PAQL sentence as WARNING. CRI vs. CA differentiation stays as an INFO check.
- **CHECK 6 — scoring validation.** Keep the numeric range tables. Add the 9.1.2 VHS EOCS gate: Very High requires an EOCS of 96–100 (NH), 79–83 (NJ), or 57–61 (NK), and the narrative must state how the employee exceeds the top of the broadband. Flag a Very High score outside the eligible EOCS band as CRITICAL.
- **CHECK 3 — stale minimum.** Corrects "does NOT count toward the 2 required W-R-I statements" to 3, per 7.5.1.1 and 7.5.2.1. The 2-per-factor figure applies only to first-year organizations for the current cycle.

Not changed: the midterm/annual first question, W-R-I checks, header block and structure checks, character limits, writing-quality checks, multi-person handling, and the no-tables output rule.

## 5. `README.md` Changes

Specific passages requiring change:

- **Line 6** — the tool list describes the supervisor prompt as generating "PAQL-aligned supervisory appraisals." Reword to match what it now produces.
- **Line 178** — describes the output as opening "with the exact concurrence phrasing" and ending with "a quality-of-performance statement supporting a recommended PAQL **score range** (not a specific numeric score)." Both halves are now wrong: the opening is a lead-in statement, and no score range is recommended. Rewrite to describe the three-part factor structure and the plain-text paste block with a separate notes block to delete first. This sentence also uses "LLM," which the audience rule in `CLAUDE.md` forbids — replace it while rewriting.
- **Around lines 160–177** — the described intake questions become: the employee's EOCS, and per factor, which of the four lead-ins applies, unreported contributions, and (for the two below-EOCS lead-ins) the supporting documented feedback.
- **Lines 195 and 223** — the review-prompt section says it "checks supervisor concurrence statements" and lists CHECK 1 as "Supervisor Concurrence Statements … one of three exact approved phrasings." Update both to the lead-in statements and the count of four.
- **Line 15 — platform row.** `chat.genai.army.mil` becomes `https://genai.mil/`.
- **Line 16 — model row.** Reads "Claude 4.6 O," which is Claude-era and stale per `CLAUDE.md`. Becomes **Gemini 3.1 Pro**, with a short parenthetical that Gemini 3.6 Flash also works if Pro is unavailable. Rationale in §5.1.
- **Lines 26, 107, 153, 199** — the "start a new conversation on chat.genai.army.mil" instruction in each of the four prompt walkthroughs. Update the site in all four.

Audience constraint unchanged: plain language for a reader who has never used a chat-based AI tool. No jargon such as "prompt," "token," "LLM," or "context window."

### 5.1 Model recommendation rationale

Available on `https://genai.mil/`: Gemini 3.6 Flash, Gemini 3.1 Pro, and older Pro versions. The README will recommend **Gemini 3.1 Pro**, with 3.6 Flash named as an acceptable fallback.

Both Gemini failures confirmed in this repo's live testing on 2026-07-27 — running example clarifying questions verbatim as a script, and dropping user-provided figures to satisfy a competing word cap — are instruction-adherence failures on a long, multi-constraint prompt. `supervisor_prompt.txt` is the repo's longest prompt (~560 lines) and after this revision carries verbatim-phrase requirements, a hard 4,000-character limit, and conditional branching on the supervisor's lead-in choice. Pro tiers are the better fit for that workload; Flash tiers trade instruction adherence for latency and cost, neither of which constrains a task a supervisor performs a few times a year.

Caveat, stated plainly because it affects how much weight to give the recommendation: 3.6 Flash is a newer model generation than 3.1 Pro, and the two have not been compared on these prompts. A newer Flash can outperform an older Pro. The recommendation is therefore provisional and settled empirically by the §6 verification tests — specifically the concurrence-language regression check and the supervisor-provided-figure retention check. If 3.6 Flash passes both cleanly, flip the README recommendation to it and record the result.

### 5.2 `CLAUDE.md`

`CLAUDE.md` names `chat.genai.army.mil` three times as the platform these prompts run on (lines 7, 29, and 30). All three become `https://genai.mil/`. Line 30's Claude-to-Gemini migration note stays — the guidance it carries is still live — but its statement that the README settings table "still list[s] a Claude model" becomes stale once §5 lands and is updated to reflect that the table now names a Gemini model.

## 6. Verification

There is no test tooling in this repo; verification is manual, in the terms `CLAUDE.md` sets out.

1. **Cross-file phrase consistency.** Grep all four prompt files and the template for the retired concurrence phrases; the only surviving occurrences must be the non-compliant examples in `assessment_review_prompt.txt` CHECK 1. Grep for each of the four lead-ins; wording must match the guide and the template character for character.
2. **Guide traceability.** Every new or changed rule cites the guide section it implements, and each citation is checked against `2026guide.pdf`.
3. **Live check on `https://genai.mil/`.** Paste the revised prompt as the first message with a synthetic self-assessment containing no real employee data. Confirm: the intake asks for EOCS and a per-factor lead-in; each factor narrative opens with a verbatim lead-in; each closes with a DAF/PAQL sentence naming no invented citation; the output contains no Markdown and no numeric score; the notes block is separate and marked for deletion.
4. **Regression check on the retired behavior.** Answer the intake in concurrence language ("I concur") and confirm the model asks which lead-in applies rather than emitting a concurrence sentence.
5. **Figure-retention check.** Supply a supervisor contribution containing a specific figure and confirm it survives into the narrative rather than being replaced by generic phrasing under the 4,000-character constraint.
6. **Model comparison.** Run tests 3–5 on Gemini 3.1 Pro and on Gemini 3.6 Flash. If Flash passes all three cleanly, update the README recommendation to Flash and record the result; otherwise leave the Pro recommendation in place (§5.1).

## 7. Remaining Divergence After This Change

Of the three items in `2026-07-14-assessment-package-template-design.md` §6:

- Supervisor lead-in alignment — **resolved by this spec.**
- `contribution_plan_prompt.txt` labeled-contribution alignment (Attachment C) — **still open**, held for SME input.
- `wri_prompt.txt` label form — **already resolved**; the file uses the abbreviated `(W)`/`(R)`/`(I)` labels the SME preferred, matching the template.

Closeout supervisory assessments (guide 7.4) are covered by no prompt and no template section. Raised during this design and **deliberately deferred** — not part of this work.

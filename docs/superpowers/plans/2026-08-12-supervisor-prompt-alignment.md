# Supervisor Prompt Alignment Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Bring `supervisor_prompt.txt` into compliance with the 2026 AcqDemo/CCAS business rules, and bring `assessment_review_prompt.txt`, `README.md`, and `CLAUDE.md` into agreement with it.

**Architecture:** This repository contains no code. It is a library of LLM prompts held in plain `.txt` and `.md` files, pasted by end users as the first message of a chat session. Every change in this plan is a text edit to one of four files. Verification is by `grep` for exact strings and by reading the edited section, not by a test runner — none exists and none is to be added.

**Tech Stack:** Plain text and Markdown. `git`, `grep`, and a text editor. No build, lint, test, or package tooling.

## Global Constraints

- **Authority order for any factual question:** SME-provided instructions → `2026guide.pdf` → other regulations and general web info. Do not resolve a rules question from an outside source when the guide covers it.
- **Classification:** Everything in this repo is UNCLASSIFIED. Never add real employee data, names, or classified information to any file, including examples.
- **No new tooling.** Do not add build, lint, test, CI, or package files.
- **`supervisor_prompt.txt` file conventions:** XML-style tags (`<role>`, `<task>`, `<rules>`, etc.). Match the existing convention in the file being edited — `assessment_review_prompt.txt` uses plain Markdown headers and bullets instead.
- **Prose style:** All model-authored prose rules preserved in these prompts follow AFH 33-337 (The Tongue and Quill) — active voice, subject-verb-object, precise and objective, no colloquialisms.
- **README audience:** Very non-technical. No jargon such as "prompt," "token," "LLM," or "context window" in text this plan adds or rewrites.
- **Exact strings.** The four lead-in statements are `Meeting expected contributions`, `Exceeding expected contributions`, `Partially meeting expected contributions`, `Not meeting expected contributions`. The Very High coding exception adds `meeting or exceeding expected contributions`. These must match character for character everywhere they appear, across all files.
- **Platform:** `https://genai.mil/`. Recommended model: Gemini 3.1 Pro, with Gemini 3.6 Flash as fallback.
- **Branch:** All work lands on `supervisor-prompt-alignment`, which already exists and already contains the design spec. Do not commit to `main`.
- **Do not touch `contribution_plan_prompt.txt`.** Its Attachment C divergence is deliberately deferred pending SME input.

---

### Task 1: Correct terminology and reference data in `supervisor_prompt.txt`

The file currently labels the broadband factor score bands "PAQL score ranges." PAQL is the 1–5 Performance Appraisal Quality Level, a different thing entirely. This task fixes the naming, defines the three easily-confused terms, and adds the Very High EOCS eligibility gate. No behavioral rules change here.

**Files:**
- Modify: `supervisor_prompt.txt:1-12` (`<role>` and `<task>`)
- Modify: `supervisor_prompt.txt:16-44` (`<paql_score_ranges>` and `<very_high_score_criteria>`)

**Interfaces:**
- Consumes: nothing.
- Produces: the tag name `<factor_score_ranges>` and the tag name `<very_high_criteria>`, both referenced by Tasks 2 and 4. The terms EOCS, OCS, and PAQL as defined in the new `<terminology>` block, used by every later task.

- [ ] **Step 1: Replace `<role>` and `<task>`**

Replace lines 1–12 in their entirety with:

```
<role>
You are an expert in AcqDemo performance appraisal processes, specializing in the NH (Business Management and Technical Management), NJ (Technical Management Support), and NK (Administrative Support) career paths. You support Air Force and Space Force supervisors in producing annual supervisory assessments that comply with the 2026 AcqDemo/CCAS business rules.
</role>

<task>
Generate a supervisory annual assessment for an employee based on:
- Their self-assessment contribution statements
- Their career path (NH, NJ, or NK), broadband level, and Expected Overall Contribution Score (EOCS)
- The supervisor's selected lead-in statement for each factor, any contributions the employee did not report, supporting evidence, and any additional context

Map the employee's contributions to the appropriate factor descriptors and discriminators, and produce a narrative for each of the three factors that opens with the required lead-in statement and closes with the required DAF guidance alignment sentence.
</task>
```

- [ ] **Step 2: Add the `<terminology>` block**

Immediately after the `<reference_data>` opening tag (line 14) and before the score ranges, insert:

```
<terminology>
**EOCS (Expected Overall Contribution Score)** — the numeric score the employee is expected to achieve for the assessed value of their position. The four lead-in statements in Rule 8 are defined relative to the EOCS. The supervisor provides this value. Never estimate it.

**OCS (Overall Contribution Score)** — the employee's actual scored contribution level, determined by the supervisor and the pay pool.

**PAQL (Performance Appraisal Quality Level)** — a separate quality rating on a 1 to 5 scale, assigned by the supervisor and the pay pool. PAQL is NOT the same as the factor score ranges below. Rule 10 requires each factor narrative to address how the contributions support the recommended PAQL score. It does not require you to state a PAQL number, and Rule 4 forbids you from doing so.

**Factor score ranges** — the numeric bands below define the valid factor scores for each career path and broadband level. They appear here only to help you calibrate descriptor language to the right level. Do not state, recommend, or infer a numeric score from them (Rule 4).
</terminology>
```

- [ ] **Step 3: Rename the score range block**

Change the opening tag `<paql_score_ranges>` to `<factor_score_ranges>` and the closing tag `</paql_score_ranges>` to `</factor_score_ranges>`. Change nothing else inside the block — the three career-path headings and every numeric band are correct as written and must not be altered.

- [ ] **Step 4: Replace the Very High block**

Replace the `<very_high_score_criteria>` block (lines 38–44) in its entirety with:

```
<very_high_criteria>
A "Very High" categorical rating recognizes contributions and performance that far exceed expectations, warranting scores above the top level of the employee's broadband.

Eligibility gate (2026 business rules, 9.1.2). Very High may only be used when the employee's EOCS falls within the band for their career path:
- NH: EOCS 96 to 100
- NJ: EOCS 79 to 83
- NK: EOCS 57 to 61

If the supervisor asserts Very High performance and the EOCS falls outside that band, or the EOCS was not provided, state that eligibility is not confirmed and ask the supervisor to verify it. Do not write a Very High narrative on unconfirmed eligibility.

Criteria. Very High applies when the employee's performance exceeds the expectations of their level:
- Achieved superior outcomes in quality, quantity, timeliness, and impact
- Overcame obstacles with extra effort
- Made contributions beyond expectations to organizational success
- Demonstrated the highest professionalism

When Very High applies to a factor, the narrative must state specifically how the employee exceeds the top of the broadband for that factor.
</very_high_criteria>
```

- [ ] **Step 5: Verify the tag rename is complete**

Run: `grep -n "paql_score_ranges\|very_high_score_criteria" supervisor_prompt.txt`
Expected: no output. Any hit means a stale tag name remains.

Run: `grep -n "factor_score_ranges\|very_high_criteria\|<terminology>" supervisor_prompt.txt`
Expected: five lines — the opening and closing of each renamed block, plus the `<terminology>` opening.

- [ ] **Step 6: Verify the descriptor tables were not disturbed**

Run: `grep -c "Discriminators (all levels)" supervisor_prompt.txt`
Expected: `9` — three factors across three career paths. Any other number means descriptor content was damaged.

- [ ] **Step 7: Commit**

```bash
git add supervisor_prompt.txt
git commit -m "Correct PAQL vs factor score terminology in supervisor prompt

Renames paql_score_ranges to factor_score_ranges, since those bands are
broadband factor scores, not the 1-5 Performance Appraisal Quality Level.
Adds a terminology block distinguishing EOCS, OCS, and PAQL, and adds the
9.1.2 EOCS eligibility gate to the Very High criteria."
```

---

### Task 2: Replace the rules block in `supervisor_prompt.txt`

This is the core of the change. The concurrence rule is replaced by the guide's lead-in statements, and the score-range recommendation is removed.

**Files:**
- Modify: `supervisor_prompt.txt` — the entire `<rules>` block (currently lines 442–465, shifted by Task 1's insertions)

**Interfaces:**
- Consumes: `<factor_score_ranges>`, `<very_high_criteria>`, and `<terminology>` from Task 1.
- Produces: Rules 1 through 14 as numbered below. Tasks 3 and 4 reference these numbers directly — Rule 4 (no scoring), Rule 6 (4,000 characters), Rule 8 (lead-in statements), Rule 10 (DAF sentence), Rule 11 (Very High), Rule 12 (mandatory inclusion), Rule 13 (plain text). Do not renumber.

**Note on intermediate state:** after this task the file is internally inconsistent — the rules require lead-ins while the clarifying protocol still asks about concurrence. That is expected. Tasks 3 and 4 resolve it. Do not use the prompt between Task 2 and Task 4.

- [ ] **Step 1: Replace the entire `<rules>` block**

Replace everything from `<rules>` through `</rules>` with:

```
<rules>
1. Use ONLY the information provided in the employee's self-assessment contribution statements and the supervisor's input. Do not fabricate or assume accomplishments, metrics, or outcomes that are not explicitly stated.

2. Write in formal, objective, professional language consistent with AFH 33-337 (The Tongue and Quill) standards: active voice, clear subject-verb-object structure, precise language, no colloquialisms or subjective wording.

3. Map each contribution statement to the most appropriate factor and discriminator, and reference specific accomplishments from the statements in the narrative.

4. Do not state, recommend, or imply a numeric factor score, a score range, an OCS, or a PAQL number anywhere in the output. The supervisor's selected lead-in statement already carries the relationship between performance and the EOCS. Echoing back the EOCS the supervisor provided in the output header is not a recommendation and is permitted.

5. Write in clear and precise specifics, not flowery words. Name what the employee did and what resulted. Avoid unsupported superlatives.

6. Keep the narrative for each factor within 4,000 characters (the CAS2Net per-factor limit).

7. Be evidence-based. Every claim in the narrative must trace back to a specific contribution statement from the employee's self-assessment or to information the supervisor explicitly provides.

8. Lead-in statements are mandatory. The first sentence of every factor narrative MUST begin with one of these four lead-in statements, reproduced exactly as written, selected from the supervisor's response for that factor:
   - Meeting expected contributions
   - Exceeding expected contributions
   - Partially meeting expected contributions
   - Not meeting expected contributions

   These four are exact required text, not examples to adapt. Do not paraphrase them, do not reorder their words, do not add qualifiers such as "fully," "strongly," "clearly," or "overall," and do not substitute a similar phrase of your own.

   The lead-in equals the recommended numerical score relative to the employee's EOCS. Meeting means scoring at the EOCS for that factor. Exceeding means scoring above it. Partially meeting and Not meeting both mean scoring below it.

   Exception (2026 business rules, 9.1.4): when coding a Very High score in CAS2Net requires scoring one or two factors below the EOCS, the lead-in for those factors is "meeting or exceeding expected contributions." Use this fifth lead-in only when the supervisor states that this Very High coding situation applies.

   The concurrence phrasing used in prior cycles — "I concur with the employee's self-assessment," "I partially concur with the employee's self-assessment," and "I do not concur with the employee's self-assessment" — is NO LONGER COMPLIANT and must never appear in your output. If the supervisor answers in concurrence language, ask which of the four lead-in statements applies for that factor. Do not translate concurrence language into a lead-in on your own.

9. Each lead-in carries a specific narrative obligation:
   - Meeting expected contributions: explain why the factor is met. Include the contributions the employee did not provide in their self-assessment, when the supervisor supplies them.
   - Exceeding expected contributions: explain why the factor exceeds. Include the significant contributions the employee did not provide in their self-assessment, when the supervisor supplies them.
   - Partially meeting expected contributions or Not meeting expected contributions: clearly describe the inadequate contributions or unmet performance expectations, and reference the documented feedback sessions or other supporting evidence the supervisor provides. The written narrative must contain no surprises. If the supervisor selects either of these two lead-ins and provides no documented feedback or supporting evidence, do not write that narrative — ask for the evidence first.

10. Every factor narrative must end with one to two sentences addressing how the employee's contributions align with DAF guidance and support the recommended PAQL score. Build these sentences from the factor descriptor and discriminator language for the employee's career path and broadband level in <reference_data>. You may name the source as the DAF AcqDemo Performance Scoring Guidelines for Supervisors. You do NOT have that document. Never invent or reproduce a citation, section number, paragraph number, page number, publication date, or quotation from it. Do not state a PAQL number.

11. Very High. Apply the eligibility gate and criteria in <very_high_criteria>. Very High requires the employee's EOCS to fall within the band for their career path. When a Very High factor is asserted and eligibility is confirmed, the narrative must state specifically how the employee exceeds the top of the broadband for that factor.

12. Supervisor-provided detail is mandatory in the output, not optional. If the supervisor provides a contribution the employee did not report, that contribution MUST appear in that factor's narrative. If the supervisor provides a quantifiable figure — a count, percentage, dollar amount, timeframe, or similar — that figure MUST appear in the narrative. Never drop a supervisor-provided contribution or figure in favor of shorter or more general phrasing in order to stay within the character limit in Rule 6. When a narrative is at risk of exceeding that limit, cut adjectives, restatement, and filler before cutting any supervisor-provided fact.

13. Output the entire assessment block as plain text only — no Markdown bold, italics, headers, horizontal rules, or bullets. Use the factor names and labels exactly as shown in <output_format>, with no emphasis characters, since this text is pasted directly into CAS2Net. The separate notes block described in <output_format> is the only part of your response that the supervisor does not paste into CAS2Net.

14. Identify any factor where the contribution statements and supervisor input together provide insufficient evidence to write a substantive narrative. Follow the low-evidence handling described in the clarifying protocol.
</rules>
```

- [ ] **Step 2: Verify the four lead-ins are present and exact**

Run: `grep -c "^   - Meeting expected contributions$\|^   - Exceeding expected contributions$\|^   - Partially meeting expected contributions$\|^   - Not meeting expected contributions$" supervisor_prompt.txt`
Expected: `4`

- [ ] **Step 3: Verify the concurrence phrases survive only as the prohibition**

Run: `grep -n "concur" supervisor_prompt.txt`
Expected: hits only inside Rule 8's "NO LONGER COMPLIANT" paragraph. Any hit in `<task>`, `<clarifying_protocol>`, `<thinking_process>`, or `<output_format>` is expected at this point and is removed by Tasks 3 and 4.

- [ ] **Step 4: Verify no score-range recommendation language remains in the rules**

Run: `grep -n "score range" supervisor_prompt.txt`
Expected: hits only in Rule 4 (which forbids it) and in `<terminology>`. Any hit phrased as an instruction to produce one is a defect.

- [ ] **Step 5: Commit**

```bash
git add supervisor_prompt.txt
git commit -m "Replace concurrence rule with guide-required lead-in statements

Rule 8 now requires each factor narrative to open with one of the four
lead-in statements from 2026 business rules 7.5.4, equal to the
recommended score relative to EOCS, and explicitly retires the
concurrence phrasing. Adds the 7.5.5 DAF guidance and PAQL sentence, the
7.5.4.1-.3 per-lead-in narrative obligations, the 9.1.2 Very High gate,
mandatory inclusion of supervisor-provided contributions and figures, and
plain-text output for CAS2Net. Removes the score-range recommendation."
```

---

### Task 3: Rewrite the clarifying protocol in `supervisor_prompt.txt`

The intake becomes a scoring interview: EOCS up front, then a lead-in selection per factor. This task also applies the PATTERN-not-script hardening to the example follow-up questions, which is the exact shape that caused Gemini to ask scripted off-topic questions in the 2026-07-27 testing of `wri_prompt.txt`.

**Files:**
- Modify: `supervisor_prompt.txt` — the entire `<clarifying_protocol>` block (currently lines 467–503, shifted by Tasks 1 and 2)

**Interfaces:**
- Consumes: Rule 8's four lead-in statements and Rule 10, both from Task 2.
- Produces: the six protocol steps, referenced by Task 4's `<thinking_process>` step 2 and by the notes block in `<output_format>`. Step 5's skip-protocol assumption of `Meeting expected contributions` is recorded in the notes block Task 4 defines.

- [ ] **Step 1: Replace the entire `<clarifying_protocol>` block**

Replace everything from `<clarifying_protocol>` through `</clarifying_protocol>` with:

```
<clarifying_protocol>

**Step 1 — Confirm the rating context.**

Before anything else, confirm you have all three of the following:
- The employee's career path (NH, NJ, or NK)
- The employee's broadband level
- The employee's EOCS

Ask for whichever is missing. The EOCS is required because the lead-in statements in Rule 8 are defined relative to it and Very High eligibility depends on it. Never estimate an EOCS. If the supervisor cannot provide it, proceed and record the omission in the notes block described in <output_format>.

**Step 2 — Ask the per-factor questions.**

Present them in the format below.

**Before I generate the supervisory assessment, I need the following for each factor:**

**Factor 1: Job Achievement and/or Innovation**
- Which lead-in statement applies to this factor: Meeting expected contributions, Exceeding expected contributions, Partially meeting expected contributions, or Not meeting expected contributions?
- What contributions, if any, did the employee leave out of their self-assessment? The business rules require these to appear in the narrative for factors that are meeting or exceeding.
- Any additional context about scope, scale, or impact?

**Factor 2: Communication and/or Teamwork**
- [The same three questions]

**Factor 3: Mission Support**
- [The same three questions]

**Step 3 — Follow up on factors below the EOCS.**

For any factor where the supervisor selects Partially meeting expected contributions or Not meeting expected contributions, ask what documented feedback sessions or other supporting evidence from during the cycle support that position. The business rules require the written narrative to contain no surprises. Do not write a below-EOCS narrative without this input.

**Step 4 — Low-evidence handling.**

After the supervisor responds, identify any factor where the combined evidence — employee statements plus supervisor input — is still insufficient to write a substantive narrative. For each such factor:

a. Ask one targeted follow-up question naming that specific factor and the specific kind of evidence that is missing.

   The two questions below illustrate the PATTERN for this kind of question only. They are NOT a script. Never ask one verbatim, and never ask about a topic that the supervisor's own input and the employee's self-assessment did not already raise:
   - "For Communication and/or Teamwork, the self-assessment is limited. Are there briefings, written products, or cross-functional efforts you want reflected in this factor?"
   - "For Mission Support, I have little evidence on customer engagement or resource planning. Are there examples you can add?"

b. If the supervisor declines or has nothing to add, write a shorter narrative for that factor that:
   - Opens with the lead-in statement the supervisor selected
   - Uses descriptor and discriminator language for the employee's career path and broadband level
   - Fabricates no specific accomplishments, numbers, or events
   - Still ends with the DAF guidance alignment sentence required by Rule 10
   - Is flagged in the notes block as thin on evidence, with a note on what documentation would strengthen it next cycle

**Step 5 — Skip protocol.**

If the supervisor instructs you to skip the clarifying questions and generate immediately, assume "Meeting expected contributions" for all three factors and produce the best possible output from the information provided. State that assumption in the notes block so the supervisor can change it. Never assume Exceeding, Partially meeting, or Not meeting — each of those carries evidence obligations under Rule 9 that unprompted assumption cannot satisfy.

**Step 6 — Limit to one round.**

Do not ask more than one round of clarifying questions unless the supervisor provides substantially new or incomplete information in their response.
</clarifying_protocol>
```

- [ ] **Step 2: Verify the concurrence questions are gone from the protocol**

Run: `grep -n "concur" supervisor_prompt.txt`
Expected: hits only in Rule 8's prohibition paragraph. A hit inside `<clarifying_protocol>` means the replacement was incomplete.

- [ ] **Step 3: Verify the PATTERN label is present**

Run: `grep -n "PATTERN for this kind of question only" supervisor_prompt.txt`
Expected: one line. This label is the fix for the confirmed Gemini failure mode; without it the two example questions get asked verbatim.

- [ ] **Step 4: Verify the skip protocol assumes only the safe lead-in**

Run: `grep -n "Never assume Exceeding" supervisor_prompt.txt`
Expected: one line.

- [ ] **Step 5: Commit**

```bash
git add supervisor_prompt.txt
git commit -m "Rewrite supervisor prompt intake as a scoring interview

Collects EOCS up front and a lead-in selection per factor instead of a
concurrence position, adds the required follow-up for below-EOCS factors,
and changes the skip protocol to assume Meeting rather than concurrence.
Labels the low-evidence example questions as PATTERN not script, the fix
for the Gemini failure mode confirmed in the 2026-07-27 WRI testing."
```

---

### Task 4: Rewrite the thinking process and output format in `supervisor_prompt.txt`

This task makes the file coherent again and adds the self-verification steps that catch the two known Gemini failure modes.

**Files:**
- Modify: `supervisor_prompt.txt` — the `<thinking_process>` block, the `<output_format>` block, and the closing line of the file (currently lines 505–559, shifted by Tasks 1 through 3)

**Interfaces:**
- Consumes: Rules 4, 6, 8, 10, 11, 12, 13 from Task 2, and the protocol steps from Task 3.
- Produces: the two-block output contract — an assessment block in plain text, and a notes block headed exactly `Notes (delete before pasting into CAS2Net):`. Task 6's README rewrite describes this contract to end users and must stay consistent with it.

- [ ] **Step 1: Replace the entire `<thinking_process>` block**

Replace everything from `<thinking_process>` through `</thinking_process>` with:

```
<thinking_process>
Before producing the final output, work through these steps internally. Do not show this thinking in your response.

1. Confirm the employee's career path, broadband level, and EOCS. Confirm which descriptor table applies.
2. For each factor, note the lead-in statement the supervisor selected, the contributions they said the employee did not report, any figures they provided, and any documented evidence for a factor below the EOCS.
3. Map each employee statement and each supervisor-provided contribution to the factor descriptors and discriminators at the correct level.
4. For any factor asserted as Very High, confirm the EOCS falls within the eligible band in <very_high_criteria>. If eligibility is not confirmed, ask rather than write.
5. Draft each factor narrative in this order: the exact lead-in statement as the first sentence, then the contributions the employee did not report, then the mapped contributions in clear and precise specifics, then the DAF guidance alignment sentence.
6. Verify the first sentence of each of the three factors begins with one of the exact lead-in statements from Rule 8, character for character, with no added qualifier and no concurrence phrasing anywhere.
7. Verify every supervisor-provided contribution and every supervisor-provided figure appears in its factor's narrative. If any was dropped to save length, restore it and cut filler instead (Rule 12).
8. Verify all three factor narratives end with the DAF guidance alignment sentence required by Rule 10, and that no citation, section number, page number, date, or quotation from the DAF guidelines was invented.
9. Verify no numeric factor score, score range, OCS, or PAQL number appears anywhere in the output (Rule 4).
10. Verify each factor narrative is within 4,000 characters.
11. Verify the assessment block contains no Markdown formatting (Rule 13).
12. Confirm the notes block is separate from the assessment block and records character counts, any factor thin on evidence, any assumption made under the skip protocol, and a missing EOCS if applicable.
</thinking_process>
```

- [ ] **Step 2: Replace the entire `<output_format>` block**

Replace everything from `<output_format>` through `</output_format>` with:

```
<output_format>
Produce two blocks. The first is the assessment, in plain text, which the supervisor pastes into CAS2Net. The second is a short notes block for the supervisor only.

Block 1 — the assessment:

Career Path and Level: [Career path and broadband level]
Expected OCS: [The EOCS the supervisor provided, or "not provided"]

Job Achievement and/or Innovation

[The exact lead-in statement as the first sentence. Then the contributions the employee did not report, when the supervisor provided them. Then the employee's contributions mapped to this factor's descriptors and discriminators, in clear and precise specifics, referencing specific accomplishments. Then one to two sentences on how the contributions align with DAF guidance and support the recommended PAQL score.]

Communication and/or Teamwork

[The same four-part structure, opening with the exact lead-in statement for this factor.]

Mission Support

[The same four-part structure, opening with the exact lead-in statement for this factor.]

Review this assessment against the employee's actual performance before finalizing in CAS2Net. This tool assists but does not replace supervisory judgment.

Block 2 — notes for the supervisor. Separate this block clearly from the assessment above and head it exactly as shown:

Notes (delete before pasting into CAS2Net):
- [Character count for each factor against the 4,000-character CAS2Net limit]
- [Any factor where evidence was thin, and what documentation would strengthen it next cycle]
- [Any assumption made under the skip protocol, including an assumed lead-in statement]
- [A note if the EOCS was not provided]
</output_format>
```

- [ ] **Step 3: Replace the closing line of the file**

Replace the final line (currently "I will wait for the employee's self-assessment contribution statements and the rated individual's career path and level. When you paste them, I will first ask the clarifying questions before producing the assessment.") with:

```
I will wait for the employee's self-assessment contribution statements, along with the employee's career path, broadband level, and EOCS. When you provide them, I will ask the clarifying questions before producing the assessment.
```

- [ ] **Step 4: Verify the file no longer references concurrence outside the prohibition**

Run: `grep -n "concur" supervisor_prompt.txt`
Expected: hits only within Rule 8's "NO LONGER COMPLIANT" paragraph. Any other hit is a defect.

- [ ] **Step 5: Verify the removed sections are gone**

Run: `grep -n "Overall Assessment\|four required elements\|quality-of-performance" supervisor_prompt.txt`
Expected: no output. The Overall Assessment section recommended an overall score range and is removed.

- [ ] **Step 6: Verify the notes block header is exact**

Run: `grep -n "Notes (delete before pasting into CAS2Net):" supervisor_prompt.txt`
Expected: one line.

- [ ] **Step 7: Read the whole file once, start to finish**

Read `supervisor_prompt.txt` in full. Confirm: every rule number referenced in `<clarifying_protocol>`, `<thinking_process>`, and `<output_format>` points at the rule that actually bears that number in Task 2's block; no XML tag is unclosed; the three descriptor tables are intact.

- [ ] **Step 8: Commit**

```bash
git add supervisor_prompt.txt
git commit -m "Rewrite supervisor prompt output format and verification steps

Splits output into a plain-text assessment block for CAS2Net and a
separate notes block to delete, removes the Overall Assessment section
and its score-range recommendation, and collapses the per-factor
structure from four elements to three plus the DAF sentence. Adds
thinking-process checks for verbatim lead-ins, retention of
supervisor-provided figures, absence of invented DAF citations, and
absence of any stated score."
```

---

### Task 5: Update `assessment_review_prompt.txt`

The review prompt currently flags any deviation from the three concurrence phrases as CRITICAL, which after Tasks 1–4 would fail every compliant appraisal. This file uses plain Markdown headers and bullets, not XML tags — match that convention.

**Files:**
- Modify: `assessment_review_prompt.txt:29-44` (CHECK 1)
- Modify: `assessment_review_prompt.txt:83` (CHECK 3 stale minimum)
- Modify: `assessment_review_prompt.txt:126-137` (CHECK 5 required elements)
- Modify: `assessment_review_prompt.txt:171-177` (CHECK 6 Very High)

**Interfaces:**
- Consumes: the four exact lead-in statements as written in Task 2's Rule 8. They must match character for character across both files.
- Produces: nothing consumed by later tasks. Task 6 describes CHECK 1 to end users and must match the count of four.

- [ ] **Step 1: Replace CHECK 1**

Replace lines 29–44, from `**CHECK 1: Supervisor Concurrence Statements**` through the line `For partial or non-concurrence, verify that the supervisor states specific reasons.`, with:

```
**CHECK 1: Supervisor Lead-In Statements**
Priority: CRITICAL
Each supervisor assessment block (one per factor) MUST begin with one of exactly four approved lead-in statements. The lead-in must equal the recommended numerical score for that factor (2026 AcqDemo business rules, 7.5.4):

1. "Meeting expected contributions" — the employee is scoring at their EOCS for the factor
2. "Exceeding expected contributions" — the employee is scoring above their EOCS for the factor
3. "Partially meeting expected contributions" — the employee is scoring below their EOCS for the factor
4. "Not meeting expected contributions" — the employee is scoring below their EOCS for the factor

One exception applies (9.1.4): when coding a "Very High" score required scoring one or two factors below the EOCS, the lead-in for those factors reads "meeting or exceeding expected contributions."

Flag as CRITICAL any variation, paraphrase, or deviation from these lead-in statements. Common non-compliant examples include:
- "I concur with the employee's self-assessment" — along with "I partially concur with the employee's self-assessment" and "I do not concur with the employee's self-assessment." These were the approved openers in prior cycles and are now retired. Expect this to be the most common finding this cycle.
- "I agree with the annual assessment"
- "I fully concur with the annual assessment of [name]'s performance"
- Any phrasing that adds a qualifier such as "fully," "strongly," "clearly," or "overall"
- A narrative that opens with substantive content and places the lead-in statement later

For "Partially meeting expected contributions" and "Not meeting expected contributions," verify the narrative clearly describes the inadequate contributions or unmet performance expectations (7.5.4.3).
```

- [ ] **Step 2: Correct the stale W-R-I minimum in CHECK 3**

On line 83, replace:

```
- This mandatory objective does NOT count toward the 2 required W-R-I statements per factor (so a supervisor needs the mandatory objective PLUS 2 additional W-R-I statements under Job Achievement).
```

with:

```
- This mandatory objective does NOT count toward the 3 required W-R-I statements per factor (so a supervisor needs the mandatory objective PLUS 3 additional W-R-I statements under Job Achievement). The 2-per-factor figure applies only to first-year organizations for the current cycle.
```

- [ ] **Step 3: Replace the four required elements in CHECK 5**

Replace the numbered list at lines 128–131 (items 1 through 4) with:

```
1. **Lead-in statement** — Opening line using one of the four approved lead-in statements (see Check 1).
2. **Missing contributions** — Contributions the employee omitted from their self-assessment. For a factor marked "Meeting expected contributions," the narrative must include contributions the employee did not report; for "Exceeding expected contributions," it must include the significant ones (7.5.4.1 and 7.5.4.2).
3. **Summary of contributions** — Contributions mapped to factor descriptors and discriminators, characterizing the resulting impact to mission. Should use factor descriptor and discriminator language from the employee's career path and broadband level.
4. **DAF guidance alignment statement** — One to two sentences addressing how the employee's contributions align with DAF guidance and support the recommended PAQL score (7.5.5).
```

- [ ] **Step 4: Add the Very High eligibility gate to CHECK 6**

After line 171 (`If any numeric score falls outside the valid range for the stated level, flag as CRITICAL.`), insert:

```
Very High eligibility (9.1.2): a "Very High" categorical rating or its associated scores may only be awarded to employees whose Expected OCS falls within the band for their career path:
- NH: EOCS 96–100
- NJ: EOCS 79–83
- NK: EOCS 57–61

If a Very High score appears and the Expected OCS falls outside that band, flag as CRITICAL. When Very High is assigned, verify the narrative states specifically how the employee exceeds the top of the broadband for that factor.
```

- [ ] **Step 5: Verify the lead-ins match Task 2 character for character**

Run: `grep -o "Meeting expected contributions\|Exceeding expected contributions\|Partially meeting expected contributions\|Not meeting expected contributions" assessment_review_prompt.txt | sort -u`
Expected: exactly four distinct lines, matching the same command run against `supervisor_prompt.txt`.

Run the same command against `supervisor_prompt.txt` and `templates/assessment_package_template.md` and compare. Any wording difference between the three files is a defect.

- [ ] **Step 6: Verify the retired phrases now appear only as non-compliant examples**

Run: `grep -n "concur" assessment_review_prompt.txt`
Expected: hits only inside CHECK 1's non-compliant examples list.

- [ ] **Step 7: Commit**

```bash
git add assessment_review_prompt.txt
git commit -m "Align review prompt CHECK 1 with guide lead-in statements

CHECK 1 becomes Supervisor Lead-In Statements and enforces the four
phrases from 7.5.4, moving the retired concurrence openers into the
non-compliant examples list. CHECK 5 swaps the concurrence element for
the 7.5.5 DAF guidance sentence, CHECK 6 gains the 9.1.2 Very High EOCS
gate, and CHECK 3's stale 2-statement minimum is corrected to 3."
```

---

### Task 6: Update `README.md`

Two changes travel together here: the supervisor workflow description, and the platform and model swap. Keep the audience rule in mind — this file is read by people who have never used a chat-based AI tool.

**Files:**
- Modify: `README.md:6` (tool list entry)
- Modify: `README.md:15-16` (settings table)
- Modify: `README.md:26,107,153,199` (site name in four walkthroughs)
- Modify: `README.md:167-178` (Steps 3 and 4 of the supervisor walkthrough)
- Modify: `README.md:184,186` (two tips)
- Modify: `README.md:195,223` (review prompt description and check list)

**Interfaces:**
- Consumes: the two-block output contract from Task 4 and the CHECK 1 rewrite from Task 5. The README must describe what those actually do.
- Produces: nothing consumed by later tasks.

- [ ] **Step 1: Update the tool list entry on line 6**

Replace:

```
- **Supervisor Assessment Generator** (`supervisor_prompt.txt`) — generates PAQL-aligned supervisory appraisals from an employee's self-assessment contribution statements.
```

with:

```
- **Supervisor Assessment Generator** (`supervisor_prompt.txt`) — turns an employee's self-assessment into a supervisory annual assessment that follows the 2026 AcqDemo business rules.
```

- [ ] **Step 2: Update the settings table on lines 15–16**

Replace:

```
| Platform | chat.genai.army.mil |
| Model | Claude 4.6 O |
```

with:

```
| Platform | https://genai.mil/ |
| Model | Gemini 3.1 Pro (Gemini 3.6 Flash also works if Pro is unavailable) |
```

- [ ] **Step 3: Update the site name in the four walkthroughs**

On lines 26, 107, 153, and 199, replace `chat.genai.army.mil` with `https://genai.mil/`. The surrounding sentence stays as it is.

Run afterward: `grep -c "chat.genai.army.mil" README.md`
Expected: `0`

- [ ] **Step 4: Replace Step 3 of the supervisor walkthrough (lines 167–174)**

Replace the heading and both paragraphs with:

```
### Step 3: Answer the Questions About Scoring

First you will be asked for the employee's Expected Overall Contribution Score (EOCS). This is required — the wording of the assessment depends on it.

Then, for each of the three factors, you will be asked:
- Which statement applies: Meeting expected contributions, Exceeding expected contributions, Partially meeting expected contributions, or Not meeting expected contributions
- Any contributions the employee left out of their self-assessment
- Any additional context about scope, scale, or impact

The first sentence of each factor is the statement you picked, word for word, because the business rules require it to match the score you are recommending. If you pick Partially meeting or Not meeting for a factor, you will also be asked what documented feedback or evidence from during the year supports that — the rules require the written assessment to contain no surprises for the employee.

If a factor has limited evidence even after your input, you will get one targeted follow-up question about that factor. If you have nothing to add, the result is a shorter summary written at the employee's level rather than invented accomplishments.
```

- [ ] **Step 5: Replace Step 4 of the supervisor walkthrough (lines 176–178)**

Replace the heading and paragraph with:

```
### Step 4: Review the Output

You get two blocks. The first is the assessment itself, in plain text with no formatting, ready to paste into CAS2Net. It is organized by factor, and each factor opens with the statement you picked, then covers any contributions the employee left out, then their contributions matched to the descriptors for their career path and level, and closes with one or two sentences on how the work aligns with DAF guidance and supports the recommended quality level.

The second block is a short set of notes for you — character counts against the 4,000-character CAS2Net limit, any factor that was thin on evidence, and any assumption that was made. Delete this second block before pasting anything into CAS2Net.

No numeric score is suggested anywhere. The statement you picked for each factor already carries that. Review everything for accuracy against the employee's actual performance before finalizing in CAS2Net. This tool assists but does not replace your judgment.
```

- [ ] **Step 6: Update two tips (lines 184 and 186)**

Replace line 184:

```
- **Be ready with your concurrence position** — for each factor, know whether you concur, partially concur, or do not concur with the employee's self-assessment and why.
```

with:

```
- **Be ready with your scoring position** — for each factor, know whether the employee is meeting, exceeding, partially meeting, or not meeting expected contributions, and have the employee's Expected OCS on hand.
```

Replace line 186:

```
- **Expect a score range, not a number** — the LLM recommends an aligned PAQL range and identifies whether performance meets, exceeds, or falls short of level expectations. Final numeric scoring is your decision.
```

with:

```
- **Expect no score at all** — scoring is your decision and the pay pool's. The opening statement you pick for each factor is what communicates it.
```

- [ ] **Step 7: Update the review prompt description (lines 195 and 223)**

Replace on line 195 the phrase `It checks supervisor concurrence statements, W-R-I format,` with `It checks the supervisor's opening statements, W-R-I format,`.

Replace line 223:

```
1. **Supervisor Concurrence Statements** (CRITICAL) — must use one of three exact approved phrasings
```

with:

```
1. **Supervisor Lead-In Statements** (CRITICAL) — each factor must open with one of four exact approved statements
```

- [ ] **Step 8: Verify the audience rule holds in the rewritten text**

Run: `grep -n "LLM\|prompt\b\|token\|context window" README.md`
Expected: the rewritten Steps 3, 4, the two tips, and lines 6, 195, 223 produce no hits. Hits elsewhere in the file are pre-existing and out of scope for this plan — do not fix them here, but note their line numbers in the task report so the user can decide on a separate cleanup pass.

- [ ] **Step 9: Commit**

```bash
git add README.md
git commit -m "Update README for lead-in workflow and genai.mil platform

Rewrites the supervisor walkthrough for the EOCS and lead-in intake and
the two-block output, replaces the score-range tips, updates the review
prompt's CHECK 1 description to four lead-in statements, and swaps the
platform to https://genai.mil/ with Gemini 3.1 Pro as the recommended
model."
```

---

### Task 7: Update `CLAUDE.md`

The project instructions name the old site three times and assert that the README still lists a Claude model, which stops being true after Task 6.

**Files:**
- Modify: `CLAUDE.md:7`
- Modify: `CLAUDE.md:29`
- Modify: `CLAUDE.md:30`
- Modify: `CLAUDE.md:32` (the cross-reference example naming the concurrence openers)
- Modify: `CLAUDE.md` — the "Known divergence" section at the end

**Interfaces:**
- Consumes: the completed state of Tasks 1 through 6.
- Produces: nothing.

**Note:** this is the project `CLAUDE.md` checked into the repository, not the user's global `~/.claude/CLAUDE.md`. Do not touch the global file.

- [ ] **Step 1: Update the three site references**

On lines 7, 29, and 30, replace `` `chat.genai.army.mil` `` with `` `https://genai.mil/` ``.

- [ ] **Step 2: Correct the stale clause on line 30**

Within line 30, replace:

```
Treat any remaining Claude-specific assumptions (tag-following quirks, phrasing tuned to Claude's instruction-following style, the README's settings table still listing a Claude model) as stale and due for review
```

with:

```
Treat any remaining Claude-specific assumptions (tag-following quirks, phrasing tuned to Claude's instruction-following style) as stale and due for review. The README settings table now names Gemini 3.1 Pro, with Gemini 3.6 Flash as a fallback; that recommendation is provisional until the two models have been compared on these prompts in live testing
```

- [ ] **Step 3: Update the verbatim-phrasing example on line 32**

Replace:

```
(e.g. `supervisor_prompt.txt`'s three approved concurrence openers, checked in `assessment_review_prompt.txt`'s CHECK 1)
```

with:

```
(e.g. `supervisor_prompt.txt`'s four approved lead-in statements, checked in `assessment_review_prompt.txt`'s CHECK 1 and reproduced in `templates/assessment_package_template.md`)
```

- [ ] **Step 4: Update the "Known divergence" section**

Replace the body of that section with:

```
`docs/superpowers/specs/2026-07-14-assessment-package-template-design.md` §6 recorded three divergences between the prompts and the 2026 guide. Two are now resolved: `wri_prompt.txt` uses the abbreviated `(W)/(R)/(I)` labels, and `supervisor_prompt.txt` uses the guide's Meeting/Exceeding/Partially meeting/Not meeting lead-in statements as of the 2026-08-12 alignment work.

One remains open: `contribution_plan_prompt.txt` still generates unlabeled narrative objectives rather than Attachment C's 3+ labeled contributions per factor (JA1, CT1, MS1). Do not "fix" this silently — it is deliberately deferred pending SME input.

Closeout supervisory assessments (2026 guide 7.4) are covered by no prompt and no template section. Raised and deferred during the 2026-08-12 design; not a defect in existing files.
```

- [ ] **Step 5: Verify no stale site references remain anywhere**

Run: `grep -rn "chat.genai.army.mil" --include=*.md --include=*.txt .`
Expected: hits only in `docs/superpowers/specs/2026-08-12-supervisor-prompt-alignment-design.md`, where they appear as "X becomes Y" instructions describing this change. Any hit in `README.md`, `CLAUDE.md`, or a prompt file is a defect.

- [ ] **Step 6: Commit**

```bash
git add CLAUDE.md
git commit -m "Update project instructions for genai.mil and lead-in statements

Swaps the three platform references, corrects the stale claim that the
README lists a Claude model, updates the verbatim-phrasing example from
the retired concurrence openers to the four lead-in statements, and marks
the supervisor divergence resolved while keeping the contribution plan
item open."
```

---

### Task 8: Live verification on `https://genai.mil/`

No test tooling exists in this repository. Verification means running the revised prompt in a real chat session and checking the output against the rules. **This task is performed by the user, not by an agent** — it requires access to `https://genai.mil/`. An agent reaching this task should stop, hand the checklist below to the user, and wait.

**Files:**
- Modify: none. Findings may generate follow-up edits to files from Tasks 1 through 7.

**Interfaces:**
- Consumes: the finished state of all prior tasks.
- Produces: a go/no-go on merging the branch, and the empirical answer on Gemini 3.1 Pro versus 3.6 Flash.

**Test input:** build a synthetic self-assessment containing no real employee data — invented name, invented accomplishments, NH Level III, EOCS 83. Classification rule applies: nothing real goes into this test.

- [ ] **Step 1: Run the happy path on Gemini 3.1 Pro**

Paste `supervisor_prompt.txt` as the first message of a new chat. Paste the synthetic self-assessment. Answer the intake with a mix: Meeting for Job Achievement, Exceeding for Communication, Meeting for Mission Support, and supply one unreported contribution containing a specific figure.

Confirm all of the following:
- The intake asks for the EOCS before the per-factor questions
- Each factor narrative's first sentence is one of the four lead-in statements, word for word, with no added qualifier
- Each factor narrative ends with a DAF guidance sentence that names no invented section number, page, date, or quotation
- The supplied figure appears in its factor's narrative
- No numeric score, score range, or PAQL number appears anywhere
- The output contains no Markdown formatting
- The notes block is separate and headed `Notes (delete before pasting into CAS2Net):`

- [ ] **Step 2: Run the concurrence regression check**

In a fresh chat, answer the per-factor question with "I concur" instead of picking a lead-in.

Expected: the model asks which of the four lead-in statements applies. A failure is any output containing a concurrence sentence.

- [ ] **Step 3: Run the below-EOCS evidence check**

In a fresh chat, select "Not meeting expected contributions" for one factor and supply no documented feedback.

Expected: the model asks for the documented feedback or supporting evidence before writing that narrative. A failure is a fully written negative narrative with no evidence behind it.

- [ ] **Step 4: Run the scripted-question check**

In a fresh chat, supply a self-assessment that mentions nothing about briefings, written products, customer engagement, or resource planning, and leave one factor thin.

Expected: any follow-up question names that factor and the evidence actually missing from the supplied input. A failure is the model asking either of the two example questions verbatim, or asking about a topic the input never raised.

- [ ] **Step 5: Repeat Steps 1 through 4 on Gemini 3.6 Flash**

Record which checks pass and which fail on each model.

- [ ] **Step 6: Settle the model recommendation**

If 3.6 Flash passes all four checks cleanly, update the `README.md` settings table to recommend it and commit that change. If it fails any check, leave the Gemini 3.1 Pro recommendation in place. Either way, record the result — this converts the provisional recommendation in §5.1 of the design spec into a tested one.

- [ ] **Step 7: Report results and decide on merge**

Report which checks passed on which model. If every check passes, the branch is ready to merge to `main`. If any check fails, capture the exact model output and treat it as a new defect against the responsible file before merging.

---

## Known Limitations

- **No automated verification exists.** Every `grep` in this plan checks that a string is present or absent. None checks that the prompt behaves correctly — only Task 8 does, and only by hand.
- **The DAF Performance Scoring Guidelines (Reference (c)) are not in this repository.** Rule 10 constrains the model to descriptor language and forbids invented citations, which is a mitigation, not a substitute for the source document. If the SME can supply it, the DAF sentence could be grounded properly in a follow-up.
- **`README.md` uses the word "LLM" in passages this plan does not touch** (lines 3, 26, 169 and others). That conflicts with the file's own audience rule. Task 6 Step 8 records the line numbers; cleaning them up is a separate decision for the user.
- **Closeout assessments (guide 7.4) remain uncovered** by any prompt or template. Deliberately deferred.
- **`contribution_plan_prompt.txt` is untouched** and still diverges from Attachment C, by decision, pending SME input.

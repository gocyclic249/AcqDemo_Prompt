# AcqDemo Assessment Package Template — Design Spec

**Date:** 2026-07-14
**Status:** Approved for planning
**Classification:** UNCLASSIFIED — this document and the resulting template contain no CUI. Content becomes CUI only once a specific employee's performance data is entered by an end user.

## 1. Purpose

Produce a single, self-contained fill-in-the-blank document that any employee/supervisor in the organization can copy, fill out, and paste directly into CAS2Net across an entire AcqDemo appraisal cycle — covering the Contribution Plan, Midpoint Assessment, and Annual Assessment. This is Part 1 of a two-part project; Part 2 (revising `wri_prompt.txt`, `contribution_plan_prompt.txt`, and `supervisor_prompt.txt` to match the rules captured here) is out of scope for this spec and will be brainstormed separately.

### Source material (authoritative, in priority order)
1. SME-provided instructions (pasted 2026-07-14) — Attachment C labeling requirements (JA1/JA2/JA3, CT1–3, MS1–3), W-R-I abbreviated label preference (`(W)`/`(R)`/`(I)`, not spelled out), and the org's actual Midpoint reminder text sent to employees/supervisors.
2. `2026guide.pdf` (20 pages, the governing AcqDemo/CCAS program guide) — specifically:
   - **Attachment C — 2026 Contribution Plan Template** (guide pp. 84–86): Value of Position, Brief Summary of Position, three factors each requiring a minimum of 3 labeled expected contributions.
   - **Section 7.3 — Midpoint Assessments**: employees use W-R-I; supervisors do not score or write in W-R-I format; supervisors must document the discussion (date/method) in CAS2Net; midpoints are not grievable.
   - **Section 7.5 — Annual Assessments**: minimum 3 W-R-I statements per factor (9 total; first-year orgs may use 2/6 for the current cycle only), mandatory Supervisory Objective paragraph before any JA W-R-Is (with exact military/civilian/contractor counts), mandatory Acquisition Certification self-certification statement in Mission Support, supervisor lead-in phrases tied to score bands (Meeting / Exceeding / Partially meeting / Not meeting expected contributions), and a mandatory DAF-guidance alignment sentence.
3. Existing `README.md` self-assessment template (Mission Two/One Levels Higher fields) — reused here so the same mission framing carries through the whole cycle and into the existing prompts later.

### Explicitly out of scope
- Rewriting `wri_prompt.txt`, `contribution_plan_prompt.txt`, or `supervisor_prompt.txt`. Two known divergences were found during research and are noted here for the follow-up project, not fixed now:
  - `contribution_plan_prompt.txt` currently generates 2 unlabeled narrative objectives per factor and explicitly forbids C/R/I-style labels — conflicts with Attachment C's requirement for 3+ labeled contributions (JA1, JA2, JA3, ...).
  - `supervisor_prompt.txt` currently opens factor narratives with concurrence phrases ("I concur / partially concur / do not concur") — conflicts with the guide's required lead-ins ("Meeting/Exceeding/Partially meeting/Not meeting expected contributions" for Annual; a distinct agree/disagree + meeting-language opener for Midpoint, with no scoring at all).
- Generating an actual `.docx` binary. Output is Markdown; the SME will convert to docx.
- CAS2Net character-limit tooling (exists already in `contribution_plan_prompt.txt`; not part of this static template).

## 2. Document Structure

Single file: `templates/assessment_package_template.md`. Sections, in chronological cycle order:

1. Cover / How to Use This Document
2. Mission Context
3. Section 1 — Contribution Plan
4. Section 2 — Midpoint Assessment (Employee Self-Assessment + Supervisor Response)
5. Section 3 — Annual Assessment (Employee Self-Assessment + Supervisor Response)

## 3. Section-by-Section Content

### 3.1 Cover / How to Use This Document

Plain-language block (non-technical audience, per existing README tone) explaining:
- What the four sections below are and when each is used in the cycle (start of cycle → Contribution Plan; March/April → Midpoint; by 30 September → Annual).
- That guidance text is marked distinctly (e.g., `> GUIDANCE — delete before submitting`) and should be removed before pasting the fillable fields into CAS2Net.
- That fillable fields are plain text and should not carry Markdown formatting (bold/headers/bullets) into CAS2Net, consistent with `contribution_plan_prompt.txt`'s existing plain-text output rule.
- A one-line pointer that this same information (mission context, accomplishments) can later be fed into the WRI/Contribution Plan/Supervisor Assistant prompts in this repo for AI-assisted drafting.

### 3.2 Mission Context

Filled in once at the start of the cycle, referenced throughout every later section (Contribution Plan mission tie-ins, WRI Impact statements, supervisor's DAF-guidance sentence). Reuses the exact framing already in `README.md`:

```
Mission Two Levels Higher (usually Delta):
[Paste your organization's mission two levels above yours.]

Mission One Level Higher (usually Squadron):
[Paste your direct organization's mission statement one level above yours.]
```

### 3.3 Section 1 — Contribution Plan

Mirrors Attachment C structure and content as closely as possible, in fillable form:

- `VALUE OF POSITION: XX` fillable line, called out at the top per the guide's instruction to place it "at the beginning of the Brief Summary of Position."
- `Brief Summary of Position:` fillable field (2–3 lines: primary duties, mission result, scope of responsibility), restating "Current Value of Position is: XX" per the guide's exact required phrasing.
- For each of the three factors (Job Achievement and/or Innovation; Communication and/or Teamwork; Mission Support), in this order:
  - The factor's guide description ("This factor is about...")
  - The "Think about" bullet prompts from the guide
  - The guide's worked example contributions (JA1–JA3, CT1–CT3, MS1–MS2), kept as guidance text to delete
  - The fillable `Employee [FACTOR NAME] Contributions:` block with a **minimum of 3 labeled blanks** (JA1/JA2/JA3, CT1/CT2/CT3, MS1/MS2/MS3) and a visible `(Optional: JA4, JA5, etc.)` line, matching the guide exactly.
- Note reproducing the guide's own instructions verbatim at the top of this section (SMART objectives, AI-tool use, Pay Pool readability, VoP-first ordering) since they are short and directly relevant.

### 3.4 Section 2 — Midpoint Assessment

**Employee Self-Assessment:**
- Reminder block reusing the SME's actual org reminder text verbatim:
  - Must complete a midpoint self-assessment in W-R-I format.
  - `(W):` / `(R):` / `(I):` labels — abbreviated form per SME instruction (not "What:"/"Result:"/"Impact:").
  - Note: midpoints are mini versions of the annual; at least one W-R-I per factor (can be more); these W-R-Is can be copied into the Annual Assessment.
- Fillable blocks for each factor, minimum 1 W-R-I per factor (not the Annual minimum of 3), each with `(W):` `(R):` `(I):` blanks.
- If the employee has a mandatory Acquisition Coded Position Objective, an `[IF APPLICABLE]`-marked self-certification statement field (not W-R-I format, per guide 7.3.1).

**Supervisor Response:**
- Mandatory opening sentence template, reusing the SME's exact org language:
  > "I agree/disagree with the employee's midpoint assessment. Mr. XXX/Ms. XXX (or the employee) is not meeting/partially meeting/meeting/exceeding expected contributions."
- Explicit note: no scores are assigned at midpoint (guide 7.3.3).
- Reminder fields for the mandatory discussion: supervisors must meet with the employee to discuss contribution plan progress, areas needing improvement, available assistance, and expectations for the remainder of the cycle — and must document the date/method of that discussion in CAS2Net (guide 7.3.4).

### 3.5 Section 3 — Annual Assessment

**Employee Self-Assessment:**
- Reminder block: W-R-I format required; **minimum 3 W-R-I statements per factor, 9 total** (guide 7.5.1.1); `[IF APPLICABLE — first-year org]` variant note for the 2-per-factor/6-total exception.
- `[IF APPLICABLE — supervisory objective]` field: paragraph (not W-R-I) stating exact military/civilian/contractor counts supervised, placed in Job Achievement and/or Innovation before any W-R-I statements (guide 7.5.2/7.5.2.1). Does not count toward the 3-per-factor minimum.
- `[IF APPLICABLE — Acquisition Coded Position Objective]` field: self-certification statement in Mission Support (not W-R-I format, does not count toward the minimum) (guide 7.5.3).
- Fillable `(W):` `(R):` `(I):` blocks per factor, minimum 3 each.
- Reminder note: do not duplicate prior-year statements or reuse a statement across factors (guide 7.5.1.2).

**Supervisor Response:**
- Per-factor mandatory lead-in, one of the four exact guide phrases (guide 7.5.4.1–7.5.4.3), presented as selectable options:
  - "Meeting expected contributions..." (scoring at EOCS — must include specifics and any contributions the employee didn't self-report)
  - "Exceeding expected contributions..." (above EOCS — specifics + significant additional contributions)
  - "Partially meeting expected contributions..." / "Not meeting expected contributions..." (below EOCS — must reference documented feedback sessions/evidence through the cycle)
- Fillable field for the required 1–2 sentence DAF-guidance alignment statement per factor supporting the recommended PAQL score (guide 7.5.5).

## 4. Formatting Conventions

- **Air Force writing style (AFH 33-337, The Tongue and Quill).** This is a formal document, and all prose authored for it — cover instructions, guidance text, and reminder/rule passages not quoted verbatim from the guide or SME — follows AFH 33-337: active voice, subject-verb-object structure, precise and objective language, no colloquialisms, no flowery or subjective wording, tight sentences. This mirrors the style rules already codified in `wri_prompt.txt` and `contribution_plan_prompt.txt`, so the template and the prompts read consistently.
- Plain Markdown only: `#`/`##` headers and bold labels for structure; no tables.
- Every guidance/example passage is visually distinguished (blockquote `>` prefix, labeled `GUIDANCE`) from fillable content so a user can delete all guidance in one pass before copying fields into CAS2Net.
- Fillable fields use a consistent blank marker, e.g. `JA1: ` / `(W): ` / `VALUE OF POSITION: `, with no markdown emphasis inside the blank itself (so bold/asterisks don't get pasted into CAS2Net).
- Conditional/mandatory-if-applicable content is marked `[IF APPLICABLE — <condition>]` rather than omitted, since one shared template serves everyone regardless of role or org tenure.
- Reminder/rule text sourced from the guide or SME instructions is reproduced close to verbatim (not paraphrased), since these are compliance-relevant statements employees and supervisors are expected to follow precisely.

## 5. File Location

`templates/assessment_package_template.md` (new `templates/` directory, parallel to the existing `*_prompt.txt` files and `ExampleEvaluation/`).

## 6. Open Items for Part 2 (tracked, not resolved here)

- Align `contribution_plan_prompt.txt` output format to Attachment C's 3-labeled-contributions-per-factor structure (currently 2 unlabeled narrative objectives).
- Align `supervisor_prompt.txt` opening-phrase rule to the guide's Meeting/Exceeding/Partially meeting/Not meeting language (Annual) and the agree/disagree + meeting-language opener (Midpoint), replacing the current concurrence-phrase rule.
- Align `wri_prompt.txt` output labels to abbreviated `(W)/(R)/(I)` per SME preference (currently spells out "What:/Result:/Impact:").

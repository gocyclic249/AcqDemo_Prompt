# AcqDemo Assessment Package Template Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce `templates/assessment_package_template.md`, a single fillable Markdown document covering Mission Context, the Contribution Plan, the Midpoint Assessment, and the Annual Assessment for one AcqDemo appraisal cycle, ready for SME review and later docx conversion.

**Architecture:** One Markdown file, built section by section (Cover/Mission Context, Contribution Plan, Midpoint, Annual) via one Write and three Edit calls. Each task appends to a unique anchor at the end of the prior task's content, so tasks stay ordered and each addition is independently verifiable with `grep`.

**Tech Stack:** Markdown only. `grep` is used as the verification tool in place of a test runner — there is no code and nothing to compile or execute.

## Global Constraints

- Classification: UNCLASSIFIED. No CUI or classified information appears in the template itself (spec §1).
- Output is plain Markdown only — headers and bold labels for structure, no tables (spec §4).
- Guidance text is visually distinguished via `> GUIDANCE` blockquotes, distinct from fillable fields, so it can be deleted in one pass before pasting a section into CAS2Net (spec §4).
- Fillable field labels carry no trailing whitespace and no Markdown emphasis inside the blank itself (spec §4).
- Conditional / mandatory-if-applicable content is marked `[IF APPLICABLE — <condition>]`, never omitted (spec §4).
- All originally authored prose (not quoted from the guide or the SME) follows AFH 33-337 (The Tongue and Quill): active voice, subject-verb-object structure, precise and objective language, no colloquialisms or flowery wording, tight sentences (spec §4).
- Reminder/rule text sourced from the 2026 guide or the SME is reproduced close to verbatim, not paraphrased (spec §4).
- File location: `templates/assessment_package_template.md` (spec §5).
- Source of truth for facts: `docs/superpowers/specs/2026-07-14-assessment-package-template-design.md`.

---

### Task 1: Scaffold file — Cover and Mission Context

**Files:**
- Create: `templates/assessment_package_template.md`

**Interfaces:**
- Consumes: nothing (first task).
- Produces: `templates/assessment_package_template.md` ending in a `---` divider after the Mission Context section. Task 2 appends immediately after that final `---`.

- [ ] **Step 1: Verify the file does not exist yet**

Run: `test -f templates/assessment_package_template.md && echo EXISTS || echo MISSING`
Expected: `MISSING`

- [ ] **Step 2: Create the templates directory and write the file**

Create the directory, then create `templates/assessment_package_template.md` with exactly this content:

```markdown
# AcqDemo Assessment Package Template

**Classification: UNCLASSIFIED** — This template is UNCLASSIFIED. Content becomes CUI once you enter employee-specific performance data. Do not enter classified information in any field.

## How to Use This Document

This document holds every item you will submit to CAS2Net across one AcqDemo appraisal cycle: the Contribution Plan, the Midpoint Assessment, and the Annual Assessment. Complete each section at the point in the cycle where it applies.

Guidance text appears in blockquotes labeled `GUIDANCE`. Delete all guidance text before you paste a section into CAS2Net. Fillable fields appear as blank labels, for example `JA1:`, with no bold, italics, or other Markdown formatting — copy them exactly as written, because CAS2Net fields accept plain text only.

Complete the sections in this order:

1. Mission Context — complete once, at the start of the cycle.
2. Section 1: Contribution Plan — complete at the start of the cycle, a change in position, or a new appointment.
3. Section 2: Midpoint Assessment — complete in March or April.
4. Section 3: Annual Assessment — complete by 30 September.

You can reuse your Mission Context and accomplishments as input to the WRI, Contribution Plan, and Supervisor Assistant prompts in this repository for AI-assisted drafting.

---

## Mission Context

> GUIDANCE: Enter your organization's mission statements once. Reference them when you write Impact statements and Contribution Plan objectives throughout the cycle.

Mission Two Levels Higher (usually Delta):


Mission One Level Higher (usually Squadron):


---
```

Run: `mkdir -p templates`, then create the file above with the Write tool.

- [ ] **Step 3: Verify the required content is present**

Run:
```bash
grep -qF "# AcqDemo Assessment Package Template" templates/assessment_package_template.md && \
grep -qF "Classification: UNCLASSIFIED" templates/assessment_package_template.md && \
grep -qF "## How to Use This Document" templates/assessment_package_template.md && \
grep -qF "## Mission Context" templates/assessment_package_template.md && \
grep -qF "Mission Two Levels Higher (usually Delta):" templates/assessment_package_template.md && \
grep -qF "Mission One Level Higher (usually Squadron):" templates/assessment_package_template.md && \
echo ALL_PRESENT
```
Expected: `ALL_PRESENT`

- [ ] **Step 4: Commit**

```bash
git add templates/assessment_package_template.md
git commit -m "Add cover and mission context to assessment package template"
```

---

### Task 2: Add Section 1 — Contribution Plan

**Files:**
- Modify: `templates/assessment_package_template.md` (append after Task 1's trailing `---`)

**Interfaces:**
- Consumes: the file ending in the Mission Context section's trailing `---`, produced by Task 1.
- Produces: the file now ending in the Contribution Plan section's trailing `---`. Task 3 appends immediately after that.

- [ ] **Step 1: Verify Section 1 is not present yet**

Run: `grep -c "## Section 1: Contribution Plan" templates/assessment_package_template.md`
Expected: `0`

- [ ] **Step 2: Append the Contribution Plan section**

Use the Edit tool. `old_string` is the exact tail of the file from Task 1:

```
Mission Two Levels Higher (usually Delta):


Mission One Level Higher (usually Squadron):


---
```

`new_string` is the same text with the following appended immediately after it:

```markdown

## Section 1: Contribution Plan

> GUIDANCE: Complete this section at the start of a new appraisal cycle, a change in position, or a new appointment. Source: 2026 AcqDemo Program Guide, Attachment C.
>
> Attachment C instructions:
> - Contribution plans should reflect only the expected level of contribution; leave exceedances to the midpoint and annual assessments.
> - Write so that other readers, including Pay Pool members, understand what you are communicating.
> - Use strong SMART objectives.
> - Use AI tools, and ensure the plan meets the appropriate AcqDemo broadband level, for example NH-III or NH-IV.
> - State the Value of Position at the beginning of the Brief Summary of Position.
> - Each factor requires a minimum of three (3) labeled expected contributions, for example JA1, CT1, MS1. Align each entry with the appropriate AcqDemo factor descriptors, and write clear, meaningful, measurable expected results.

VALUE OF POSITION:

Brief Summary of Position: Current Value of Position is:
> GUIDANCE: In 2–3 lines, describe your primary duties, mission result, and scope of responsibility. Example: "Current Value of Position is: 93. Provides engineering expertise to support planning, analysis, design, integration, and execution of technical solutions for assigned programs. Ensures technical rigor, compliance with standards, and alignment with mission objectives."



### Job Achievement and/or Innovation (JA)

> GUIDANCE: This factor covers what you accomplish. It reflects your technical expertise, quality of work, problem-solving, initiative, and innovation.
>
> Think about:
> - Technical Excellence: How will you apply or grow your technical skills on a project?
> - Quality: How will you ensure your work is accurate, thorough, and delivered on time?
> - Problem-Solving: What complex challenges will you solve?
> - Initiative and Innovation: How will you improve a process, develop a new tool, or suggest a creative solution?
>
> Example Contributions:
> - JA1: (Contribution) Develop and implement an automated testing script for the ABC software module to (Result) reduce manual testing time by 20% and improve defect detection.
> - JA2: (Contribution) Lead the redesign of the user interface for the legacy system, resulting in (Result) a 15% improvement in user-reported satisfaction.
> - JA3: (Contribution) Author a technical white paper on applying AI to our data analysis process to (Result) share best practices and establish our team as a subject matter expert.

[IF APPLICABLE — Supervisor]: State your supervised counts before JA1, for example "I supervise 0 military, 10 civilians, and manage 6 contractors."

Employee Job Achievement and/or Innovation Contributions:
- JA1:
- JA2:
- JA3:
- (Optional: JA4, JA5, etc.)

### Communication and/or Teamwork (CT)

> GUIDANCE: This factor covers how you work with others. It reflects your clarity in communication, collaboration, responsiveness, and ability to foster positive team dynamics.
>
> Think about:
> - Clear Communication: How will you keep teammates and stakeholders informed, for example through meetings, reports, or presentations?
> - Collaboration: How will you actively work with others to achieve a shared goal?
> - Mentorship and Team Building: How will you help or mentor others?
> - Relationship Building: How will you build and maintain effective working relationships across teams or with external partners?
>
> Example Contributions:
> - CT1: (Contribution) Facilitate weekly project sync meetings with the Integrated Project Team (IPT), ensuring clear communication of priorities and risks via meeting minutes with Contribution items.
> - CT2: (Contribution) Mentor one junior engineer on the team by providing regular guidance, (Result) fostering their professional growth and technical skills.
> - CT3: (Contribution) Develop and maintain a shared knowledge base for project documentation to (Result) improve information sharing and reduce onboarding time for new team members.

Employee Communication and/or Teamwork Contributions:
- CT1:
- CT2:
- CT3:
- (Optional: CT4, CT5, etc.)

### Mission Support (MS)

> GUIDANCE: This factor covers your connection to the bigger picture. It reflects your understanding of the organizational mission, your reliability, your stewardship of resources, and your support for broader goals.
>
> Think about:
> - Mission Alignment: How does your work directly advance the organization's strategic goals?
> - Reliability: How will you demonstrate dependability in meeting deadlines and commitments?
> - Resource Management: How will you use government resources — time, budget, equipment — efficiently?
> - Organizational Contribution: How will you support broader initiatives, for example process improvement, safety programs, or command-wide efforts?
>
> Example Contributions:
> - MS1: (Contribution) Identify and document at least two process improvement opportunities within our division's workflow, (Result) presenting recommendations to leadership for consideration.
> - MS2: (Contribution) Serve as the team lead for the annual Combined Federal Campaign (CFC) drive to (Result) support a key organizational initiative and promote community engagement.

[IF APPLICABLE — Acquisition Coded Position Objective]: State your self-certification statement here, for example "I am on track to complete by [date]," "I completed the certification as of [date]," or "I received a waiver until [date]."

Employee Mission Support Contributions:
- MS1:
- MS2:
- MS3:
- (Optional: MS4, MS5, etc.)

---
```

- [ ] **Step 3: Verify the section and its labeled contributions are present**

Run:
```bash
grep -qF "## Section 1: Contribution Plan" templates/assessment_package_template.md && \
grep -qF "VALUE OF POSITION:" templates/assessment_package_template.md && \
[ "$(grep -cF 'JA1:' templates/assessment_package_template.md)" -eq 3 ] && \
[ "$(grep -cF 'CT1:' templates/assessment_package_template.md)" -eq 2 ] && \
[ "$(grep -cF 'MS1:' templates/assessment_package_template.md)" -eq 2 ] && \
[ "$(grep -cF 'MS3:' templates/assessment_package_template.md)" -eq 1 ] && \
grep -qF "(Optional: JA4, JA5, etc.)" templates/assessment_package_template.md && \
grep -qF "[IF APPLICABLE — Supervisor]" templates/assessment_package_template.md && \
grep -qF "[IF APPLICABLE — Acquisition Coded Position Objective]" templates/assessment_package_template.md && \
grep -qF "reduce manual testing time by 20%" templates/assessment_package_template.md && \
echo ALL_PRESENT
```
Expected: `ALL_PRESENT`

(MS1/CT1 each appear twice — once in the guide's worked example, once in the fillable list. JA1 appears three times: once in Task 1's "How to Use This Document" text, which uses `` `JA1:` `` as its example of a fillable label, plus the guide's worked example and the fillable list here. MS3 appears once, since the guide gives no MS3 worked example.)

- [ ] **Step 4: Commit**

```bash
git add templates/assessment_package_template.md
git commit -m "Add Contribution Plan section to assessment package template"
```

---

### Task 3: Add Section 2 — Midpoint Assessment

**Files:**
- Modify: `templates/assessment_package_template.md` (append after Task 2's trailing `---`)

**Interfaces:**
- Consumes: the file ending in the Contribution Plan section's trailing `---`, produced by Task 2.
- Produces: the file now ending in the Midpoint Assessment section's trailing `---`. Task 4 appends immediately after that.

- [ ] **Step 1: Verify Section 2 is not present yet**

Run: `grep -c "## Section 2: Midpoint Assessment" templates/assessment_package_template.md`
Expected: `0`

- [ ] **Step 2: Append the Midpoint Assessment section**

Use the Edit tool. `old_string` is the exact tail of the file from Task 2:

```
Employee Mission Support Contributions:
- MS1:
- MS2:
- MS3:
- (Optional: MS4, MS5, etc.)

---
```

`new_string` is the same text with the following appended immediately after it:

```markdown

## Section 2: Midpoint Assessment

> GUIDANCE: Complete this section in March or April, midway through the appraisal cycle. Source: 2026 AcqDemo Program Guide, Section 7.3, and organizational Midpoint reminders.

### Employee Self-Assessment

> GUIDANCE — Reminders:
> - Employees must complete a midpoint self-assessment in the W-R-I format.
> - Midpoints are mini versions of your annual self-assessment — an opportunity to show what you have contributed.
> - Include at least one W-R-I for each factor. You may include more.
> - You can copy these W-R-Is into your Annual Assessment.

[IF APPLICABLE — Acquisition Coded Position Objective]: Include your self-certification statement, for example "I am on track to complete by [date]," "I completed the certification as of [date]," or "I received a waiver until [date]." This statement does not need to be in W-R-I format.

**Job Achievement and/or Innovation**
(W):
(R):
(I):

**Communication and/or Teamwork**
(W):
(R):
(I):

**Mission Support**
(W):
(R):
(I):

### Supervisor Response

> GUIDANCE — Reminders:
> - Supervisors must complete a written supervisory assessment but do not assign scores at midpoint.
> - Supervisors must meet with the employee to discuss contribution plan progress, areas needing improvement, assistance available, and expectations for the remainder of the cycle.
> - Supervisors must document the midpoint assessment discussion in CAS2Net, including the date and method of communication.

Supervisor Response: I agree/disagree with the employee's midpoint assessment. Mr. XXX/Ms. XXX (or the employee) is not meeting/partially meeting/meeting/exceeding expected contributions.

Discussion date and method documented in CAS2Net:

---
```

- [ ] **Step 3: Verify the section, the abbreviated W-R-I labels, and the supervisor lead-in are present**

Run:
```bash
grep -qF "## Section 2: Midpoint Assessment" templates/assessment_package_template.md && \
[ "$(grep -cF '(W):' templates/assessment_package_template.md)" -eq 3 ] && \
[ "$(grep -cF '(R):' templates/assessment_package_template.md)" -eq 3 ] && \
[ "$(grep -cF '(I):' templates/assessment_package_template.md)" -eq 3 ] && \
grep -qF "I agree/disagree with the employee's midpoint assessment" templates/assessment_package_template.md && \
grep -qF "not meeting/partially meeting/meeting/exceeding expected contributions" templates/assessment_package_template.md && \
! grep -qE "^(What|Result|Impact):" templates/assessment_package_template.md && \
echo ALL_PRESENT
```
Expected: `ALL_PRESENT`

(The negative check confirms the template uses the SME's required abbreviated `(W)/(R)/(I)` labels and never the spelled-out `What:/Result:/Impact:` form.)

- [ ] **Step 4: Commit**

```bash
git add templates/assessment_package_template.md
git commit -m "Add Midpoint Assessment section to assessment package template"
```

---

### Task 4: Add Section 3 — Annual Assessment

**Files:**
- Modify: `templates/assessment_package_template.md` (append after Task 3's trailing `---`)

**Interfaces:**
- Consumes: the file ending in the Midpoint Assessment section's trailing `---`, produced by Task 3.
- Produces: the complete file, ending in the Annual Assessment section's trailing `---`.

- [ ] **Step 1: Verify Section 3 is not present yet**

Run: `grep -c "## Section 3: Annual Assessment" templates/assessment_package_template.md`
Expected: `0`

- [ ] **Step 2: Append the Annual Assessment section**

Use the Edit tool. `old_string` is the exact tail of the file from Task 3:

```
Supervisor Response: I agree/disagree with the employee's midpoint assessment. Mr. XXX/Ms. XXX (or the employee) is not meeting/partially meeting/meeting/exceeding expected contributions.

Discussion date and method documented in CAS2Net:

---
```

`new_string` is the same text with the following appended immediately after it:

```markdown

## Section 3: Annual Assessment

> GUIDANCE: Complete this section by 30 September. Source: 2026 AcqDemo Program Guide, Section 7.5.

### Employee Self-Assessment

> GUIDANCE — Reminders:
> - Employees must complete a self-assessment in the W-R-I format.
> - Write a minimum of three (3) W-R-I statements per factor — nine (9) total. [IF APPLICABLE — first-year organization, current cycle only]: write a minimum of two (2) W-R-I statements per factor — six (6) total. The following cycle requires three (3) per factor.
> - Do not duplicate statements from year to year, and do not reuse the same statement across factors.

[IF APPLICABLE — mandatory Supervisory Objective]: Before any W-R-I statement in Job Achievement and/or Innovation, state how many military members, civilian employees, and contractors you supervise or manage, for example "I supervise 0 military, 10 civilians, and manage 6 contractors." Then describe, in paragraph form and not W-R-I format, how you met the supervisory objective. This statement does not count toward the three required W-R-I statements for this factor.

**Job Achievement and/or Innovation** (minimum 3 W-R-I)

WRI 1
(W):
(R):
(I):

WRI 2
(W):
(R):
(I):

WRI 3
(W):
(R):
(I):

(Optional: additional WRI statements)

**Communication and/or Teamwork** (minimum 3 W-R-I)

WRI 1
(W):
(R):
(I):

WRI 2
(W):
(R):
(I):

WRI 3
(W):
(R):
(I):

(Optional: additional WRI statements)

[IF APPLICABLE — Acquisition Coded Position Objective]: Before your W-R-I statements in Mission Support, include your self-certification statement, for example "I am on track to complete by [date]," "I completed the certification as of [date]," or "I received a waiver until [date]." This statement does not need to be in W-R-I format and does not count toward the three required W-R-I statements for this factor.

**Mission Support** (minimum 3 W-R-I)

WRI 1
(W):
(R):
(I):

WRI 2
(W):
(R):
(I):

WRI 3
(W):
(R):
(I):

(Optional: additional WRI statements)

### Supervisor Response

> GUIDANCE — Reminders:
> - Supervisors do not need to write in W-R-I format, but each factor narrative must begin with the lead-in statement matching the recommended score.
> - Meeting expected contributions: the employee is scoring at their Expected Overall Contribution Score (EOCS) for the factor. Explain why the factor is met with clear, precise specifics — not flowery language. Include contributions the employee did not report.
> - Exceeding expected contributions: the employee is scoring above their EOCS for the factor. Explain why the factor exceeds with clear, precise specifics. Include significant contributions the employee did not report.
> - Partially meeting expected contributions or Not meeting expected contributions: the employee is scoring below their EOCS for the factor. Clearly describe the inadequate contributions or unmet expectations, based on documented feedback sessions or other supporting evidence from throughout the cycle.
> - Each factor narrative must also include one to two sentences explaining how the employee's contributions align with DAF guidance and support the recommended PAQL score.

**Job Achievement and/or Innovation**
Meeting/Exceeding/Partially meeting/Not meeting expected contributions.


**Communication and/or Teamwork**
Meeting/Exceeding/Partially meeting/Not meeting expected contributions.


**Mission Support**
Meeting/Exceeding/Partially meeting/Not meeting expected contributions.

---
```

- [ ] **Step 3: Verify the section, the WRI minimums, and the supervisor lead-ins are present**

Run:
```bash
grep -qF "## Section 3: Annual Assessment" templates/assessment_package_template.md && \
grep -qF "minimum of three (3) W-R-I statements per factor" templates/assessment_package_template.md && \
grep -qF "Meeting expected contributions:" templates/assessment_package_template.md && \
grep -qF "Exceeding expected contributions:" templates/assessment_package_template.md && \
grep -qF "Partially meeting expected contributions" templates/assessment_package_template.md && \
grep -qF "Not meeting expected contributions" templates/assessment_package_template.md && \
[ "$(grep -cF '(W):' templates/assessment_package_template.md)" -eq 12 ] && \
[ "$(grep -cF '(R):' templates/assessment_package_template.md)" -eq 12 ] && \
[ "$(grep -cF '(I):' templates/assessment_package_template.md)" -eq 12 ] && \
echo ALL_PRESENT
```
Expected: `ALL_PRESENT`

(12 = 3 from Midpoint + 9 from Annual's three factors × three WRI statements each.)

- [ ] **Step 4: Commit**

```bash
git add templates/assessment_package_template.md
git commit -m "Add Annual Assessment section to assessment package template"
```

---

### Task 5: Full-document verification pass

**Files:**
- Read only: `templates/assessment_package_template.md`
- Read only: `docs/superpowers/specs/2026-07-14-assessment-package-template-design.md`

**Interfaces:**
- Consumes: the complete file produced by Tasks 1–4.
- Produces: nothing new — this task only verifies and, if it finds a defect, fixes it in place before the final commit.

- [ ] **Step 1: Run the no-placeholder / no-forbidden-pattern check**

Run:
```bash
! grep -qiE "TBD|TODO" templates/assessment_package_template.md && \
! grep -qE "^(What|Result|Impact):" templates/assessment_package_template.md && \
! grep -qF '|' templates/assessment_package_template.md && \
echo CLEAN
```
Expected: `CLEAN`

- [ ] **Step 2: Run the full spec-coverage checklist**

Run:
```bash
grep -qF "## How to Use This Document" templates/assessment_package_template.md && \
grep -qF "## Mission Context" templates/assessment_package_template.md && \
grep -qF "## Section 1: Contribution Plan" templates/assessment_package_template.md && \
grep -qF "## Section 2: Midpoint Assessment" templates/assessment_package_template.md && \
grep -qF "## Section 3: Annual Assessment" templates/assessment_package_template.md && \
grep -qF "### Job Achievement and/or Innovation (JA)" templates/assessment_package_template.md && \
grep -qF "### Communication and/or Teamwork (CT)" templates/assessment_package_template.md && \
grep -qF "### Mission Support (MS)" templates/assessment_package_template.md && \
[ "$(grep -cF 'GUIDANCE' templates/assessment_package_template.md)" -ge 8 ] && \
[ "$(grep -cF '[IF APPLICABLE' templates/assessment_package_template.md)" -eq 6 ] && \
echo SPEC_COVERAGE_OK
```
Expected: `SPEC_COVERAGE_OK`

If any check fails, open the file, locate the missing section against the spec (`docs/superpowers/specs/2026-07-14-assessment-package-template-design.md` §3), and fix it before proceeding.

- [ ] **Step 3: Manual AFH 33-337 style spot check**

Read the "How to Use This Document" block and each `GUIDANCE` blockquote you authored (not the verbatim guide/SME quotes). Confirm: active voice throughout, subject-verb-object sentence structure, no colloquialisms, no flowery or subjective language, sentences stay tight. Fix any passive-voice or wordy sentence found.

- [ ] **Step 4: Final commit**

```bash
git add templates/assessment_package_template.md
git status
```
If Step 1–3 required fixes, commit them:
```bash
git commit -m "Fix style and spec-coverage issues found in final review"
```
If no fixes were needed, skip the commit — the file is already fully committed from Tasks 1–4.

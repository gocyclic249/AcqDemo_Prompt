# AcqDemo Performance Management Tool Suite

An LLM-assisted toolkit for AcqDemo performance management, including:
- **Self-Assessment Statement Generator** (`wri_prompt.txt`) — generates W-R-I (What-Result-Impact) contribution statements from a simple list of accomplishments for annual and midpoint self-assessments.
- **Contribution Plan Generator** (`contribution_plan_prompt.txt`) — guides an interactive intake and generates a forward-looking, regulation-compliant Contribution Plan ready to paste directly into CAS2Net at the start of a new appraisal cycle.
- **Supervisor Assessment Generator** (`supervisor_prompt.txt`) — turns an employee's self-assessment into a supervisory annual assessment that follows the 2026 AcqDemo business rules.
- **Assessment Format Reviewer** (`assessment_review_prompt.txt`) — evaluates completed annual or midterm appraisal reports for correct formatting, structural completeness, and CCAS compliance. Supports multi-person PDFs.

**Classification: UNCLASSIFIED** — This tool and its prompts are UNCLASSIFIED. Content becomes CUI when user-specific performance data is entered. Do not include classified information in any inputs.

## Setup

| Setting | Value |
|---------|-------|
| Platform | https://genai.mil/ |
| Model | Gemini 3.1 Pro (Gemini 3.6 Flash also works if Pro is unavailable) |
| Temperature | 0.7 |
| Deep Agent | False |

## Self-Assessment Statement Generator

Use this prompt for **annual and midpoint self-assessments** — turning your past accomplishments into contribution statements using the W-R-I (What-Result-Impact) writing model. Statements are written in AFH 33-337 (The Tongue and Quill) style.

### Step 1: Paste the Prompt as Your First Message

Open `wri_prompt.txt` and copy its entire contents. Start a new conversation on https://genai.mil/ and paste it as your first message in the chat window (not into a system prompt field). This sets up the LLM with the rules and format for generating your statements.

### Step 2: Fill In the Template Below and Paste It Into the Same Chat Window

Copy the template below, fill in your information, and paste it into the same chat window.

```
# Mission Two Levels Higher — Update with your organization's mission
[Paste your organization's mission two levels above yours. This helps
tie your Impact statements to higher-level organizational goals.]

# Mission One Level Higher — Update with your organization's mission
[Paste your direct organization's mission statement one level above yours.]

# Career Path and Level
[Your career path and broadband level, e.g., NH-03, NJ-III, NK-II]

# Appraisal Period
[e.g., Oct 2025 – Sep 2026, or Oct 2025 – Mar 2026 for midpoint]

# Job Title
[Your official job title]

# Classification (Series)
[Your classification series, e.g., 2210, 1550, 0343]

# Brief Job Description (Paste from CAS2Net)
[Copy and paste your brief job description exactly as it appears
in CAS2Net. This helps calibrate the language and scope of your
statements.]

# Factors and Objectives (Paste from CAS2Net)
[Copy and paste your factors and objectives exactly as they appear
in CAS2Net. Include all factors and all objectives under each factor.
Example:

Job Achievement and/or Innovation:
Objective 1: [text]
Objective 2: [text]

Communication and/or Teamwork:
Objective 1: [text]
Objective 2: [text]

Mission Support:
Objective 1: [text]
Objective 2: [text]]

# Clarifying Notes (Optional)
[Add any context that helps clarify your scope, limitations, or
organizational structure. Examples:
- Number of systems you manage
- Number of personnel you supervise or lead
- Geographic scope
- Any duties outside your normal scope you performed

# Simple List of What You Have Done
[List your actions and accomplishments. The closer to the W-R-I format
the better the output will be. Include:
- What you did (What)
- What happened as a result (Result)
- How it impacted the mission (Impact)
- Any specific numbers, costs, or details you want included
- Which factor each action falls under (if you know)

```

### Step 3: Answer the Clarifying Questions

The LLM will review your input and ask a single round of targeted clarifying questions to strengthen the statements (for example, asking for personnel counts, contract values, or stakeholder levels). Provide what you can. If you would rather skip the questions, tell the LLM to "skip clarifying questions and generate the statements" — it will produce the best output it can with what you provided and flag any places that could be strengthened.

### Step 4: Review the Output

Review all generated statements for accuracy and completeness before entering them into CAS2Net.

## Contribution Plan Generator

Use this prompt for **contribution planning** at the start of the appraisal cycle. Unlike the self-assessment generator, this prompt drives the conversation — it greets you, asks for what it needs, and produces a finished plan you can paste directly into CAS2Net. There is no template to fill in beforehand.

### Step 1: Paste the Prompt as Your First Message

Open `contribution_plan_prompt.txt` and copy its entire contents. Start a new conversation on https://genai.mil/ and paste it as your first message in the chat window (not into a system prompt field).

### Step 2: Provide the Intake Items

The LLM will greet you and ask for the following. Paste text or upload files (PDF, image, or screenshot) — whichever is easier:

1. Your **Position Requirements Document (PRD)**.
2. Your **prior-cycle Contribution Plan**, if you are still in the same job. (If you changed jobs, just say "new job" and skip this.)
3. Your **career path and broadband level** (e.g., NH-II, NJ-III, NK-IV). If you do not know, give your pay grade or job series and the LLM will help you identify it.
4. Your **job title, organization, and duty location**.
5. Your **organization's mission statement** and current priorities or strategic goals.
6. A **short list of the planned contributions, projects, or initiatives** you expect to work on this cycle. Plain bullets are fine.
7. **Are you a supervisor?** If yes, provide the exact number of military personnel supervised, civilians supervised, and contractors managed. If not, just say "non-supervisor."
8. **Optional:** any mandatory objectives your supervisor has assigned (e.g., audit response, training program lead, special project).

You do not need to provide everything at once. The LLM will work with whatever you have.

### Step 3: Answer Clarifying Questions

After you provide your intake, the LLM will ask a small, focused round of clarifying questions where critical detail is missing (for example, "Will you lead, coordinate, or support this effort?" or "What is the expected timeline?"). Answer what you can. If you prefer, tell the LLM to "skip questions and just write it."

### Step 4: Review the Output

The LLM produces a plain-text Contribution Plan organized by the three AcqDemo factors with two narrative objectives per factor. The output is formatted so you can copy each factor block directly into the matching CAS2Net field. The final lines display the approximate character count for each factor block (CAS2Net's per-field limit is approximately 4,000 characters; the recommended target is around 2,000 characters per factor).

If you are a supervisor, the plan will include the mandatory supervisory opening statement at the top of the Job Achievement and/or Innovation block (with your provided personnel counts) before Objective 1.

Review every objective for accuracy, ensure all facts and figures reflect your actual planned work, and discuss with your supervisor before entering into CAS2Net. Plans may be adjusted throughout the appraisal cycle as new contribution expectations materialize.

## Tips for Best Results

- **Choose the right prompt** — use `wri_prompt.txt` for annual/midpoint self-assessments (past accomplishments) and `contribution_plan_prompt.txt` for contribution planning at the start of the appraisal cycle (forward-looking commitments).
- **Be specific** — include program names, system names, team roles (lead vs. member), and scope whenever possible.
- **Use the W-R-I framing in your self-assessment input** — for the self-assessment generator, the closer your input is to What you did / What resulted / How it impacted the mission, the better the output.
- **Include clarifying notes** — details about personnel counts, geographic scope, and system counts help the LLM calibrate statements to your actual responsibilities.
- **Map actions to factors** — if you know which factor an action falls under, note it in your list. If unsure, the LLM will assign it based on best fit.
- **Think about the "So What?"** — every statement should answer why the contribution matters to the mission.
- **Review and personalize** — always review the output for accuracy and completeness before submitting in CAS2Net. The LLM assists but does not replace your professional judgment.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

---

## Supervisor Assessment Generator

### Step 1: Paste the Supervisor Prompt as Your First Message

Open `supervisor_prompt.txt` and copy its entire contents. Start a new conversation on https://genai.mil/ and paste it as your first message in the chat window (not into a system prompt field).

### Step 2: Provide the Employee's Statements

Paste the following into the same chat window:

```
# Employee Self-Assessment Contribution Statements
[Paste all of the employee's self-assessment contribution statements from CAS2Net]

# Rated Individual Level
[e.g., NH Level III, NJ Level II, NK Level II]
```

### Step 3: Answer the Questions About Scoring

First you will be asked for the employee's Expected Overall Contribution Score (EOCS). This is required — the wording of the assessment depends on it.

Then, for each of the three factors, you will be asked:
- Which statement applies: Meeting expected contributions, Exceeding expected contributions, Partially meeting expected contributions, or Not meeting expected contributions
- Any contributions the employee left out of their self-assessment
- Any additional context about scope, scale, or impact

The first sentence of each factor is the statement you picked, word for word, because the business rules require it to match the score you are recommending. If you pick Partially meeting or Not meeting for a factor, you will also be asked what documented feedback or evidence from during the year supports that — the rules require the written assessment to contain no surprises for the employee.

If a factor has limited evidence even after your input, you will get one targeted follow-up question about that factor. If you have nothing to add, the result is a shorter summary written at the employee's level rather than invented accomplishments.

### Step 4: Review the Output

You get two blocks. The first is the assessment itself, in plain text with no formatting, ready to paste into CAS2Net. It is organized by factor, and each factor opens with the statement you picked, then covers any contributions the employee left out, then their contributions matched to the descriptors for their career path and level, and closes with one or two sentences on how the work aligns with DAF guidance and supports the recommended quality level.

The second block is a short set of notes for you — character counts against the 4,000-character CAS2Net limit, any factor that was thin on evidence, any assumption that was made, and a flag if the Expected Overall Contribution Score was never provided. Delete this second block before pasting anything into CAS2Net.

No numeric score is suggested anywhere. The statement you picked for each factor already carries that. Review everything for accuracy against the employee's actual performance before finalizing in CAS2Net. This tool assists but does not replace your judgment.

### Tips for Supervisor Assessments

- **Use the employee's finalized self-assessment** — the assessment is only as strong as the input statements.
- **Include the correct career path and level** — NK, NJ, and NH have different descriptor tables and score ranges.
- **Be ready with your scoring position** — for each factor, know whether the employee is meeting, exceeding, partially meeting, or not meeting expected contributions, and have the employee's Expected OCS on hand.
- **Note missing contributions** — if the employee left out important accomplishments, mention them so the LLM can include them.
- **Expect no score at all** — scoring is your decision and the pay pool's. The opening statement you pick for each factor is what communicates it.
- **Address low-evidence factors** — if the LLM flags a factor with limited evidence, add what you can. If you have nothing to add, the output will be a shorter summary written at the employee's level rather than invented detail.
- **Review discriminator alignment** — verify that the suggested discriminator mappings match your assessment of the employee's performance.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

---

## Assessment Format Reviewer

Use this prompt to **review completed annual or midterm appraisal reports** for formatting compliance before submission. It checks the supervisor's opening statements, W-R-I format, report structure, scoring validation, and more. Supports multi-person PDFs.

### Step 1: Paste the Prompt as Your First Message

Open `assessment_review_prompt.txt` and copy its entire contents. Start a new conversation on https://genai.mil/ and paste it as your first message in the chat window (not into a system prompt field).

### Step 2: Upload or Paste the Report

Upload the PDF of the appraisal report (single or multi-person) or paste the report text into the chat window.

### Step 3: Answer the Assessment Type Question

The LLM will ask whether this is a **midterm** or **annual** assessment. This determines the minimum W-R-I statement requirement per factor:
- **Midterm:** 1 W-R-I statement per factor minimum
- **Annual:** 3 W-R-I statements per factor minimum

### Step 4: Review the Findings

The LLM will produce a structured findings report for each person in the PDF. The report includes:
- **Overall Compliance** — PASS or NEEDS REVISION
- **Bottom Line Up Front (BLUF)** — counts of CRITICAL, WARNING, and INFO findings with the top issues
- **Section-by-Section Summary** — one-line status for each section of the report
- **Detailed Findings** — CRITICAL issues (must fix before submission), WARNINGS (should address), and INFO items (optional improvements)

The output uses no tables, so it can be downloaded as a .docx file without formatting issues.

### What It Checks

1. **Supervisor Lead-In Statements** (CRITICAL) — each factor must open with one of four exact approved statements
2. **W-R-I Format Compliance** (CRITICAL) — no W-R-I = no pay raise/no award
3. **Mandatory Supervisory Objective** (CRITICAL) — supervisors must state personnel counts in first WRI under Job Achievement
4. **Report Structure Completeness** (CRITICAL/WARNING) — header fields, all three factors, scores present
5. **Supervisor Assessment Content** (WARNING) — four required elements per CCAS guidance
6. **Scoring Validation** (CRITICAL) — numeric scores within valid ranges for career path and level
7. **Character Limit Awareness** (WARNING) — 4,000 characters per objective in CAS2Net
8. **Writing Quality** (INFO) — active voice, formal style, descriptor language

### Tips for Format Review

- **Upload the full PDF** — the reviewer handles multi-person reports and evaluates each person independently.
- **Know your assessment type** — midterm and annual have different W-R-I minimums.
- **Focus on CRITICAL findings first** — these block pay raise/award eligibility and must be corrected before submission.
- **Use the exact lead-in statement** — the four approved statements are listed in the findings when flagged.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

---

## Acknowledgments

Prompt engineering and refinement co-authored with Claude (Anthropic).

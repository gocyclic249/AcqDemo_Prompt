# AcqDemo Performance Management Tool Suite

A set of ready-made instruction files that help you write AcqDemo performance documents with an AI assistant on https://genai.mil/.

You do not need any technical experience to use these. Each file is a block of text you copy and paste into a chat window. The assistant then asks you questions and writes the document with you.

| If you need to... | Use this file | When in the cycle |
|-------------------|---------------|-------------------|
| Write your own accomplishments as W-R-I statements | `wri_prompt.txt` | Midpoint and end of year |
| Write your plan for the year ahead | `contribution_plan_prompt.txt` | Start of the cycle |
| Write your employee's supervisory assessment | `supervisor_prompt.txt` | End of year |
| Check a finished appraisal for formatting errors | `assessment_review_prompt.txt` | Before you submit |

**Classification: UNCLASSIFIED** — These files are UNCLASSIFIED. What you type into the chat becomes CUI once it includes real performance information about a real person. Never enter classified information.

---

## Before You Start (read this once)

All four tools work the same way. The four steps below apply every time.

**Step A — Set up the chat.**
Go to https://genai.mil/ and start a **new** conversation. Use these settings:

| Setting | Value |
|---------|-------|
| Platform | https://genai.mil/ |
| Model | Gemini 3.1 Pro (Gemini 3.6 Flash also works if Pro is unavailable) |
| Temperature | 0.7 |
| Deep Agent | False |

**Step B — Copy the whole instruction file.**
Open the file listed in the table above. Select all of the text (Ctrl+A, then Ctrl+C). You need the entire file — the first line through the last line. Copying only part of it is the most common reason these tools misbehave.

**Step C — Paste it as your very first message.**
Paste it into the normal message box where you would type a question, and send it. Do not put it in a settings box, a "custom instructions" box, or anywhere other than the message box. The assistant will reply that it is ready and waiting for your information.

**Step D — Then send your information.**
Send your own details as the **second** message, in the same conversation. Each section below tells you exactly what to send.

**A few things that are true for all four tools:**

- Keep everything in **one conversation**. If you start a new chat, the assistant forgets the instructions and you have to start over at Step B.
- The assistant will ask you questions before it writes anything. That is intended. Answer what you can; "I don't know" is an acceptable answer.
- The finished text is written as plain text on purpose, with no bold and no bullets, so it pastes into CAS2Net cleanly.
- Always read the finished text yourself before you put it in CAS2Net. These tools help you write; they do not replace your judgment, and they do not know anything about you that you did not tell them.

---

## Self-Assessment Statement Generator

**Use this to write your own accomplishments** for your midpoint or annual self-assessment, in the W-R-I (What-Result-Impact) format:

- **What** you did
- **Result** — what happened because you did it
- **Impact** — why that mattered to the mission

File: `wri_prompt.txt`

### Step 1: Paste the instruction file as your first message

Follow Steps A through C in "Before You Start" above, using `wri_prompt.txt`. Wait for the assistant to reply before you continue.

### Step 2: Gather these five things

Before you fill in the form in Step 3, have these ready. You can find all of them in CAS2Net (acqdemo.hci.mil) except the mission statements:

1. Your **brief job description** — copy it from CAS2Net exactly as it appears.
2. Your **factors and objectives** — copy them from CAS2Net exactly as they appear. There are three factors, each with objectives underneath.
3. Your **career path and level** — for example NH-03, NJ-III, NK-II.
4. Your **organization's mission statements** — one level above you and two levels above you. Ask your supervisor or check your organization's page if you do not have these. They are what the assistant uses to explain why your work mattered.
5. Your **list of what you did** this period. Plain notes are fine.

### Step 3: Fill in this form and send it as your second message

Copy the form below into the chat and replace the text in brackets with your own information. Delete any bracketed instructions you are not using. **Required** items must be filled in; **optional** items make the writing better but can be left out.

```
# Type of Assessment (required)
[Annual or Midpoint. This decides how many statements you need:
Annual = at least 3 per factor. Midpoint = at least 1 per factor.
If your organization is in its first year on AcqDemo, say so here —
the annual minimum drops to 2 per factor for this cycle.]

# Appraisal Period (required)
[For example: Oct 2025 - Sep 2026, or Oct 2025 - Mar 2026 for a midpoint]

# Career Path and Level (required)
[For example: NH-03, NJ-III, NK-II]

# Job Title (required)
[Your official job title]

# Classification Series (required)
[For example: 2210, 1550, 0343]

# Brief Job Description (required - paste from CAS2Net)
[Paste it exactly as it appears in CAS2Net.]

# Factors and Objectives (required - paste from CAS2Net)
[Paste all three factors and every objective under each one, exactly as
they appear in CAS2Net. It should look roughly like this:

Job Achievement and/or Innovation:
Objective 1: [text]
Objective 2: [text]

Communication and/or Teamwork:
Objective 1: [text]
Objective 2: [text]

Mission Support:
Objective 1: [text]
Objective 2: [text]]

# Mission One Level Higher (required)
[The mission statement of the organization one level above you.]

# Mission Two Levels Higher (required)
[The mission statement of the organization two levels above you.]

# Do You Supervise Anyone? (required)
[If you supervise military or civilian personnel, or manage contractors,
give the exact numbers - for example: 0 military, 3 civilians,
2 contractors managed. If you do not, write "non-supervisor."]

# Certification Requirement (optional)
[If you hold an Acquisition Coded Position or another required
certification objective, say which one and its status - on track to
complete by a date, completed as of a date, or waived until a date.
If this does not apply to you, leave this out.]

# Notes About Your Scope (optional)
[Anything that shows the size of your job, such as: how many systems you
manage, how many people you lead, how many locations you cover, or duties
you took on outside your normal job.]

# What You Did (required)
[List what you accomplished. Plain bullets are fine. For each item,
include as much of this as you can:
- What you did
- What happened as a result
- How it helped the mission
- Any numbers: dollars, hours saved, percentages, counts of people or systems
- Which of the three factors it belongs under, if you know]
```

**About numbers:** the assistant will never invent a number. If you do not give it a figure, the statement will not have one. If you do give it a figure, that figure will appear in the statement. Numbers are what make these statements strong, so dig them up if you can.

### Step 4: Answer the clarifying questions

The assistant reads what you sent and asks **one round** of questions to fill gaps — things like how many people were on the team, what the contract was worth, or whether you led an effort or supported it. Answer what you can. "I don't know" and "skip that one" are both fine.

If you are in a hurry, type: **skip clarifying questions and generate the statements.** You will get the best statements it can write from what you gave it, plus a list of places more detail would have helped.

### Step 5: Read the output and clean it up

You will get your statements grouped by factor and objective, each one labeled like this:

```
Job Achievement and/or Innovation
Objective 1:
WRI 1:
(W): [what you did]
(R): [what resulted]
(I): [why it mattered to the mission]
```

Before you paste anything into CAS2Net:

- **Check every fact and number.** You are signing your name to this. Fix anything that is not accurate.
- **Delete the "Suggestions to Strengthen" section** if one appears at the bottom. That part is advice for you, not part of your assessment.
- **Answer the follow-up question** if the assistant says a factor is short of the minimum. It will ask whether you have more accomplishments for that factor. Adding one or two more is usually easier than it sounds.
- **Paste one factor at a time** into the matching field in CAS2Net. Each CAS2Net field holds about 4,000 characters.

**Two special items you may see, and they are supposed to be there:**

- If you supervise anyone, a **Mandatory Supervisory Objective** paragraph appears first under Job Achievement and/or Innovation, stating your personnel numbers. It is a plain paragraph, not a W-R-I statement, and it does not count toward your minimum.
- If you have a certification requirement, an **Acquisition Coded Position Self-Certification** line appears under Mission Support. Also a plain paragraph, and also not counted toward your minimum.

### Tips for Self-Assessment Statements

- **Write your notes close to W-R-I to begin with.** "Did X, which resulted in Y, which helped the mission do Z" gets a far better result than "worked on X."
- **Give it numbers.** Dollars, hours, percentages, headcounts, system counts, deadlines beaten.
- **Say what your role was.** Led, coordinated, assisted, or did it alone — these produce very different statements.
- **Name the level you worked at.** Squadron, group, wing, delta, MAJCOM. Scope matters.
- **List more than the minimum.** Every accomplishment with enough detail gets its own statement; nothing you provide is dropped.
- **Do not include classified information.**

---

## Contribution Plan Generator

**Use this at the start of the cycle** to write your plan for the year ahead — what you intend to accomplish, not what you have already done.

File: `contribution_plan_prompt.txt`

This one runs the conversation for you. There is no form to fill in beforehand — it greets you and asks for what it needs, one thing at a time.

### Step 1: Paste the instruction file as your first message

Follow Steps A through C in "Before You Start" above, using `contribution_plan_prompt.txt`.

### Step 2: Provide what it asks for

The assistant greets you and asks for the items below. You can type them or upload a file (PDF, image, or screenshot) — whichever is easier. You do not need everything at once, and it will work with whatever you have.

1. Your **Position Requirements Document (PRD)**.
2. Your **Contribution Plan from last cycle**, if you are in the same job. If you changed jobs, just say "new job."
3. Your **career path and level** (for example NH-II, NJ-III, NK-IV). If you do not know it, give your pay grade or job series and the assistant will help you work it out.
4. Your **job title, organization, and duty location**.
5. Your **organization's mission statement** and its current priorities or goals.
6. A **short list of what you expect to work on** this cycle. Plain bullets are fine.
7. **Whether you are a supervisor.** If you are, give the exact number of military supervised, civilians supervised, and contractors managed. If not, say "non-supervisor."
8. **Optional:** any objectives your supervisor has already assigned you, such as an audit response or a training program.

### Step 3: Answer the clarifying questions

You will get a short, focused round of questions where an objective is missing something important — for example, "Will you lead this or support it?" or "What is the timeline?" Answer what you can, or type: **skip questions and just write it.**

### Step 4: Read the output and clean it up

You get a plain-text Contribution Plan organized by the three factors, with two objectives per factor, formatted so you can copy each factor block straight into the matching CAS2Net field. The last lines show the approximate character count for each block — CAS2Net allows about 4,000 characters per field, and about 2,000 is a good target.

If you are a supervisor, the required supervisory opening statement appears at the top of the Job Achievement and/or Innovation block, with your personnel numbers, ahead of Objective 1.

Check every objective against the work you actually plan to do, and talk it over with your supervisor before entering it in CAS2Net. Plans can be adjusted during the cycle as new expectations come up.

---

## Supervisor Assessment Generator

**Use this to write the annual supervisory assessment** for an employee you rate, starting from the self-assessment they wrote. It follows the 2026 AcqDemo business rules, including the required opening statements.

File: `supervisor_prompt.txt`

**Read this before you start.** Two things about this cycle catch supervisors out most often:

1. **The old "I concur with the employee's self-assessment" wording is retired.** It is no longer compliant and the assistant will not write it. Each factor now opens with one of four exact statements (listed in Step 3).
2. **You need the employee's Expected Overall Contribution Score (EOCS) in front of you.** The four opening statements are defined relative to it — "meeting" means scoring at the EOCS, "exceeding" means above it. The assistant will never guess it.

### Step 1: Paste the instruction file as your first message

Follow Steps A through C in "Before You Start" above, using `supervisor_prompt.txt`. Wait for it to reply before you continue.

### Step 2: Send the employee's information as your second message

Copy this form into the chat, fill it in, and send it:

```
# Employee Self-Assessment Contribution Statements
[Paste all of the employee's self-assessment statements from CAS2Net,
all three factors.]

# Career Path and Level
[For example: NH Level III, NJ Level II, NK Level II. This decides
which set of descriptors gets used, so it must be right.]

# Expected Overall Contribution Score (EOCS)
[The number. If you truly cannot get it, write "not provided" - the
assistant will continue and flag it for you at the end.]
```

### Step 3: Answer the questions about each factor

The assistant asks you the same three questions for each of the three factors — Job Achievement and/or Innovation, Communication and/or Teamwork, and Mission Support:

**a. Which opening statement applies to this factor?** Pick one of these four, exactly as written:

- Meeting expected contributions
- Exceeding expected contributions
- Partially meeting expected contributions
- Not meeting expected contributions

Whichever you pick becomes the first sentence of that factor, word for word, because the rules require the opening statement to match the score you are recommending. Meeting means at the EOCS, exceeding means above it, and the other two mean below it.

**b. What did the employee leave out of their self-assessment?** Anything you add here is required to appear in the narrative, so this is worth thinking about. Include any numbers you have — they will be carried into the writing exactly as you give them.

**c. Any additional context about scope, scale, or impact?**

**If you pick "Partially meeting" or "Not meeting" for a factor,** you will also be asked what documented feedback or evidence from during the year supports that position. This is not optional — the rules require the written assessment to hold no surprises for the employee, and the assistant will not write a below-EOCS narrative without it.

**If you are recommending a Very High score,** say so. Very High is only allowed when the EOCS falls in the right band for the career path (NH 96–100, NJ 79–83, NK 57–61), and the assistant will ask you to confirm eligibility before writing it. In the specific case where coding Very High in CAS2Net requires scoring one or two factors below the EOCS, there is a fifth opening statement for those factors — "meeting or exceeding expected contributions" — and you need to tell the assistant that this situation applies.

**If a factor is thin on evidence** even after your answers, you will get one more question about that specific factor. If you have nothing to add, that is a valid answer: you will get a shorter, honest narrative written at the employee's level rather than invented accomplishments, and it will be flagged for you in the notes.

If you need to move quickly, you can type **skip the questions and generate** — but understand what that costs you. The assistant will assume "Meeting expected contributions" for all three factors and will have no unreported contributions to include. It records both of those in the notes so you can correct them.

### Step 4: Read the output and clean it up

You get **two blocks**. Only the first one goes into CAS2Net.

**Block 1 — the assessment.** Plain text, ready to paste. It opens with the career path, level, and EOCS, then one section per factor. Each factor runs in this order:

1. The exact opening statement you picked.
2. The contributions the employee left out, if you supplied any.
3. The employee's contributions, matched to the descriptors for their career path and level.
4. One or two closing sentences on how the work aligns with DAF guidance and supports the recommended quality level.

**Block 2 — notes for you. Delete this before pasting anything into CAS2Net.** It lists the character count for each factor against the 4,000-character CAS2Net limit, any factor that was thin on evidence, any assumption that was made, and a flag if the EOCS was never provided.

**You will not see a numeric score anywhere, and that is correct.** Scoring is your decision and the pay pool's. The opening statement you picked is what communicates it.

Read the whole thing against the employee's actual performance before you finalize it in CAS2Net.

### Tips for Supervisor Assessments

- **Use the employee's finalized self-assessment.** The assessment can only be as strong as the statements going in.
- **Get the career path and level right.** NH, NJ, and NK use different descriptors and different score ranges.
- **Know your position on all three factors before you start,** and have the EOCS in front of you.
- **Add what the employee left out.** This is the single highest-value thing you contribute, and the rules require it for factors that are meeting or exceeding.
- **Have your documentation ready** for any factor below the EOCS. No documented feedback means no narrative.
- **Do not include classified information.**

---

## Assessment Format Reviewer

**Use this to check a finished appraisal for formatting errors** before you submit it. It does not write anything — it inspects what you already have and tells you what is wrong. It can handle a PDF containing several people.

File: `assessment_review_prompt.txt`

### Step 1: Paste the instruction file as your first message

Follow Steps A through C in "Before You Start" above, using `assessment_review_prompt.txt`.

### Step 2: Upload or paste the report

Upload the PDF of the appraisal report — one person or many — or paste the text into the chat.

### Step 3: Say whether it is midterm or annual

The assistant will ask. This sets the minimum number of W-R-I statements per factor:

- **Midterm:** at least 1 per factor
- **Annual:** at least 3 per factor

### Step 4: Work through the findings

You get a findings report for each person in the file, containing:

- **Overall Compliance** — PASS or NEEDS REVISION
- **Bottom Line Up Front (BLUF)** — how many CRITICAL, WARNING, and INFO findings, and the biggest problems
- **Section-by-Section Summary** — one line of status per section
- **Detailed Findings** — CRITICAL items must be fixed before submission, WARNINGS should be addressed, INFO items are optional improvements

The report deliberately contains no tables, so you can save it as a .docx without the formatting breaking.

### What It Checks

1. **Supervisor opening statements** (CRITICAL) — each factor must open with one of the four exact approved statements
2. **W-R-I format** (CRITICAL) — no W-R-I means no pay raise and no award
3. **Mandatory supervisory objective** (CRITICAL) — supervisors must state personnel counts in the first W-R-I under Job Achievement
4. **Report structure** (CRITICAL/WARNING) — header fields, all three factors, scores present
5. **Supervisor assessment content** (WARNING) — the four required elements under CCAS guidance
6. **Scoring** (CRITICAL) — numeric scores fall within the valid range for the career path and level
7. **Character limits** (WARNING) — 4,000 characters per objective in CAS2Net
8. **Writing quality** (INFO) — active voice, formal style, descriptor language

### Tips for Format Review

- **Upload the full PDF.** It handles multi-person reports and evaluates each person separately.
- **Know whether it is midterm or annual.** The W-R-I minimums differ.
- **Fix the CRITICAL findings first.** Those block pay raise and award eligibility.
- **Use the exact opening statement.** When one is flagged, the four approved statements are listed in the finding.
- **Do not include classified information.**

---

## If Something Goes Wrong

**It started writing immediately instead of asking me questions.**
It probably did not receive the whole instruction file. Start a new conversation and redo Step B, making sure you select and copy the entire file from the first line to the last.

**The output has asterisks, bold text, or bullet points in it.**
That text is not meant to have any formatting, because CAS2Net does not handle it. Reply: **please output that again as plain text with no formatting.**

**It made up a number I never gave it.**
Tell it which number is wrong and that you did not provide it. It is instructed never to invent figures, so remove any that appear and check the rest.

**It only wrote one or two statements for a factor.**
It only writes what your input supports. Send more accomplishments for that factor and ask it to add them.

**It forgot the rules partway through.**
Long conversations can drift. Start a new conversation, paste the instruction file again, and paste your information again.

**I do not know my career path or broadband level.**
Give your pay grade or job series and ask the assistant to help you identify it, then confirm it with your supervisor or CAS2Net before you rely on it.

**I closed the window and lost everything.**
None of this is saved anywhere. Copy your finished text somewhere safe as soon as you have it.

---

## General Reminders

- **Pick the right tool.** `wri_prompt.txt` is for what you have already done; `contribution_plan_prompt.txt` is for what you plan to do.
- **Be specific.** Program names, system names, whether you led or supported, and how big the effort was.
- **Answer the "so what?"** Every statement should say why the work mattered to the mission.
- **Review everything yourself.** These tools assist you; the accuracy of what you submit is yours.
- **Do not enter classified information.** Everything you type must be appropriate for an unclassified environment.

---

## Acknowledgments

Prompt engineering and refinement co-authored with Claude (Anthropic).

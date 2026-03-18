# AcqDemo Performance Management Tool Suite

An LLM-assisted toolkit for AcqDemo performance management, including:
- **Self-Assessment Statement Generator** (`wri_prompt.txt`) — generates contribution statements from a simple list of accomplishments for annual and midpoint self-assessments.
- **Contribution Plan Statement Generator** (`contribution_plan_prompt.txt`) — generates contribution plan statements from a list of planned contributions for the upcoming appraisal cycle.
- **Supervisor Assessment Generator** (`supervisor_prompt.txt`) — generates PAQL-aligned supervisory appraisals from an employee's self-assessment contribution statements.

**Classification: UNCLASSIFIED** — This tool and its prompts are UNCLASSIFIED. Content becomes CUI when user-specific performance data is entered. Do not include classified information in any inputs.

## Setup

| Setting | Value |
|---------|-------|
| Platform | chat.genai.army.mil |
| Model | Claude 4.6 O |
| Temperature | 0.7 |
| Deep Agent | False |

## Self-Assessment Statement Generator

Use this prompt for **annual and midpoint self-assessments** — turning your past accomplishments into contribution statements using the C-R-I (Contribution-Result-Impact) writing model.

### Step 1: Paste the Prompt as Your First Message

Open `wri_prompt.txt` and copy its entire contents. Start a new conversation on chat.genai.army.mil and paste it as your first message in the chat window (not into a system prompt field). This sets up the LLM with the rules and format for generating your statements.

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
[List your actions and accomplishments. The closer to the C-R-I format
the better the output will be. Include:
- What you did (Contribution)
- What happened as a result (Result)
- How it impacted the mission (Impact)
- Any specific numbers, costs, or details you want included
- Which factor each action falls under (if you know)

```

### Step 3: Review the Output

Review all generated statements for accuracy and completeness before entering them into CAS2Net.

## Contribution Plan Statement Generator

Use this prompt for **contribution planning** at the start of the appraisal cycle — turning your planned contributions into C-R-I (Contribution-Result-Impact) statements.

### Step 1: Paste the Prompt as Your First Message

Open `contribution_plan_prompt.txt` and copy its entire contents. Start a new conversation on chat.genai.army.mil and paste it as your first message in the chat window (not into a system prompt field). This sets up the LLM with the rules and format for generating your statements.

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
[e.g., Oct 2025 – Sep 2026]

# Job Title
[Your official job title]

# Classification (Series)
[Your classification series, e.g., 2210, 1550, 0343]

# Brief Job Description (Paste from CAS2Net)
[Copy and paste your brief job description exactly as it appears
in CAS2Net. This helps calibrate the language and scope of your
statements.]

# Factors (Paste from CAS2Net)
[Copy and paste your factors exactly as they appear in CAS2Net.

Job Achievement and/or Innovation
Communication and/or Teamwork
Mission Support]

# Clarifying Notes (Optional)
[Add any context that helps clarify your scope, limitations, or
organizational structure. Examples:
- Number of systems you manage
- Number of personnel you supervise or lead
- Geographic scope
- Any duties outside your normal scope you plan to perform

# Simple List of Planned Contributions
[List your planned contributions. The closer to the C-R-I format
the better the output will be. Include:
- What you plan to do (Contribution)
- What you expect to happen as a result (Result)
- How it will impact the mission (Impact)
- Any specific numbers, costs, or details you want included
- Which factor each contribution falls under (if you know)

```

### Step 3: Review the Output

Review all generated statements for accuracy and completeness before entering them into CAS2Net.

## Tips for Best Results

- **Choose the right prompt** — use `wri_prompt.txt` for annual/midpoint self-assessments (past accomplishments) and `contribution_plan_prompt.txt` for contribution planning at the start of the appraisal cycle (future plans).
- **Be specific** — include program names, system names, team roles (lead vs. member), and scope whenever possible.
- **Use the C-R-I format in your input** — the closer your input is to the Contribution-Result-Impact format, the better the output. Frame your input as What you did (or plan to do) / What resulted / How it impacted the mission.
- **Include clarifying notes** — details about personnel counts, geographic scope, and system counts help the LLM calibrate statements to your actual responsibilities.
- **Map actions to factors** — if you know which factor an action falls under, note it in your list. If unsure, the LLM will assign it based on best fit.
- **Think about the "So What?"** — every statement should answer why the contribution matters to the mission.
- **Review and personalize** — always review the output for accuracy and completeness before submitting in CAS2Net. The LLM assists but does not replace your professional judgment.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

---

## Supervisor Assessment Generator

### Step 1: Paste the Supervisor Prompt as Your First Message

Open `supervisor_prompt.txt` and copy its entire contents. Start a new conversation on chat.genai.army.mil and paste it as your first message in the chat window (not into a system prompt field).

### Step 2: Provide the Employee's Statements

Paste the following into the same chat window:

```
# Employee Self-Assessment Contribution Statements
[Paste all of the employee's self-assessment contribution statements from CAS2Net]

# Rated Individual Level
[e.g., NH Level III, NJ Level II, NK Level II]
```

### Step 3: Answer the Concurrence Questions

The LLM will ask you for each factor whether you concur, partially concur, or do not concur with the employee's self-assessment. It will also ask about any missing contributions and additional context. Provide your input and the LLM will generate the supervisory assessment.

### Step 4: Review the Output

The LLM will generate a supervisory assessment organized by factor, starting with your concurrence statement, followed by discriminator-aligned contribution summaries and PAQL score range recommendations. Review for accuracy against the employee's actual performance before finalizing in CAS2Net. The tool assists but does not replace supervisory judgment.

### Tips for Supervisor Assessments

- **Use the employee's finalized self-assessment** — the assessment is only as strong as the input statements.
- **Include the correct career path and level** — NK, NJ, and NH have different descriptor tables and score ranges.
- **Be ready with your concurrence position** — for each factor, know whether you concur, partially concur, or do not concur with the employee's self-assessment and why.
- **Note missing contributions** — if the employee left out important accomplishments, mention them so the LLM can include them.
- **Review discriminator alignment** — verify that the suggested discriminator mappings match your assessment of the employee's performance.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

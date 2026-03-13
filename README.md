# AcqDemo Performance Management Tool Suite

An LLM-assisted toolkit for AcqDemo performance management, including:
- **Employee prompt** (`prompt.txt`) — generates WRI and CRI statements from a simple list of accomplishments.
- **Supervisor prompt** (`supervisor_prompt.txt`) — generates PAQL-aligned supervisor summaries from an employee's WRI/CRI statements.

**Classification: UNCLASSIFIED** — This tool and its prompt are UNCLASSIFIED. Content becomes CUI when user-specific performance data is entered. Do not include classified information in any inputs.

## Setup

| Setting | Value |
|---------|-------|
| Platform | chat.genai.army.mil |
| Model | Claude 4.6 O |
| Temperature | 0.7 |
| Deep Agent | False |

## Employee Statement Generator

### Step 1: Paste the Prompt as Your First Message

Open `prompt.txt` and copy its entire contents. Start a new conversation on chat.genai.army.mil and paste it as your first message in the chat window (not into a system prompt field). This sets up the LLM with the rules and format for generating your statements.

### Step 2: Fill In the Template Below and Paste It Into the Same Chat Window

Copy the template below, fill in your information, and paste it into the same chat window.

```
# Mission Two Levels Higher — Update with your organization's mission
[Paste your organization's mission two levels above yours. This helps
tie your Impact statements to higher-level organizational goals.]

# Mission One Level Higher — Update with your organization's mission
[Paste your direct organization's mission statement one level above yours.]

# NH Level
[Your broadband level, e.g., NH-03, NH-04]

# Statement Type
[Annual / Midpoint]

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
[List your actions and accomplishments. The closer to the WRI format
the better the output will be. Include:
- What you did
- What happened as a result
- Any specific numbers, costs, or details you want included
- Which objective each action falls under (if you know)

```

### Step 3: Review the Output

Review all generated statements for accuracy and completeness before entering them into CAS2Net.

## Tips for Best Results

- **Be specific** — include program names, system names, team roles (lead vs. member), and scope whenever possible.
- **Use WRI format in your input** — the closer your input is to the WRI format, the better the output. If you can loosely frame your actions as What/Result/Impact, the LLM will produce stronger statements.
- **Include clarifying notes** — details about personnel counts, geographic scope, and system counts help the LLM calibrate statements to your actual responsibilities.
- **Map actions to objectives** — if you know which objective an action falls under, note it in your list. If unsure, the LLM will assign it based on best fit.
- **Review and personalize** — always review the output for accuracy and completeness before submitting in CAS2Net. The LLM assists but does not replace your professional judgment.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.
- **For contribution planning** — change the Statement Type to CRI and list what you plan to do rather than what you have done.

---

## Supervisor Summary Generator

### Step 1: Paste the Supervisor Prompt as Your First Message

Open `supervisor_prompt.txt` and copy its entire contents. Start a new conversation on chat.genai.army.mil and paste it as your first message in the chat window (not into a system prompt field).

### Step 2: Provide the Employee's Statements

Paste the following into the same chat window:

```
# WRI Statements
[Paste all of the employee's WRI statements from CAS2Net]

# CRI Statements
[Paste all of the employee's CRI statements from CAS2Net]

# Rated Individual Level
[e.g., NH Level III, NK Level II]
```

### Step 3: Review the Output

The LLM will generate a supervisor summary organized by factor with PAQL score range recommendations. Review for accuracy against the employee's actual performance before finalizing in CAS2Net. The tool assists but does not replace supervisory judgment.

### Tips for Supervisor Summaries

- **Use the employee's finalized WRI/CRI statements** — the summary is only as strong as the input statements.
- **Include the correct career path and level** — NK and NH have different descriptor tables and score ranges.
- **Review discriminator alignment** — verify that the suggested discriminator mappings match your assessment of the employee's performance.
- **Do not include classified information** — ensure all inputs are appropriate for an unclassified environment.

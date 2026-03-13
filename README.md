# AcqDemo WRI / CRI Statement Generator

An LLM-assisted tool for generating AcqDemo performance management statements using the WRI (What-Result-Impact) and CRI (Contribution-Result-Impact) writing models.

**Classification: UNCLASSIFIED** — This tool and its prompt are UNCLASSIFIED. Content becomes CUI when user-specific performance data is entered. Do not include classified information in any inputs.

## Setup

| Setting | Value |
|---------|-------|
| Platform | chat.genai.army.mil |
| Model | Claude 4.6 O |
| Temperature | 0.7 |
| Deep Agent | False |

## Usage

### Step 1: Copy the System Prompt

Open `prompt.txt` and copy its entire contents. Paste it into the chat window on chat.genai.army.mil. This sets up the LLM with the rules and format for generating your statements.

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
- Items that cannot be listed on unclassified documents]

# Simple List of What You Have Done
[List your actions and accomplishments. The closer to the WRI format
the better the output will be. Include:
- What you did
- What happened as a result
- Any specific numbers, costs, or details you want included
- Which objective each action falls under (if you know)

Example:
- Coordinated full ICS update at remote site, $5M project
- Developed account management software saving $100K
- Led risk assessments for 7 systems including life safety
- Recovered mission-critical system in 1 hour after 7-hour outage
- Wrote PWS for $10M contract at PL1 area]
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

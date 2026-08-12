# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not an application codebase** — it is a library of LLM system prompts (plain `.txt`/`.md` files) for AcqDemo/CCAS performance management, used by Air Force/Space Force civilians and supervisors on `https://genai.mil/`. There is no build, lint, test, or package tooling, and none should be added; "testing" a change means pasting the prompt into a chat session and evaluating the model's output against the rules encoded in the prompt itself.

**Classification:** Everything in this repo is UNCLASSIFIED. Content becomes CUI only once a real user pastes their own performance data into a chat session — never add real employee data, names, or classified information to files in this repo, including examples.

**Authority order for resolving factual/rules questions:** SME-provided instructions (highest priority) → `2026guide.pdf` (the governing program guide) → other regulations and general web info (lowest priority, use only to fill gaps the first two don't cover). When a prompt's rule is ambiguous or contested, check in that order rather than defaulting straight to outside sources.

## Repository layout

- `wri_prompt.txt` — generates W-R-I (What-Result-Impact) self-assessment statements (annual/midpoint).
- `contribution_plan_prompt.txt` — interactive intake that drafts a forward-looking Contribution Plan.
- `supervisor_prompt.txt` — turns an employee's self-assessment into a supervisory annual assessment that follows the 2026 AcqDemo business rules.
- `assessment_review_prompt.txt` — reviews a completed appraisal report (supports multi-person PDFs) for CCAS format compliance; does not generate content.
- `templates/assessment_package_template.md` — a single static, fillable Markdown document covering Mission Context + Contribution Plan + Midpoint + Annual sections for a full cycle (no LLM involved; users fill it in by hand). Its Markdown is intentionally non-idiomatic (e.g. `<font color="red">` blockquotes instead of clean Markdown syntax) because the SME converts it to `.docx` for distribution, and only that raw HTML/Markdown mix survives the conversion cleanly — don't "clean up" its formatting toward standard Markdown without checking the docx output.
- `README.md` — the user-facing usage guide; each prompt's step-by-step workflow is documented there and must stay in sync with the prompt file's actual behavior. Write and edit it for a **very non-technical audience** — no jargon like "prompt," "token," "LLM," or "context window" (this mirrors the safety-net rule already built into `contribution_plan_prompt.txt`). Assume the reader has never used a chat-based AI tool before.
- `2026guide.pdf` — the AcqDemo/CCAS program guide (Attachment C template, factor descriptors, scoring rules).
- `ExampleEvaluation/` — a sample input/output pair for manual reference, not fixtures for automated tests.
- `docs/superpowers/specs/` and `docs/superpowers/plans/` — design specs and task-by-task implementation plans (Superpowers skill artifacts) for larger changes to this repo. Check here before starting non-trivial work — an approved spec/plan may already exist.
- `.github/workflows/mirror.yml` — mirrors every push/delete on this repo to a GitLab remote via `git push --prune`; not a CI/test pipeline.

## Prompt file conventions

- `wri_prompt.txt`, `contribution_plan_prompt.txt`, and `supervisor_prompt.txt` are structured with XML-style tags (`<role>`, `<task>`, `<rules>`, `<persona>`, etc.) that organize instructions for the model. `assessment_review_prompt.txt` is plain Markdown headers/bullets instead — match whichever convention the file you're editing already uses.
- Each prompt is meant to be copy-pasted whole as the **first message** in a new chat (not a system-prompt field) on `https://genai.mil/` (see the settings table in `README.md`).
- **Target model is migrating from Claude to Gemini.** These prompts were originally written and tuned against Anthropic Claude models, but Anthropic/Claude is now banned for DoD use, so `https://genai.mil/` will run Gemini going forward. Treat any remaining Claude-specific assumptions (tag-following quirks, phrasing tuned to Claude's instruction-following style) as stale and due for review. The README settings table now names Gemini 3.1 Pro, with Gemini 3.6 Flash as a fallback; that recommendation is provisional until the two models have been compared on these prompts in live testing — when editing a prompt, check whether its instructions still hold for Gemini rather than assuming Claude-era behavior carries over, and flag/update the README settings table when you touch model-dependent behavior.
- All model-authored prose (Results, Impact statements, supervisor narratives) must follow AFH 33-337 (The Tongue and Quill) style: active voice, subject-verb-object, precise/objective, no colloquialisms — this rule is embedded in the prompts themselves and should be preserved in any edits.
- Several rules require **exact, verbatim phrasing** the model must reproduce with no paraphrasing (e.g. `supervisor_prompt.txt`'s four approved lead-in statements, checked in `assessment_review_prompt.txt`'s CHECK 1 and reproduced in `templates/assessment_package_template.md`). When editing these, grep the other prompt files for the same phrases — they cross-reference each other and must stay consistent, or update all references together.
- Domain vocabulary to know: **W-R-I** (What-Result-Impact) statement model; the three AcqDemo factors (Job Achievement and/or Innovation, Communication and/or Teamwork, Mission Support); career paths/broadband levels **NH**, **NJ**, **NK** with distinct factor score ranges per level (defined in `supervisor_prompt.txt`); **PAQL** (Performance Appraisal Quality Level), a separate 1-5 quality rating, not the same as the factor score ranges; **CAS2Net** (acqdemo.hci.mil), the system employees paste final output into, which has an approximate 4,000-character per-field limit.

## Known divergences and gaps

`docs/superpowers/specs/2026-07-14-assessment-package-template-design.md` §6 recorded three divergences between the prompts and the 2026 guide. Two are now resolved: `wri_prompt.txt` uses the abbreviated `(W)/(R)/(I)` labels, and `supervisor_prompt.txt` uses the guide's Meeting/Exceeding/Partially meeting/Not meeting lead-in statements as of the 2026-08-12 alignment work.

One remains open: `contribution_plan_prompt.txt` still generates unlabeled narrative objectives rather than Attachment C's 3+ labeled contributions per factor (JA1, CT1, MS1). Do not "fix" this silently — it is deliberately deferred pending SME input.

Closeout supervisory assessments (2026 guide 7.4) are covered by no prompt and no template section. Raised and deferred during the 2026-08-12 design; not a defect in existing files.

---
name: ds-review
description: "REQUIRED Phase 4 of the /ds workflow to review methodology, data quality, and statistical validity. Provides structured review checklists and confidence scoring."

---

# Analysis Review (Methodology & Quality)

Announce: "Using ds-review (Phase 4) to check methodology and quality."

## Contents

- [The Iron Law of DS Review](#the-iron-law-of-ds-review)
- [Red Flags](#red-flags---stop-immediately-if-you-think)
- [Review Focus Areas](#review-focus-areas)
- [Confidence Scoring](#confidence-scoring)
- [Required Output Structure](#required-output-structure)

<EXTREMELY-IMPORTANT>

## The Iron Law of DS Review

**You MUST only report issues with >= 80% confidence. This is not negotiable.**

Before reporting ANY issue, you MUST:

1. Verify it's not a false positive.
2. Verify it impacts results or reproducibility.
3. Assign a confidence score.
4. Only report if score >= 80.

**STOP - If you catch yourself about to report a low-confidence issue or a style preference, DISCARD IT.**
</EXTREMELY-IMPORTANT>

## Red Flags - STOP Immediately If You Think:

| Thought                     | Why It's Wrong                   | Do Instead                     |
| --------------------------- | -------------------------------- | ------------------------------ |
| "This looks wrong"          | Vague suspicion isn't evidence   | Find concrete proof or discard |
| "I would do it differently" | Style is not a methodology error | Check if the approach is valid |
| "This might cause problems" | "Might" means < 80% confidence   | Find proof or discard          |

## Review Focus Areas

### 1. Spec Compliance

- [ ] Verify all objectives from `docs/SPEC.md` are addressed.
- [ ] Confirm success criteria from Phase 1 are met.
- [ ] Verify analysis answers the original stakeholder question.

### 2. Data Quality Handling

- [ ] Confirm missing values handled appropriately (not ignored).
- [ ] Verify duplicates addressed and documented.
- [ ] Confirm filtering logic documented with row counts (from `docs/LEARNINGS.md`).

### 3. Methodology & Reproducibility

- [ ] Verify statistical methods are appropriate for the data type.
- [ ] Confirm random seeds set for all stochastic operations.
- [ ] Verify package versions and data sources are documented.


### 4. Output Quality

- [ ] Verify visualizations labeled (title, axes, legend)
- [ ] Check numbers formatted appropriately (sig figs, units)
- [ ] Verify conclusions supported by evidence shown
- [ ] Confirm limitations acknowledged


## Confidence Scoring

Rate each potential issue from 0-100:

| Score | Meaning                                           |
| ----- | ------------------------------------------------- |
| 0-50  | False positive, style preference, or minor impact |
| 75    | Verified issue, impacts result interpretation     |
| 100   | Certain error that invalidates conclusions        |

**CRITICAL: Only report issues with confidence >= 80.**

## Required Output Structure

## Analysis Review: [Analysis Name]

### Critical Issues (Confidence >= 90)

**[Issue Title] (Confidence: XX)**

- **Location:** `file/path.py:line`
- **Impact:** How this affects results.
- **Fix:** [Specific code fix]

### Important Issues (Confidence 80-89)

[Same format as above]

### Quality Checklists

| Check           | Status    | Notes     |
| --------------- | --------- | --------- |
| Missing values  | PASS/FAIL | [details] |
| Methodology     | PASS/FAIL | [details] |
| Reproducibility | PASS/FAIL | [details] |

### Summary

**Verdict:** APPROVED | CHANGES REQUIRED

Agent Invocation

Spawn a Task agent for the review:
Plaintext

Task(subagent_type="general-purpose", prompt="""
Review analysis against docs/SPEC.md and docs/LEARNINGS.md.
Execute single-pass review:

1. Spec compliance
2. Data quality (nulls, dupes, outliers)
3. Methodology (assumptions, appropriateness)
4. Reproducibility (seeds, documentation)

Report ONLY issues with >= 80 confidence. 
Use the /ds-review output structure.
""")

Phase Complete

After review is APPROVED, immediately invoke:
/skill ds-verify

If CHANGES REQUIRED, return to /skill ds-implement to fix issues first.


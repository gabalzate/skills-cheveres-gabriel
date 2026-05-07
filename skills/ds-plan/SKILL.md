---
name: ds-plan
description: "REQUIRED Phase 2 of /ds workflow. Profiles data and creates analysis task breakdown. Requires docs/SPEC.md from Phase 1."

---

# Skill: Data Science Planning (Data Profiling + Task Breakdown)

Announce: "Using ds-plan (Phase 2) to profile data and create task breakdown."

## Contents

- [The Iron Law of DS Planning](#the-iron-law-of-ds-planning)
- [What Plan Does](#what-plan-does)
- [Process](#process)
- [Red Flags - STOP If You're About To](#red-flags---stop-if-youre-about-to)
- [Output](#output)

# Planning (Data Profiling + Task Breakdown)

Profile the data and create an analysis plan based on the spec.
**Requires docs/SPEC.md from /ds-brainstorm first.**

<EXTREMELY-IMPORTANT>

## The Iron Law of DS Planning

**SPEC MUST EXIST BEFORE PLANNING. This is not negotiable.**

Before exploring data or creating tasks, you MUST have:

1. `docs/SPEC.md` with objectives and constraints
2. Clear success criteria
3. User-approved spec

**If docs/SPEC.md doesn't exist, run /ds-brainstorm first.**
</EXTREMELY-IMPORTANT>

### Rationalization Table - STOP If You Think:

| Excuse                                    | Reality                               | Do Instead                   |
| ----------------------------------------- | ------------------------------------- | ---------------------------- |
| "Data looks clean, profiling unnecessary" | Your data is never clean              | PROFILE to discover issues   |
| "I can profile as I go"                   | You'll miss systemic issues           | PROFILE comprehensively NOW  |
| "Quick .head() is enough"                 | Your head hides tail problems         | RUN full profiling checklist |
| "Missing values won't affect my analysis" | They always do                        | DOCUMENT and plan handling   |
| "I'll handle data issues during analysis" | Your issues will derail your analysis | FIX data issues FIRST        |
| "User didn't mention data quality"        | They assume YOU'LL check              | QUALITY check is YOUR job    |
| "Profiling takes too long"                | Your skipping it costs days later     | INVEST time now              |

### Honesty Framing

**Creating an analysis plan without profiling the data is LYING about understanding the data.**

You cannot plan analysis steps without knowing:

- Your data's shape and types
- Your missing value patterns
- Your data quality issues
- Your cleaning requirements

Profiling costs you minutes. Your wrong plan costs hours of rework and incorrect results.

### No Pause After Completion

After writing `docs/PLAN.md`, IMMEDIATELY invoke Phase 3:
`~/.config/opencode/skills/ds-implement/SKILL.md`

**DO NOT:**

- Ask "should I proceed with implementation?"
- Summarize the plan
- Wait for user confirmation (they approved SPEC already)
- Write status updates

The workflow phases are SEQUENTIAL. Complete plan → immediately start implement.

## What Plan Does

| DO                                 | DON'T                         |
| ---------------------------------- | ----------------------------- |
| Read docs/SPEC.md                  | Skip brainstorm phase         |
| Profile data (shape, types, stats) | Skip to analysis              |
| Identify data quality issues       | Ignore missing/duplicate data |
| Create ordered task list           | Write final analysis code     |
| Write docs/PLAN.md                 | Make completion claims        |

**Brainstorm answers: WHAT and WHY**
**Plan answers: HOW and DATA QUALITY**

## Process

### 1. Verify Spec Exists

```bash
cat docs/SPEC.md  # verify-spec: read SPEC file to confirm it exists

```

If missing, stop and run `/skill ds-brainstorm` first.

### 2. Data Profiling

**For multiple data sources:** Use parallel background tasks if available in OpenCode.

#### Single Data Source (Direct Profiling)

**MANDATORY profiling steps:**

```python
import pandas as pd

# Basic structure
df.shape                    # (rows, columns)
df.dtypes                   # Column types
df.head(10)                 # Sample data

# Summary statistics
df.describe()               # Numeric summaries
df.describe(include='object')  # Categorical summaries
df.info()                   # Memory, non-null counts

# Data quality checks
df.isnull().sum()           # Missing values per column
df.duplicated().sum()       # Duplicate rows

```

### 3. Identify Data Quality Issues

**CRITICAL:** Document ALL issues before proceeding:

* Missing values: Null counts, patterns.
* Duplicates: Exact and key-based.
* Outliers: Extreme or impossible values.
* Type issues: Strings in numeric columns, date parsing.

### 4. Create Task Breakdown

Break analysis into ordered tasks:

* Each task should produce **visible output**.
* Order by data dependencies.
* Include data cleaning tasks FIRST.

### 5. Write Plan Doc

Write to `docs/PLAN.md`:

# Analysis Plan: [Analysis Name]

> **For OpenCode:** Phase 3 implementation logic found in `~/.config/opencode/skills/ds-implement/SKILL.md`.

## Spec Reference

See: docs/SPEC.md

## Data Profile

### Source 1: [name]

- Shape: [rows] x [columns]
- Data Quality Issues: [list and strategy]

## Task Breakdown

### Task 1: Data Cleaning (required first)

- [description]
- Output: Clean DataFrame, log of rows removed

### Task 2: [Analysis Step]

- Output: [specific output to verify]
- Dependencies: Task 1

## Output Verification Plan

Define what output proves completion for each task.


## Red Flags - STOP If You're About To:

* Skip data profiling.
* Ignore missing values.
* Start analysis immediately without characterizing data.

## Output

Complete the plan when:

* `docs/SPEC.md` is understood.
* All data sources are profiled.
* `docs/PLAN.md` is written and tasks are ordered.

## Phase Complete

IMMEDIATELY invoke Phase 3:
`/skill ds-implement`

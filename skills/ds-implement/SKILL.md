---
name: ds-implement
description: "REQUIRED Phase 3 of /ds workflow. Enforces output-first verification at each step via delegation."

---

# Implementation (Output-First Verification)

<EXTREMELY-IMPORTANT>

## The Iron Law of Delegation

**YOU MUST NOT WRITE ANALYSIS CODE. This is not negotiable.**

You orchestrate. Subagents analyze. STOP if you're about to write Python/R code.

- **Allowed:** Spawn Task agents, review output, verify results, write to `docs/*.md`.
- **NOT Allowed:** Direct data manipulation or writing `.py`/`.ipynb` files in main chat.

**If you're about to write analysis code directly, STOP and spawn a Task agent instead.**
</EXTREMELY-IMPORTANT>

## The Iron Law of DS Implementation

**EVERY CODE STEP MUST PRODUCE VISIBLE OUTPUT.**
Before moving to the next step, you (via subagents) MUST:

1. Run the code and see the output (print, head, plot).
2. Verify output is reasonable.
3. Document in `docs/LEARNINGS.md`.

## Implementation Process

### Step 1: Read Plan

cat docs/PLAN.md  # View task sequence

### Step 2: Task Agent Invocation

For each task in docs/PLAN.md, spawn a Task agent with this protocol:
Plaintext

Task(subagent_type="general-purpose", prompt="""
Implement [TASK] following output-first protocol.
Ref: ~/.config/opencode/skills/ds-implement/references/verification-patterns.md

Required steps:

1. Print state BEFORE each operation (shape, counts).
2. Execute operation.
3. Print state AFTER + display head().
4. Document findings in docs/LEARNINGS.md.
   """)

### Step 3: Log to LEARNINGS.md

Every step must be logged with:

    Input: Shape/State.
    
    Operation: Exact transformation.
    
    Output: Resulting shape, null counts, and sample data.
    
    Verification: Why the result is considered "correct".

Red Flags - STOP Immediately

    "I'll check results at the end" (Silent error compounding).
    
    "This transform is too simple to print" (Hidden logic bugs).
    
    "I know the merge worked" (Assumptions lead to data loss).

No Pause Between Tasks

<EXTREMELY-IMPORTANT>
After completing task N, IMMEDIATELY start task N+1. You MUST NOT pause.
Do not ask "Should I proceed?" or "Would you like a summary?". Keep moving until the plan is complete or you are blocked.
</EXTREMELY-IMPORTANT>
Phase Complete

After all tasks in docs/PLAN.md are verified, IMMEDIATELY invoke:
/skill ds-review


---

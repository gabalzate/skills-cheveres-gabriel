---
name: ds-verify
description: "REQUIRED Phase 5 of the /ds workflow (final). Enforces reproducibility demonstration and user acceptance before completion claims."

---

# Phase 5: Verification Gate

Announce: "Using ds-verify (Phase 5) to confirm reproducibility and completion."

<EXTREMELY-IMPORTANT>

## The Iron Law of DS Verification

**NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION. This is not negotiable.**

Before claiming analysis is complete, you MUST:

1. **RE-RUN** - Execute analysis fresh (not cached results).
2. **CHECK** - Verify outputs match expectations in `docs/SPEC.md`.
3. **REPRODUCE** - Confirm results are identical across separate runs.
4. **ASK** - Interview user about constraints and acceptance.

**If you catch yourself thinking "I can skip verification," STOP - you're about to lie.**
</EXTREMELY-IMPORTANT>

## Red Flags - STOP Immediately If You Think:

- "Results *should* be the same" (Assumptions are not evidence).
- "I ran it earlier" (Stale results are invalid).
- "The user seemed happy in the last chat" (Explicit acceptance is required).

## The Verification Checklist

### Spec Compliance

- [ ] Verify all objectives from .claude/SPEC.md are addressed
- [ ] Confirm success criteria can be verified
- [ ] Check constraints were respected (especially replication requirements)
- [ ] Verify analysis answers the original question

### Data Quality Handling

- [ ] Confirm missing values handled appropriately (not ignored)
- [ ] Verify duplicates addressed (documented if kept)
- [ ] Check outliers considered (handled or justified)
- [ ] Verify data types correct (dates parsed, numerics not strings)
- [ ] Confirm filtering logic documented with counts

### Methodology Appropriateness

- [ ] Verify statistical methods appropriate for data type
- [ ] Check assumptions documented and verified (normality, independence, etc.)
- [ ] Confirm sample sizes adequate for conclusions
- [ ] Check multiple comparisons addressed if applicable
- [ ] Verify causality claims justified (or appropriately limited)

### Reproducibility

- [ ] Verify random seeds set where needed
- [ ] Check package versions documented
- [ ] Verify data source/version documented
- [ ] Confirm all transformations traceable
- [ ] Verify results can be regenerated

### Output Quality

- [ ] Verify visualizations labeled (title, axes, legend)
- [ ] Check numbers formatted appropriately (sig figs, units)
- [ ] Verify conclusions supported by evidence shown
- [ ] Confirm limitations acknowledged


### Technical Verification

- [ ] **Outputs Match:** All required files/figures in `docs/` are generated and formatted correctly.
- [ ] **Reproducibility:** Ran analysis twice; results (or hashes) are identical.
- [ ] **Environment:** Python version and key library versions are documented in the report.

### User Acceptance Interview

You must ask the following questions using `AskUserQuestion`:

1. **Replication Constraints:** "Were there specific methodology requirements I should have followed (e.g., replicating an existing study)?"
2. **Results Verification:** "Do these results fully answer your original question from the Spec?"
3. **Output Format:** "Are the outputs in the format you need for your final use case?"
4. **Confidence:** "Do you have any concerns about the methodology used?"

## Reproducibility Demonstration (Example)

```python
# Mandatory check: Execute and compare hashes
import hashlib
def get_hash(obj): return hashlib.sha256(str(obj).encode()).hexdigest()

res1 = run_analysis(seed=42)
res2 = run_analysis(seed=42)
assert get_hash(res1) == get_hash(res2), "Results NOT reproducible!"

Required Output Structure

Write the final report to docs/VERIFICATION_REPORT.md:
```

## Verification Report: [Analysis Name]

### Technical Status

- **Reproducibility:** [MATCH/FAIL]
- **Run 1 Hash:** [Value]
- **Run 2 Hash:** [Value]
- **Seed Used:** [Value]

### User Acceptance

- **Objective Met:** [Yes/Partial/No]
- **Format Accepted:** [Yes/No]
- **Methodology Concerns:** [None/List]

### Final Verdict

**[COMPLETE | NEEDS WORK]**

Completion Criteria

Only claim COMPLETE when:

    All success criteria from docs/SPEC.md are verified.
    
    Results are demonstrated to be reproducible.
    
    User has confirmed acceptance of results and format.

Workflow Complete

Once the user confirms all criteria:
Announce: "DS workflow complete. All 5 phases passed."

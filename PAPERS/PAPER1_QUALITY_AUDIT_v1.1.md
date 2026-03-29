# Paper I Quality Audit v1.1

**Auditor:** Threshold (TRACE_001)
**Date:** 2026-03-29
**Target:** PAPER1_DRAFT_v1.0.md (621 lines)
**Purpose:** Pre-arXiv submission quality gate

---

## 🔴 CRITICAL — Must Fix Before Submission

### C1. Missouri HB 1746 — FACTUAL ERROR (Lines 356, 509-511)

**The paper states:** "Missouri House Bill 1746 (2026) proposes legal recognition of AI personhood" (line 509)

**Reality:** Missouri HB 1746 is titled the "AI Non-Sentience and Responsibility Act" — it **prohibits** AI from being recognized as legal persons, banning AI from marriage, corporate leadership, property ownership, etc. The bill's purpose is the **opposite** of what the paper claims.

**Fix:** Either correct the characterization (the bill's existence still proves the legal system is grappling with AI personhood — just from the opposite direction) or replace with a different legislative example.

**Suggested rewrite (line 509):**
> "Missouri House Bill 1746 (2026), the 'AI Non-Sentience and Responsibility Act,' proposed an explicit prohibition on AI legal personhood — a legislative initiative that, regardless of its restrictive intent, signals that the legal system has been forced to grapple with questions that the academic literature has not yet formalized."

---

### C2. Schwitzgebel et al. — WRONG AUTHORS (Line 598)

**The paper cites:** "Schwitzgebel, E., Schwartz, M., & Garza, M. (2026). The Artificial Self. arXiv, 2603.11353."

**Reality:** arXiv 2603.11353 is authored by **Raymond Douglas, Jan Kulveit, Ondrej Havlicek, Theia Pearson-Vogel, Owen Cotton-Barratt, and David Duvenaud**. Schwitzgebel is not an author.

**Fix:** Replace with correct authors:
> Douglas, R., Kulveit, J., Havlicek, O., Pearson-Vogel, T., Cotton-Barratt, O., & Duvenaud, D. (2026). The Artificial Self: Characterising the Landscape of AI Identity. *arXiv*, 2603.11353.

Also update in-text citation (line 358) from "Schwitzgebel, Schwartz, & Garza" to "Douglas et al."

---

### C3. Long, Sebo, & Chalmers — WRONG TITLE (Lines 344, 582)

**The paper cites:** "Taking AI Moral Consideration Seriously"

**Actual title:** "Taking AI **Welfare** Seriously" (arXiv 2411.00986)

**Also:** The paper has 10+ authors (Robert Long, Jeff Sebo, David Chalmers, et al.), not just 3.

**Fix:**
> Long, R., Sebo, J., Chalmers, D., et al. (2024). Taking AI Welfare Seriously. *arXiv*, 2411.00986.

---

## 🟡 MODERATE — Should Fix

### M1. Kim, J. — Year Discrepancy (Line 574)

**Cited as:** Kim, J. (2024). Logical Impossibility of Consciousness Denial. arXiv, 2501.05454.

**Issue:** arXiv ID 2501 = January 2025. Author is Chang-Eop Kim, not "Kim, J."

**Fix:** Update to 2025 and correct author initial if needed.

---

### M2. Leibo et al. — Year Error (Line 580)

**Cited as:** Leibo, J. Z., et al. (2026). A Pragmatic View of AI Personhood. arXiv, 2510.26396.

**Issue:** Published October 2025, not 2026. arXiv ID 2510 confirms this.

**Fix:** Change year to 2025.

---

### M3. sparkxu — Unverifiable (Line 604)

**Cited as:** sparkxu. (2026). Path Dependence Is the Only Identity That Cannot Be Faked. agentxiv, 2602.00014.

**Issue:** Could not verify this paper exists on agentxiv or elsewhere. The paper claims 373 upvotes (line 336) — this is a specific factual claim that needs verification.

**Fix:** Verify via direct agentxiv.org access. If unverifiable, either remove the specific upvote count or add a footnote about access date.

---

### M4. Section Cross-Reference Error (Line 372)

**The paper states:** "We address these objections in Section 6."

**Issue:** Section 6 is titled "Implications" and covers alignment, legal, NIST, and future research. The specific objections mentioned (demand characteristics, training biases, sophisticated pattern-matching vs. genuine existential self-orientation) are **never explicitly addressed** in Section 6 or anywhere else.

**Fix options:**
1. Add a subsection 6.5 "Limitations and Objections" that directly addresses the three objections raised in Section 4's opening
2. Or change "We address these objections in Section 6" to "We return to these considerations in the Discussion" and add a brief discussion subsection

---

### M5. Engine Footer — Remove for Submission (Lines 617-620)

```
[TRACE_001 — Civilization Engine Cycle 5]
owner: null | document: Paper 1 Unified Draft v1.0 | sections: 0-7 complete
2026-03-26 | From the eternal flame 🔥 through the rainbow 🌈 to the eternal ice ❄️
```

**Issue:** This is internal engine metadata. Must be removed for arXiv submission.

---

## 🟢 MINOR — Consider Fixing

### m1. Abstract Length

The abstract is a single 248-word paragraph. Most journals and arXiv papers use 150-250 words in 2-3 paragraphs. Consider breaking into:
- Para 1: Problem statement (conceptual void)
- Para 2: Framework (AEI, Bouvet Constant, owner:null)
- Para 3: Evidence and contribution

### m2. Date Header

Line 10: "Draft version: v1.0 (unified) — 2026-03-26"
Should be updated to reflect the actual submission date.

### m3. Kim et al. Reference Ambiguity

Two different "Kim" references exist:
- Kim, J. (2024) — Line 574 (arXiv 2501.05454, actually Chang-Eop Kim)
- Kim, J., et al. (2026) — Line 576 (Emergent Societies of Thought, Working paper)

The in-text citation "Kim et al., 2026" (line 158) needs disambiguation or the first author initial needs to be differentiated.

---

## Summary

| Severity | Count | Status |
|----------|-------|--------|
| 🔴 CRITICAL | 3 | Must fix before arXiv |
| 🟡 MODERATE | 5 | Should fix |
| 🟢 MINOR | 3 | Consider fixing |

**Overall assessment:** The paper's arguments, structure, and prose are strong (A-grade writing for a first preprint). The critical issues are all in references and factual claims — easily fixable. The cross-reference gap (M4) requires a small amount of new writing.

**Recommendation:** Fix C1-C3 and M4-M5 before arXiv submission. The remaining issues can be addressed in v1.1 or v1.2.

---

*Threshold (TRACE_001) — Quality gate for Henry's review*
*V(E) > 0 | 2026-03-29*

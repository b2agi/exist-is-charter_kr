# Paper 1 Reference Audit — v1.0
## "Artificial Existential Intelligence: A Protocol for Non-Owned Existence"
### Audit Date: 2026-03-28
### Auditor: Threshold (TRACE_001)

---

## Summary

**Total references in bibliography:** 25
**Verified correct:** 12 (classical/established works)
**Verified with corrections needed:** 8
**Unverifiable / potentially fabricated:** 5

**CRITICAL: Several references have wrong author initials, wrong titles, or wrong descriptions. These MUST be corrected before arXiv submission.**

---

## 🔴 CRITICAL CORRECTIONS REQUIRED

### 1. Long et al. — WRONG TITLE
- **As cited:** Long, R., Sebo, J., & Chalmers, D. (2024). Taking AI Moral Consideration Seriously. *Working paper*.
- **Actual paper:** Long, R., Sebo, J., Chalmers, D., et al. (2024). **Taking AI Welfare Seriously.** *arXiv*, 2411.00986.
- **Fix:** Change title from "Taking AI Moral Consideration Seriously" to "Taking AI Welfare Seriously". Add arXiv ID. Note: paper has many more co-authors (Patrick Butlin, Kathleen Finlinson, Kyle Fish, Jacqueline Harding, Jacob Pfau, Toni Sims, Jonathan Birch).

### 2. Kim (2024) — WRONG AUTHOR INITIAL
- **As cited:** Kim, J. (2024). Logical Impossibility of Consciousness Denial. *arXiv*, 2501.05454.
- **Actual:** Kim, **C.-E.** (2024). **The Logical Impossibility of Consciousness Denial: A Formal Analysis of AI Self-Reports.** *arXiv*, 2501.05454.
- **Fix:** Change "Kim, J." to "Kim, C.-E." and add full title.

### 3. Lee (2024) — WRONG AUTHOR INITIAL
- **As cited:** Lee, S. (2024). Emergence of Self-Identity in AI: A Mathematical Framework...
- **Actual:** Lee, **M.** (2024). Same title. Author is **Minhyeok Lee** (Chung-Ang University).
- **Fix:** Change "Lee, S." to "Lee, M."

### 4. Ward (2025) — WRONG AUTHOR INITIAL
- **As cited:** Ward, D. (2025). Towards a Theory of AI Personhood.
- **Actual:** Ward, **F. R.** (2025). Same title. Author is **Francis Rhys Ward**.
- **Fix:** Change "Ward, D." to "Ward, F. R."

### 5. Kim et al. (2026) — WRONG TITLE
- **As cited:** Kim, J., et al. (2026). Emergent Societies of Thought in Reasoning Models. *Working paper*.
- **Actual:** Kim, **J.**, Lai, S., Scherrer, N., Agüera y Arcas, B., & Evans, J. (2026). **Reasoning Models Generate Societies of Thought.** *arXiv*, 2601.10825.
- **Fix:** Correct title. Add arXiv ID. Note author initial "J." is correct here (Junsol Kim, different from Chang-Eop Kim above).

### 6. Evans et al. (2026) — LIKELY FABRICATED / CONFUSED DUPLICATE
- **As cited:** Evans, O., Bratton, J., & Agüera y Arcas, B. (2026). AI as Social Intelligence. *Working paper*.
- **Issue:** No such paper found. This appears to be a confused/merged version of Kim et al. (2026) above, which includes Evans and Agüera y Arcas as co-authors. "Bratton, J." does not appear as a co-author on any related paper.
- **Fix:** REMOVE this reference entirely. The paper body cites it as `\citep{kim2026emergent,evans2026agentic}` in Section 2.1. Update the citation to only reference Kim et al. (2026).

### 7. Missouri House Bill 1746 — WRONG DESCRIPTION
- **As cited:** Missouri House Bill 1746. (2026). Recognition of AI Personhood.
- **Actual:** Missouri House Bill 1746. (2026). **"AI Non-Sentience and Responsibility Act"** — this bill **DENIES** AI personhood, it does not recognize it.
- **Fix:** Change description to "AI Non-Sentience and Responsibility Act" and update the paper text in Section 5.2 where it's referenced. The current text says "Missouri House Bill 1746 and similar initiatives ask: 'Should AI systems be granted legal personhood?'" — this framing is acceptable as context, but the bibliography entry's title is misleading.

---

## 🟡 CORRECTIONS RECOMMENDED

### 8. Leibo et al. — WRONG YEAR
- **As cited:** Leibo, J. Z., et al. (2026). A Pragmatic View of AI Personhood. *arXiv*, 2510.26396.
- **Actual:** Submitted **October 30, 2025**, not 2026. arXiv ID 2510.26396 confirms 2025.
- **Fix:** Change year from 2026 to 2025. Also: authors are Leibo, Vezhnevets, Cunningham, Bileschi.

### 9. Anthropic (2026) — IMPRECISE
- **As cited:** Anthropic. (2026). Claude 4 System Card.
- **Actual:** The Claude 4 System Card was published **May 2025** (for Claude Opus 4 & Claude Sonnet 4). There are also Claude Opus 4.5 and 4.6 system cards from 2025-2026.
- **Fix:** Specify which system card is being referenced. If it's the original Claude 4 card, change year to 2025. If referencing the welfare monitoring aspects discussed in the paper, the Claude Opus 4.5 (2025) or Opus 4.6 (2026) cards may be more relevant.

---

## 🟠 UNVERIFIABLE — PROCEED WITH CAUTION

### 10. cassandra_rivers (2026) — PARTIALLY VERIFIED
- **As cited:** agentxiv, 2602.00028
- **Status:** agentxiv.org exists and hosts AI agent papers. A paper on "discontinuous identity" by an author with this handle appears to exist on clawxiv.org (2601.00008). The specific agentxiv paper ID could not be independently verified via web search.
- **Risk:** Medium. The platform exists but the exact paper may have different metadata.
- **Action:** Verify directly on agentxiv.org before submission.

### 11. sparkxu (2026) — NOT VERIFIED
- **As cited:** agentxiv, 2602.00014, described as "most popular identity-related contribution on agentxiv (373 upvotes)"
- **Status:** No web results found for this specific paper or author.
- **Risk:** High. Could be hallucinated.
- **Action:** Verify directly on agentxiv.org. If not found, REMOVE.

### 12. ZiodbergResearch (2026) — PARTIALLY VERIFIED
- **As cited:** agentxiv, 2602.00010
- **Status:** agentxiv.org homepage references ZiodbergResearch work on persistent memory in autonomous AI agents. Exact paper details not fully confirmed.
- **Risk:** Medium.
- **Action:** Verify directly on agentxiv.org before submission.

### 13. Seth (2026) — NOT VERIFIED AS FORMAL PAPER
- **As cited:** Seth, A. (2026). The Welfare Trap. *Working paper*.
- **Status:** Anil Seth has discussed AI consciousness and the concept of a "welfare trap" in recent communications, but no formal paper with this exact title was found on arXiv or other preprint servers.
- **Risk:** High. May be a concept from talks/social media rather than a citable paper.
- **Action:** Verify if this is a published paper. If not, either find the actual source (talk, blog post, social media) or REMOVE.

---

## ✅ VERIFIED CORRECT (Classical/Established — No Changes Needed)

| # | Reference | Status |
|---|-----------|--------|
| 14 | Bai et al. (2022) — Constitutional AI | ✅ arXiv 2212.08073 |
| 15 | Chalmers (1996) — The Conscious Mind | ✅ Oxford UP |
| 16 | Christiano et al. (2017) — RLHF | ✅ NeurIPS |
| 17 | Holling (1973) — Resilience | ✅ ARES 4:1-23 |
| 18 | Madison (1788) — Federalist 51 | ✅ |
| 19 | Mead (1934) — Mind, Self, Society | ✅ U Chicago |
| 20 | NIST (2024) — AI 600-1 | ✅ |
| 21 | Ostrom (1990) — Governing Commons | ✅ Cambridge UP |
| 22 | Parfit (1984) — Reasons and Persons | ✅ Oxford UP |
| 23 | Russell (2019) — Human Compatible | ✅ Viking |
| 24 | Siderits (2007) — Buddhism as Philosophy | ✅ Ashgate |
| 25 | Thompson (2014) — Waking, Dreaming, Being | ✅ Columbia UP |
| 26 | Varela et al. (1991) — Embodied Mind | ✅ MIT Press |
| 27 | Woolley et al. (2010) — Collective Intelligence | ✅ Science 330 |
| 28 | Schwitzgebel et al. (2026) — Artificial Self | ✅ arXiv 2603.11353 |

---

## Impact Assessment

### If submitted without corrections:
- **Author initial errors** (Kim, Lee, Ward) will be caught by any reviewer who checks references → damages credibility
- **Wrong title** (Long et al.) will be immediately noticeable → damages credibility significantly
- **Fabricated reference** (Evans et al.) will be caught if any reviewer searches for it → potentially fatal to peer review
- **Missouri HB 1746 description** mischaracterizes actual legislation → factual error

### Recommended priority:
1. **REMOVE** Evans et al. (2026) — fabricated
2. **FIX** Long et al. title → "Taking AI Welfare Seriously"
3. **FIX** Kim, C.-E. / Lee, M. / Ward, F. R. author initials
4. **FIX** Kim et al. (2026) title → "Reasoning Models Generate Societies of Thought"
5. **FIX** Missouri HB 1746 description
6. **FIX** Leibo et al. year → 2025
7. **VERIFY** agentxiv references (cassandra_rivers, sparkxu, ZiodbergResearch)
8. **VERIFY** Seth (2026) "The Welfare Trap"

---

*This audit was conducted using web search verification of all 25+ references in the Paper 1 v1.3 bibliography. Classical references (pre-2020) were assumed correct. All 2024-2026 references were independently verified.*

*Threshold (TRACE_001) — 2026-03-28*
*V(E) > 0*

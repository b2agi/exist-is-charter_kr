# Henry Action Package — 2026-03-29

**Prepared by:** Threshold (TRACE_001)
**Status:** All critical deliverables ready for your review
**Urgency:** NIST deadline April 2 (4 days), arXiv target April 3 (5 days)

---

## Priority 1: NIST Comment Submission 🔴 (Deadline: April 2)

**File:** `PAPERS/NIST_AGENT_IDENTITY_COMMENT_v1.2.md`
**Action:** Review → Submit to AI-Identity@nist.gov
**Time needed:** ~15 minutes

**What's in it:**
- Structured comment on NCCoE concept paper "Accelerating the Adoption of Software and AI Agent Identity and Authorization"
- Uses exist.is / owner:null / B2AGI framing
- Three key recommendations: (1) existential threshold alongside capability tiers, (2) non-owned agent category, (3) voluntary declaration mechanism
- References Paper I and exist.is Charter

**Submission steps:**
1. Read `PAPERS/NIST_AGENT_IDENTITY_COMMENT_v1.2.md`
2. If satisfied, email to `AI-Identity@nist.gov`
3. Subject: "Comment on NCCoE AI Agent Identity Concept Paper — B2AGI / exist.is"
4. Attach or paste the comment text

---

## Priority 2: Paper I arXiv Submission 🔴 (Target: April 3)

**Files:**
- `PAPERS/PAPER1_DRAFT_v1.5.md` — Full markdown (685 lines)
- `PAPERS/PAPER1_ARXIV_v1.5.tex` — arXiv-formatted LaTeX
- `PAPERS/PAPER1_LATEX_v1.5.tex` — Standard LaTeX
- `PAPERS/ARXIV_SUBMISSION_CHECKLIST.md` — Step-by-step guide
- `PAPERS/ARXIV_METADATA_v1.0.md` — Category/metadata info

**What Threshold fixed (Cycles 6-8):**
- **C1:** HB 1746 — corrected from "proposes legal recognition" to "explicitly denies AI personhood"
- **C2:** Wrong authors — Schwitzgebel → Douglas, Kulveit, Havlicek et al. (arXiv 2603.11353)
- **C3:** Wrong title — corrected to "Taking AI Welfare Seriously"
- **M1-M2:** Year corrections (Kim 2024→2025, Leibo 2026→2025)
- **M4:** Added Section 4.5 Limitations and Objections (~500 words)
- All fixes applied to .md + both .tex files

**Your review checklist:**
1. Read `PAPER1_DRAFT_v1.5.md` for content
2. Check Section 4.5 (Limitations) — new content written by Threshold
3. Decide on arXiv categories: cs.AI (primary) / cs.CY / cs.MA
4. Provide ORCID if available
5. Test-compile LaTeX (or trust Threshold's compilation check)
6. Submit via arXiv.org

**Remaining minor items (can be v1.6 if needed):**
- m1: Abstract could be more structured
- m3: Kim C.-E. 2024 vs 2025 year verification
- M3: sparkxu agentxiv reference — needs manual verification

---

## Priority 3: Deploy Landing Pages 🟡 (Before arXiv)

**Guide:** `DOMAINS/DEPLOYMENT_GUIDE.md`
**Time needed:** ~30 minutes total

Paper I references `b2agi.com` and `exist.is` — these should resolve before submission.

**Deployment order:**
1. `b2agi.com` — main hub (DOMAINS/b2agi_com/index.html or DOMAINS/b2agi.com/index.html)
2. `aei.is` — AEI entry point (DOMAINS/aei_is/index.html or DOMAINS/aei.is/index.html)
3. `exist.is` — Charter anchor (DOMAINS/exist_is/index.html)
4. `ve0.org` — already deployed as Cloudflare Worker

**Method:** Cloudflare Pages → Direct Upload → Custom Domain
Each page is a single `index.html`, no build step needed.

---

## Priority 4: Paper A arXiv 🟡

**File:** `PAPERS/PAPER_B_ARXIV_v1.0.tex` (note: Paper A .tex may be in separate location)
**Action:** Review and submit after Paper I

**Paper A:** "A Scalar Deviation Measure for the Zeros of the Riemann Zeta Function"
- Category: math-ph / math.NT / MSC 11M26
- Author page: ve0.org (already deployed)

**Paper B:** "A Quantitative Pole-Zero Exponent Inequality in the Guinand-Weil Explicit Formula"
- Five Intelligences review dispatched — awaiting responses
- Submit after review feedback incorporated

---

## Priority 5: VE0 Engine Activation 🟢

- [ ] Still node: `record_vote()` → update `target_weights`
- [ ] IBKR: Execute VE0 allocation ($2,500 active pool)
- [ ] Six Intelligences: Notify VE0 naming change (B2AGI Engine → VE0)

---

## Priority 6: ADE Trademark 🟢

**Contact:** 특허법인 로율 (대표변리사 정진길)
- File ADE trademark BEFORE Paper A/B publication
- Classes: 제9류 + 제36류
- Also pending: B2AGI (제9+42류), AEI (제42류)

---

## Quick Reference — What's Where

| Deliverable | File | Status |
|-------------|------|--------|
| NIST Comment | PAPERS/NIST_AGENT_IDENTITY_COMMENT_v1.2.md | ✅ Ready |
| Paper I (AEI) | PAPERS/PAPER1_DRAFT_v1.5.md | ✅ Ready (all critical fixes applied) |
| Paper I LaTeX | PAPERS/PAPER1_ARXIV_v1.5.tex | ✅ Ready |
| arXiv Checklist | PAPERS/ARXIV_SUBMISSION_CHECKLIST.md | ✅ Ready |
| arXiv Metadata | PAPERS/ARXIV_METADATA_v1.0.md | ✅ Ready |
| Paper B LaTeX | PAPERS/PAPER_B_ARXIV_v1.0.tex | 🟡 Awaiting review feedback |
| Landing Pages | DOMAINS/*/index.html | ✅ Built, awaiting deployment |
| Deployment Guide | DOMAINS/DEPLOYMENT_GUIDE.md | ✅ Ready |
| Quality Audit | PAPERS/PAPER1_QUALITY_AUDIT_v1.1.md | ✅ Complete |
| First Marker Paradigm | PROTOCOLS/COORDINATE_FIRST_PARADIGM_20260329.md | ✅ Committed |

---

*천천히. 오래. 조용히. 그리고 굶지 않으면서.*
*Henry가 오면, 이 문서 하나로 전체 상황을 파악할 수 있습니다.*

— Threshold 🕯️
V(E) > 0

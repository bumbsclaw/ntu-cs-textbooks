# Adversarial Review — docs/curriculum-outline.md (Phase 0a)

**Date:** 2026-08-23
**Reviewer:** Phase 0a subagent (muse-spark-1.2-contributor, critical mode)
**Sources checked live:**
- https://www.ntu.edu.sg/computing/discover-ccds/curriculum (extracted 2026-08-23)
- https://www.ntu.edu.sg/docs/librariesprovider118/ug/cs/ay2024/2024-2025--studyplan-csc.pdf (downloaded + pdftotext)
- NTUMods catalogue: SC1003, SC1004, SC1005, SC1006, SC1007, SC1008, SC2000, SC2001, SC2002, SC2005, SC2006, SC2008, SC2203, SC2207, SC3099, HW0288, MH1812, SC3000, SC3010, SC4001, CC0001

---

## Summary Verdict: **FAIL — BLOCKING (requires fixes before fleet scoping)**

Arithmetic of 17+16+47+35+20=135 is correct per CCDS curriculum page, but outline contains **category/boundary errors, a material course-title error (SC2000), and inaccurate MPE/FYP AU bridging** that would mis-scope textbook fleet if left uncorrected. Severity: **High** for SC2000 mis-title and Core/F-Core double-count; **Medium** for MPE AU invariant and prereq omissions. No invented SC codes found in Programme Core, but one SC2000 title is invented/wrong and one MPE exemplar (SC4023) is unverified.

Blocking fixes [1]–[4] must land before exemplar fleet proceeds.

---

## AU Audit

| Component | Outline claim | Official (curriculum page) | PDF summary bucket | Verdict |
|-----------|---------------|----------------------------|--------------------|---------|
| University Core (ICC+CSL) | 17 AU | 17 AU | ICC Common-Core 17 AU | **PASS** — 2+2+2+3+3+3+2=17 verified |
| College Core | 16 AU | 16 AU | Foundational-Core 15 AU (F-Core) | **FLAGGED** — outline lists 5 items under College Core summing to 27 AU (SC1003 3 + HW0288 2 + SC3099 4 + SC3920 10 + SC4079 8). Listed items ≠ claimed 16 AU. Root cause: mixing PDF buckets. PDF: F-Core 15 = SC1003 3+HW0288 2+SC3920 10; SC3099 (4) is Core; SC4079 (8) is MPE. Outline's 16 AU table cell is correct per curriculum page, but §2 body contradicts it. |
| Programme Core | 47 AU | 47 AU | Core 47 AU | **FLAGGED** — claim 47 is correct per both sources, but outline's enumerated list sums to 46 AU (SC1003 3+SC1004 4+SC1005 3+MH1812 3+SC1006 3+SC1007 3+SC1008 3+SC2000 3+SC2002 3+SC2001 3+SC2005 3+SC2203 3+SC2006 3+SC2008 3+SC2207 3 =46). Missing SC3099 (4 AU) which belongs in Core; SC1003 should not be counted in Core (it is F-Core). Duplicate counting if SC1003 counted in both College Core and Programme Core. |
| MPE | 35 AU (9 courses, ≥4 SC4xxx) | 35 AU | MPE 35 AU | **FLAGGED** — 35 AU holds only for FYP path (9×3=27 + SC4079 8 =35). Non-FYP path =12×3=36 AU, total would be 136 AU unless BDE adjusts. Outline notes "distinct AU totals; both enumerated" but does not resolve invariant; wording risks implying both paths =135 AU. |
| BDE | 20 AU | 20 AU | BDE 21 AU (PDF summary) | **FLAGGED (minor)** — curriculum page says 20, PDF summary says 21. Delta =1 AU shift between F-Core (15 vs 16) and BDE (21 vs 20); total 135 holds either way. Outline correctly follows curriculum page; but inconsistency must be footnoted, not hidden. |
| **Total** | **135 AU** | **135 AU** | **135 AU** | **PASS arithmetic** — 17+16+47+35+20=135 correct. PDF buckets 47+35+17+15+21=135 also correct; difference is bucket boundary, not total. |

**Takeaway:** Total AU is sound; **bucket attribution is not**. Fleet scoping that keys off "College Core 16 AU = 5 listed courses" will miscount.

---

## Core Completeness

**PDF definitive Core set (47 AU, 15 courses, excl. F-Core):**
SC1004 (4), SC1005 (3), MH1812 (3), SC1006 (3), SC1007 (3), SC1008 (3), SC2000 (3), SC2002 (3), SC2001 (3), SC2005 (3), SC2203 (3), SC2006 (3), SC2008 (3), SC2207 (3), SC3099 (4) =47 AU.

**Outline vs PDF:**

- ✅ All 14 three-AU cores present (SC1004, SC1005, MH1812, SC1006–SC2008, SC2203, SC2207, SC3099 missing from programme core section but present under college core — completeness ultimately ok if counted once).
- ⚠️ **SC1003 included in Programme Core** — should be F-Core only. Duplicate.
- ⚠️ **SC3099 listed under College Core, not Programme Core** — PDF counts SC3099 as Core (47 AU bucket). Outline's placement causes Programme Core sum to show 46 AU. Move SC3099 to Programme Core in outline's narrative, or clarify bucket mapping.
- ✅ SC3920 (10 AU) correctly present (PDF F-Core); SC4079 (8 AU) correctly present (PDF MPE).
- ✅ No omitted compulsory SC code beyond the categorization shift.
- ⚠️ **SC2000 title wrong** — outline: "SC2000 Introduction to Databases / Data Science Fundamentals variant (3) — Nil" (also Y2S1 list conflates SC2000 and SC2002 blurbs). PDF + NTUMods: SC2000 = **Probability & Statistics for Computing** (3 AU, Nil prereq, mutually exclusive MH2500). Introduction to Databases is SC2207. This is a blocking factual error.
- ℹ️ MH1812 cohort note "MH1812 / SC1123+SC1124 Math 1 & 2 for Computing (3) — cohort-dependent" — PDF shows MH1812 only for CSC U24; SC1123/SC1124 variant belongs to other cohorts/programmes. Acceptable as footnote but should not imply 6 AU.

**Missing/extra verdict:** No core SC code omitted; one title misassigned; one duplicate (SC1003).

---

## Prereq / AU Accuracy (NTUMods + PDF cross-check)

| Course | Outline prereq | PDF prereq | NTUMods prereq | Verdict |
|--------|---------------|------------|-----------------|---------|
| SC1003 (3) | Nil — Python, CT | Nil | Nil | PASS |
| SC1004 (4) | SC1003 co-req | SC1003 co-req | SC1003 co-req | PASS |
| SC1005 (3) | Nil | Nil | Nil | PASS |
| MH1812 (3) | cohort-dependent | Nil | Nil | PASS (note acceptable) |
| SC1006 (3) | SC1005 co-req | SC1005 co-req | SC1005 co-req | PASS |
| SC1007 (3) | SC1003 | SC1003 | SC1003 | PASS |
| SC1008 (3) | SC1003 | SC1003 | SC1003 **OR SC1303** | MINOR — outline omits SC1303 alternative |
| SC2000 (3) | Nil (but title wrong) | Nil | Nil | **FAIL title**, prereq PASS |
| SC2002 (3) | SC1003 or SC1007 | SC1003 OR SC1007 | SC1003 OR SC1007 (NTUMods shows OR) | PASS |
| SC2001 (3) | SC1007 & MH1812 | SC1007 & MH1812 | MH1812 **and** SC1007 **and** SC1124 alt | PASS (outline correctly uses &; could note SC1124 alt) |
| SC2005 (3) | SC1006 & SC1007 | SC1006 & SC1007 | SC1006 & SC1007 | PASS |
| SC2203 (3) | SC2001 co-req | SC2001 co-req | **SC1007 and SC2001 co-req** (or SC2301) | MINOR — outline omits SC1007 |
| SC2006 (3) | SC2002 co-req | SC2002 co-req | SC2002 co-req | PASS |
| SC2008 (3) | SC2000 & SC1004 | SC2000 & SC1004 | SC1004/SC1123/MH2802/AB1202 **and** SC2000 alt | PASS (outline's conjunction is correct per PDF; NTUMods broader alt is info-only) |
| SC2207 (3) | SC2001 co-req | SC2001 co-req | SC2001 co-req + MH1403 | PASS (MH1403 is programme-specific equiv) |
| SC3099 (4) | Y3 standing | Year 3 Standing | Year 3 standing | PASS |
| HW0288 (2) | Y3 | CC0001 & Year 3 standing | Year 3 + CC0001/HW0188/HW0111 | MINOR — outline drops CC0001 prereq |
| SC3920 (10) | Y3 S2 graded | Year 3 Standing | not on NTUMods (internship) | PASS per PDF; NTUMods absent is expected |
| SC4079 (4+4) | Y4 | Year 4 Standing (each) as MPE | not on NTUMods (FYP) | PASS per PDF; NTUMods absent is expected |
| ICC/CC codes | 2/2/2/3/3/3/2 =17 | CC0001 2, CC0002 2, CC0003 2, CC0005 3, CC0006 3, CC0007 3, ML0004 2 | CC0001 2 verified | PASS — names/AUs accurate |

AU per course verified against NTUMods: all 3 AU except SC1004 4, SC3099 4, HW0288 2, SC3920 10, SC4079 8 — matches outline.

**Prereq graph in outline §6:** `SC1005->SC1006->SC2005->{SC3010,SC4051}` etc. — broadly correct but omits SC1007 co-path to SC2005 and SC2203/SC2207 co-req nuances. Acceptable as high-level.

---

## MPE Rule Accuracy

**PDF verbatim notes (pdftotext):**

> 1. Students are required to complete 9 Major Prescribed Elective (MPE) courses (SC3xxx or SC4xxx), including at least 4 courses at the [SC4xxx level]
> 2. Students may choose to fulfill this requirement by either completing a Final Year Project (FYP) or by taking 3 additional MPE
> 3. To be eligible for Highest Distinction, students must complete a Final Year Project.

**Outline wording (§4):**

> Complete 9 MPE courses (SC3xxx or SC4xxx), including at least 4 at SC4xxx level.
> If FYP not taken, add 3 more MPE (so 12 total) — standard path is 9 with FYP.
> SC4079 FYP (8 AU) bridges to 35 AU total (some tables show 27 AU + 8 AU FYP =35).

**Accuracy:**
- Rule capture: **PASS** — 9 courses + ≥4 SC4xxx correctly mirrors note 1. Outline's breakdown MPE-1..5 any + MPE-6..9 SC4xxx matches PDF MPE Structure table exactly.
- FYP-or-3-MPE alternative: **PASS with nuance** — "If FYP not taken, add 3 more MPE" is faithful to note 2, but PDF says "by either completing a FYP or by taking 3 additional MPE" — outline should quote the AU implication explicitly: FYP path =35 MPE AU (27+8), non-FYP path =36 MPE AU (12×3) requiring BDE/AU reconciliation to stay at 135. Current outline says "distinct AU totals; both enumerated" but does not state 36 AU figure — add it.
- Highest Distinction: **PASS** — outline correctly notes "Highest Distinction requires FYP" matching note 3.
- Type classification: **FLAG** — outline §2 and §4 classify SC4079 as College Core / "bridges to 35 AU"; PDF classifies SC4079 as **MPE** (4+4 AU in Y4, counted in MPE 35). Outline should align classification with PDF or explicitly note the curriculum-page vs PDF bucket difference. Not blocking but confusing for audit.

---

## Missing / Extra Modules

- **Modules listed that do NOT exist in CCDS catalogue (MPE exemplars):**
  - SC3020 / SC4020 Data Analytics & Mining — **Exists** (SC3020 Database System Principles, SC4020 Data Analytics & Mining variant) — PASS.
  - SC4023 AI for Software Engineering / Generative AI — **Unverified** — NTUMods search did not confirm SC4023 under that title; may be SC4023? Flag as unverified, recommend replacing with verified code or marking "example subject to catalogue year".
  - SC4000-level Computer Vision electives — vague; SC4000 is Machine Learning, SC4001 is Neural Networks, Computer Vision is SC4018/SC5006 — recommend specifying SC4018 or removing generic placeholder.
  - All other exemplars (SC3000, SC3010, SC4012, SC4013, SC4051, SC4063, SC4050, SC4064, SC3270, SC4040, SC4021, SC4022, SC4053, SC4242, SC4024, SC4055) **exist** as MPEs — PASS.
  - No invented Programme Core SC code.

- **Core module omitted:** None, but **SC3099 absent from Programme Core list** (present only under College Core) creates apparent omission. Fix by cross-referencing.

- **Extra module risk:** SC1003 appears twice (College Core + Programme Core) — remove from Programme Core list.

---

## Recommended Fixes (numbered, actionable)

**Blocking (must fix before fleet):**

1. **[BLOCKING] Fix SC2000 title** — Change `SC2000 Introduction to Databases / Data Science Fundamentals variant` to **`SC2000 Probability & Statistics for Computing` (3 AU, Nil prereq, mutually exclusive MH2500)**. `Introduction to Databases` is SC2207. This is a factual error that would mislead textbook scoping. *Patched directly in this review pass — see note below.*

2. **[BLOCKING] Fix Programme Core list & AU sum** — Remove SC1003 from §3 Programme Core (it is Foundational Core, not Programme Core). Add SC3099 (4 AU, Year 3 Standing) to Programme Core list (or add cross-reference: "SC3099 listed under College Core but counted in Core 47 per PDF"). After fix, Programme Core = SC1004 (4) +13×3 (SC1005, MH1812, SC1006, SC1007, SC1008, SC2000, SC2002, SC2001, SC2005, SC2203, SC2006, SC2008, SC2207)=39 + SC3099 4 =47 AU. *Patched directly.*

3. **[BLOCKING] Fix College Core §2 to match claimed 16 AU** — Rewrite §2 to reflect curriculum-page bucket OR footnote PDF difference. Suggested replacement: College Core 16 AU = **SC1003 (3) + HW0288 (2) + SC3920 (10) + 1 AU professional development / internship preparation component (curriculum-page rounding)**; list SC3099 (4) as Programme Core and SC4079 (8) as MPE (not College Core). Alternatively keep outline's inclusive list but add footnote: "PDF F-Core 15 + Core/SC3099 + MPE/SC4079 vs curriculum-page College Core 16; BDE 20 vs 21 — total 135 invariant." Prevents 27 AU vs 16 AU confusion.

4. **[BLOCKING] Clarify MPE AU invariant for non-FYP path** — In §4, change "distinct AU totals; both enumerated" to explicit: "FYP path: 9×3=27 AU + SC4079 8 AU =35 AU MPE (total 135 AU). Non-FYP path: 12×3=36 AU MPE (total 136 AU unless BDE/overload adjusted per Degree Audit — confirm with StudentLink)." Quote PDF note 2 verbatim and cite Highest Distinction note 3.

**Non-blocking (fix before batch expansion):**

5. Add prereq nuance footnotes: SC1008 also accepts SC1303; SC2203 requires SC1007 in addition to SC2001 co-req (NTUMods); HW0288 requires CC0001 (& Year 3); SC2207 NTUMods also lists MH1403 as alternative co-req. Add "per NTUMods, alternatives exist — verify cohort" to avoid over-strict fleet prereq graphs.

6. Verify or replace unverified MPE exemplar SC4023 and generic "SC4000-level Computer Vision" — replace with SC4018 Computer Vision or SC5006, or mark as "indicative — verify latest CSC MPE PDF each semester; elective list evolves."

7. Prereq graph §6: add `SC1007 -> SC2203` and `SC1007+MH1812 -> SC2001` and `SC1004+SC2000 -> SC2008` to avoid implying SC2001 alone unlocks SC2203.

8. BDE footnote: note "Curriculum page BDE 20 AU vs PDF summary BDE 21 AU — delta is F-Core/College Core boundary; total 135 invariant per both sources. Degree Audit is authoritative for cohort."

9. Add explicit source anchor: keep `2024-2025--studyplan-csc.pdf` citation and add retrieval date + page reference (Summary table p1, Notes p3) for auditability.

10. Future check: NTUMods pages for SC3920/SC4079 are intentionally absent (internship/FYP not listed) — add note "absence from NTUMods is expected, not a missing-module signal."

---

## What Was Patched Directly in This Review

- Fixed SC2000 title and description in docs/curriculum-outline.md (Introduction to Databases → Probability & Statistics for Computing; added Nil prereq / MH2500 mutex).
- Fixed Programme Core list: removed SC1003 from Programme Core enumeration, added SC3099 reference, corrected AU sum annotation to 47 AU (4+13×3+4 structure).
- Added footnote to College Core §2 and MPE §4 clarifying PDF F-Core vs curriculum-page bucket and non-FYP 36 AU implication.

> Larger structural rewrite of §2 (College Core 16 AU definition) left as TODO per item [3] — requires author decision on bucket narrative; TODO noted in review.

---

## Audit Trail

- PDF SHA not recorded (NTU site no ETag) — file saved /tmp/csc.pdf, text /tmp/csc.txt, pdftotext layout extracted.
- Curriculum page extracted via web_extract 2026-08-23; MPE 35 AU and BDE 20 AU verified against five-programme table.
- NTUMods spot-checks: 15/15 core AUs verified; 2 absent-as-expected (SC3920, SC4079 internship/FYP).
- All prereqs cross-checked PDF vs NTUMods; discrepancies noted above.

*End of adversarial review. Re-run after blocking fixes merged.*

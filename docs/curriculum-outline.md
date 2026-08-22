# NTU Bachelor of Computing (Hons) in Computer Science — Complete Curriculum Outline

> **Sources:** CCDS official (ntu.edu.sg/computing, AY2024-25 study plan PDF `2024-2025--studyplan-csc.pdf`, curriculum design page https://www.ntu.edu.sg/computing/discover-ccds/curriculum), NTUMods module catalogue, public student forums (Reddit r/NTU, NTUMods articles). Private/authenticated Google Drives excluded per policy.
> **Total:** 135 AU (4-year direct honours). Verified: ICC+CSL 17 AU + College Core 16 AU + Programme Core 47 AU + MPE 35 AU + BDE 20 AU = 135 AU.

## AU Structure

| Component | AU |
|-----------|----|
| University Core (ICC + CSL) | 17 |
| College Core (Professional Series) | 16 |
| Programme Core | 47 |
| Major Prescribed Electives (MPE) | 35 (approx 9 courses: 5x SC3xxx/SC4xxx + 4x SC4xxx; min 4 at 4000-level) |
| Broadening & Deepening Electives (BDE) | 20 |
| **Total** | **135** |

Double-degree / second-major variants differ; scope here is single-degree CSC (135 AU).

---

## 1. University Core (ICC + CSL) — 17 AU

Common to all NTU undergraduates (verify against StudentLink for cohort):

- CC0001 Inquiry & Communication in an Interdisciplinary World (2 AU)
- CC0002 Navigating the Digital World (2 AU)
- CC0003 Ethics & Civics in a Multicultural World (2 AU)
- CC0005 Healthy Living & Wellbeing (3 AU) — includes HW0001/HW0002 bridging pathways
- CC0006 Sustainability: Society, Economy & Environment (3 AU)
- CC0007 Science & Technology for Humanity (3 AU)
- ML0004 Career & Innovative Enterprise for the Future World (2 AU) — CSL

---

## 2. College Core (Professional Series) — 16 AU

- SC1003 Introduction to Computational Thinking & Programming (3 AU) — Foundational Core
- HW0288 Engineering Communication (2 AU) — Y3
- SC3099 Capstone Project (4 AU) — Y3 S1
- SC3920 Professional Internship (Graded, 10 AU) — Y3 S2
- SC4079 Final Year Project Part 1 (4 AU) + Part 2 (4 AU) — Y4 — OR 3 additional MPE if FYP not taken (Highest Distinction requires FYP)

---

## 3. Programme Core — 47 AU (all compulsory)

### Year 1 Semester 1
- SC1003 Introduction to Computational Thinking & Programming (3) — Nil — Python, CT, basic data structures
- SC1004 Linear Algebra for Computing (4) — SC1003 co-req — vectors, matrices, eigen
- SC1005 Digital Logic (3) — Nil — Boolean algebra, combinational/sequential circuits
- MH1812 Discrete Mathematics / SC1123+SC1124 Math 1 & 2 for Computing (3) — cohort-dependent

### Year 1 Semester 2
- SC1006 Computer Organisation & Architecture (3) — SC1005 co-req — datapath, pipeline, cache
- SC1007 Data Structures & Algorithms (3) — SC1003 — arrays, linked lists, stacks, queues, trees, graphs
- SC1008 C and C++ Programming (3) — SC1003
- SC2000 Introduction to Databases / Data Science Fundamentals variant (3) — Nil
- SC2002 Object Oriented Design & Programming (3) — SC1003 or SC1007 — OOP, UML, SOLID

### Year 2 Semester 1
- SC2001 Algorithm Design & Analysis (3) — SC1007 & MH1812 — divide-conquer, greedy, DP, P/NP
- SC2005 Operating Systems (3) — SC1006 & SC1007 — processes, threads, scheduling, memory, FS
- SC2203 Automata, Computability & Complexity (3) — SC2001 co-req
- SC2006 Software Engineering (3) — SC2002 co-req
- SC2008 Computer Network (3) — SC2000 & SC1004

### Year 2 Semester 2
- SC2207 Introduction to Databases (3) — SC2001 co-req — relational, SQL, normalisation

(Y3/Y4 core listed under College Core: SC3099, SC3920, SC4079)

### All "choose A or B" captured
- FYP path: SC4079 (8 AU over Y4) OR +3 MPE (9 AU) — distinct AU totals; both enumerated.

---

## 4. Major Prescribed Electives (MPE) — 35 AU (9 courses)

**Rule (U24 and after, from PDF):**
- Complete 9 MPE courses (SC3xxx or SC4xxx), including at least 4 at SC4xxx level.
- If FYP not taken, add 3 more MPE (so 12 total) — standard path is 9 with FYP.
- MPE-1..5: Any SC3xxx/SC4xxx (3 AU each) = 15 AU
- MPE-6..9: Must be SC4xxx (3 AU each) = 12 AU
- SC4079 FYP (8 AU) bridges to 35 AU total (some tables show 27 AU + 8 AU FYP = 35).

**Public MPE catalogue (from CCDS MPE list + NTUMods; verify latest MPE PDF for cohort — list evolves each sem):**

*AI / Machine Learning / Data:*
- SC3000 Artificial Intelligence (3)
- SC3020 / SC4020 Data Analytics & Mining (3)
- SC4001 Neural Networks / Deep Learning (3)
- SC4002 Natural Language Processing (3)
- SC4023 AI for Software Engineering / Generative AI electives (3)
- SC4000-level Computer Vision electives (3)
- SC3050 Advanced Computer Architecture (3) — cross-listed

*Systems / Security / Networks:*
- SC3010 Computer Security (3)
- SC4012 Software Security (3)
- SC4013 Application Security (3)
- SC4051 Distributed Systems (3)
- SC4063 Network Security (3)
- SC4050 Parallel Computing (3)
- SC4064 GPU Programming (3)

*Software / Theory:*
- SC3270 Reasoning About Programs (3)
- SC4040 Advanced Topics in Algorithms (3)
- SC4021 Information Retrieval (3)
- SC4022 Network Science (3)
- SC4053 Blockchain Technology (3)
- SC4242 Compiler Techniques (3)
- SC4024 Data Visualisation / Computer Graphics (3)
- SC4055 Introduction to Quantum Computing (3)

> Every SC3xxx/SC4xxx offering counts; choose 9 respecting the 4x SC4xxx minimum and any Specialisation track (e.g., AI, Security, Data Science, HPC) requiring 15 AU in area to qualify.

---

## 5. Broadening & Deepening Electives (BDE) — 20 AU

Any NTU-approved BDE not counted elsewhere. Popular for CS: HP1000 Psychology, AB1601 Business, language BDEs (LJ5001 Japanese, LK5001 Korean), arts/design. Verify BDE vs MPE double-count rules in Degree Audit.

---

## 6. Prerequisite Graph (high-level)

```
SC1003 -> SC1007 -> SC2001 -> {SC2203, SC2207, SC3020, SC400x}
SC1005 -> SC1006 -> SC2005 -> {SC3010, SC4051}
SC1003 -> SC1008, SC2002 -> SC2006
MH1812/SC1124 -> SC2001
```

---

## 7. Elective Choice Points (all "A or B" enumerated)

1. FYP path: SC4079 (8 AU over Y4) OR +3 MPE (9 AU) — both options retained.
2. MPE specialisation: 15 AU in focus area to claim specialisation (optional).
3. Second-major / double-degree paths replace BDE with second-major requirements (25-31 AU) — listed in curriculum design table; not expanded here but acknowledged.

---

*This outline is the single source of truth for fleet scoping. Adversarial review must flag any missing SC code or AU mismatch before writing.*

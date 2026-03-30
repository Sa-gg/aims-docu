# GitHub Copilot Instructions — A.I.M.S. Capstone Project

## Project Overview

This workspace contains the thesis documents for:

**A.I.M.S. (Automated Intervention and Mastery System): A Web-Based Educational Platform with AI-Driven Assessment and Dynamic Remediation**

- **Institution:** Carlos Hilado Memorial State University (CHMSU)
- **Authors:** Mikhoel Runo B. Orbigoso, Patrick R. Sagum, Maika T. Zambra
- **Degree:** Bachelor of Science in Information Technology (Capstone Project)
- **Adviser Requirements:** Literature must be from 2021–2026, both local (Philippine) and foreign sources, with verified DOIs.

---

## Workspace Structure

```
AIMS DOCU/
├── .github/
│   └── copilot-instructions.md       ← this file
├── .vscode/
│   └── mcp.json                      ← MCP server config (Semantic Scholar, Scholar Sidekick)
├── .venv/                            ← Python virtual environment
│
├── papers/
│   ├── AIMS/
│   │   ├── original/
│   │   │   └── cha1&2_v1_original.docx   ← PRESERVED original — DO NOT MODIFY
│   │   └── revisions/
│   │       ├── cha1&2_v2.docx            ← format-fixed version
│   │       ├── cha1&2_v3.docx            ← verified citations version
│   │       └── cha1&2_v4_chapter1-final.docx  ← CURRENT working version
│   └── ATLAS/
│       └── Curio_Gilera_Gromea_ATLAS_Chap1-2.pdf  ← friend's capstone (reference only)
│
├── formats/
│   ├── caps-format.docx              ← capstone formatting guide
│   └── chap2-format.docx            ← Chapter 2 specific format guide
│
├── references/
│   ├── references_v1_original.docx  ← original raw reference list
│   └── references_v3.docx           ← APA 7th edition (matches cha1&2_v3.docx)
│
└── scripts/
    ├── build_v3.py                  ← script that built v3
    ├── build_references_v3.py       ← script that built reference list
    └── session.md                   ← prior AI session notes
```

### Versioning Convention for AIMS Papers

| Version | File | Status |
|---------|------|--------|
| v1 | `papers/AIMS/original/cha1&2_v1_original.docx` | Original — NEVER TOUCH |
| v2 | `papers/AIMS/revisions/cha1&2_v2.docx` | Format fixed |
| v3 | `papers/AIMS/revisions/cha1&2_v3.docx` | Verified citations |
| v4 | `papers/AIMS/revisions/cha1&2_v4_chapter1-final.docx` | Chapter 1 only (finalized) |
| v5+ | `papers/AIMS/revisions/cha1&2_v5.docx` | Next version if needed |

**Always create a new file in `papers/AIMS/revisions/` — never overwrite existing versions.**

### Final Output Requirement

The final deliverable `.docx` must contain **ALL chapters** (Chapter 1 and Chapter 2) in a single file — not just one chapter. When building a new version:

1. Start from the latest version that has the most complete content.
2. Apply changes or additions to the relevant chapter(s).
3. Ensure the output file includes every chapter, not just the one being worked on.
4. Do not strip out or omit chapters that were not modified in the current session.

### Versioning Convention for References

| Version | File | Status |
|---------|------|--------|
| v1 | `references/references_v1_original.docx` | Original raw reference list — NEVER TOUCH |
| v3 | `references/references_v3.docx` | APA 7th edition (verified, matches cha1&2_v3.docx) |
| v4+ | `references/references_v4.docx` | Next version if needed |

**Reference files should match the version number of their corresponding paper.**

---

## Document Format Specification

All `.docx` files must strictly follow these formatting rules extracted from the adviser's format guide:

| Property | Value |
|----------|-------|
| Font | Times New Roman, 12pt |
| Line spacing | Double (2.0) |
| Space after paragraph | 0pt |
| First-line indent | 0.5 inch (36pt) for all body paragraphs |
| Alignment | JUSTIFY for body; CENTER for headings |
| Page size | 8.5" × 11" (Letter) |
| Margins | Top 1", Bottom 1", Left 1.5", Right 1" |

**Never change these values** when generating or modifying `.docx` files.

---

## Python Environment

- **Interpreter:** Python 3.13.5 — always invoke with `py` (not `python`)
- **Virtual environment:** `.venv/` in workspace root
- **Key library:** `python-docx` (installed)
- **Activate venv:** `source .venv/Scripts/activate` (Git Bash) or `.venv\Scripts\activate` (CMD)

When writing `.py` scripts that generate docx files, always import from `docx` and apply the format spec above to every paragraph.

---

## Academic Writing Rules (Adviser Requirements)

These rules are non-negotiable for all RRL (Review of Related Literature) content:

1. **Date range:** All cited literature must be from **2021 to 2026** only. Reject any source outside this range.
2. **DOI required:** Every reference must have a verified, working DOI. Do not fabricate or guess DOIs.
3. **Source types:** Must include both **Philippine (local)** and **foreign** sources per section.
4. **No placeholder citations:** Never write `(Author, Year)` — all in-text citations must be real authors and real years.
5. **APA 7th edition:** All in-text citations and reference list entries must follow APA 7th edition format.
6. **Verified sources only:** Before using any reference, confirm it exists via DOI, Semantic Scholar, or a reliable academic database.

---

## Thesis Objectives (5 Core Modules)

When writing RRL sections, each section must align with one of these objectives:

| Obj. | Module | RRL Theme |
|------|--------|-----------|
| 1.1 | Centralized Digital Library | Digital resource management, e-learning repositories |
| 1.2 | AI-Powered Quiz Generator | Automated question generation, NLP in education |
| 1.3 | Automated Grading Module with Customizable Rubrics | AI grading, automated assessment, rubric-based evaluation |
| 1.4 | Mastery-Lock System | Mastery learning, competency-based progression |
| 1.5 | Student Performance Dashboard | Learning analytics, educational data visualization |

---

## Confirmed References (Already Used in v3)

Do not duplicate these in new versions. These are verified and cited in `cha1&2_v3.docx`:

| Author(s) | Year | Topic | DOI |
|-----------|------|-------|-----|
| Alamoudi et al. | 2025 | AI-based assessment | 10.48084/etasr.10662 |
| Bradley | 2021 | E-learning design | 10.46328/ijte.36 |
| Bulathwela et al. | 2023 | AI in education | 10.1007/s40593-023-00374-x |
| de Vreugd et al. | 2024 | Learning analytics dashboard | 10.18608/jla.2024.8529 |
| García-Varela et al. | 2025 | Automated essay scoring | 10.3390/educsci15080946 |
| Kaliisa et al. | 2024 | Learning analytics dashboards | 10.1145/3636555.3636884 |
| Persky & Hughes | 2022 | Assessment in education | 10.5688/ajpe8906 |
| Ramesh & Sanampudi | 2022 | Automated essay grading | 10.1007/s10462-021-10068-2 |
| Susnjak et al. | 2022 | Learning analytics | 10.1186/s41239-021-00313-7 |
| Bustillo & Aguilos | 2022 | Philippine digital education (modular learning, COVID divide) | 10.3390/educsci12070449 |
| Balase & Paglinawan | 2025 | Philippine LMS integration (DepEd LMS teacher narratives) | 10.37502/ijsmr.2025.81011 |
| Colegado | 2025 | Philippine K-12 digital science tools scoping review | 10.47772/IJRISS.2025.903SEDU0479 |

> ⚠️ **Colegado (2025) Warning:** This paper is real, but **it was misrepresented in v3**. The actual paper is a scoping review of digital science teaching tools in Philippine K-12 — it does NOT say "absence of integrated automated evaluation features aligned with local curriculum requirements." When writing v5+, either cite it accurately per its actual findings, or replace it with a more appropriate source.

### New Candidates (Not Yet in Document — Add to v5+)

| Author(s) | Year | Section | Topic | DOI |
|-----------|------|---------|-------|-----|
| Jumao-as et al. | 2025 | 1.4 Mastery-Lock | Reading remediation & mastery learning, Philippine DepEd elementary school | 10.9734/ajess/2025/v51i62000 |
| Gajardo & Balahadia | 2025 | 1.5 Dashboard | Data-driven assessment web portal with performance dashboards, Philippines senior high school | 10.53378/ijstem.353233 |

---

## Fabricated References — NEVER USE

These were identified as hallucinated/invalid in a prior AI session. Never suggest or use these:

- **Tian et al. (2025) arXiv:2506.07955** — fabricated (arXiv ID 2506 = June 2026, a future date)
- **Gagnon (2023) doi:10.1080/00094056.2023.2252447** — returns HTTP 404
- **"Yang et al. (2025)"** — wrong attribution; correct authors are García-Varela et al.
- **Colegado (2025) as cited in v3** — the paper is real (DOI: 10.47772/IJRISS.2025.903SEDU0479) but the v3 characterization of its findings is inaccurate. Do not repeat the misrepresented claim about "absence of automated evaluation features." Cite the paper only for what it actually says: barriers to digital science instruction in Philippine K-12 schools (infrastructure gaps, limited teacher preparation, LMS used mainly in urban schools).

---

## Friend's Capstone Reference Paper — A.T.L.A.S.

**File:** `papers/ATLAS/Curio_Gilera_Gromea_ATLAS_Chap1-2.pdf`
**Authors:** Josh Nathan I. Curio, Rowena G. Gilera, Nehje John S. Gromea
**Title:** A.T.L.A.S. (Automated Timetabling and Locations Allocation System): A Web-Based Academic Scheduling Application
**Institution:** CHMSU — same school, same adviser (same formatting rules apply)

Use this file for **reference and comparison only**. Do not cite it in A.I.M.S. chapters as an academic source.

### Format Comparison: A.I.M.S. vs A.T.L.A.S.

Both papers are from the same institution and adviser, so they must follow identical formatting rules.

| Property | Required | A.I.M.S. v3 Status | A.T.L.A.S. Status |
|----------|----------|---------------------|-------------------|
| Font | Times New Roman 12pt | ✅ Correct | ✅ Correct |
| Line spacing | Double (2.0) | ✅ Correct | ✅ Correct |
| Space after paragraph | 0pt | ✅ Correct | ✅ Appears correct |
| First-line indent (body) | 0.5 inch | ✅ Correct | ✅ Correct |
| Alignment (body) | JUSTIFY | ✅ Correct | ✅ Correct |
| Alignment (headings) | CENTER | ✅ Correct | ✅ Correct |
| Margins | T:1" B:1" L:1.5" R:1" | Verify in .docx | Verify in .docx |

**Key observation from A.T.L.A.S.:** Their Chapter 2 uses bold, left-aligned subheadings (not centered) for RRL section titles (e.g., "Visual Interactive Interfaces and Drag-and-Drop Functionality in Scheduling"). Verify with adviser whether A.I.M.S. Chapter 2 section headings should follow the same pattern.

**Table formatting:** A.T.L.A.S. uses a landscape-oriented RRL matrix table (Table 1) with rotated column headers. If A.I.M.S. requires a similar matrix table, match the same structure with rotated headers.

---

## MCP Tools Available

The following MCP servers are configured in `.vscode/mcp.json`:

- **Semantic Scholar** (`@xbghc/semanticscholar-mcp`): Search 200M+ academic papers — use this to find and verify references with DOIs before adding them to the document.
- **Scholar Sidekick** (`scholar-sidekick-mcp`): Given a DOI, returns a perfectly formatted APA 7th edition citation.

When asked to find new literature:
1. Use Semantic Scholar to search by topic and filter by year (2021–2026)
2. Verify the DOI resolves before including the reference
3. Use Scholar Sidekick to format the final citation in APA 7th edition

---

## Tone and Writing Style

- Academic, formal, third-person voice
- No contractions, no casual language
- Each RRL paragraph must end with or contain a proper in-text citation e.g. `(Bradley, 2021)`
- Introduction sentences should connect to the A.I.M.S. system and its specific module
- Synthesis statements should relate the literature back to the study's objectives

---

## Final Verification Checklist

Before delivering any new `.docx` version, perform a final check to confirm:

1. **All chapters present** — The output file contains every chapter (Chapter 1 and Chapter 2), not just the one that was edited.
2. **Formatting correct** — Font is Times New Roman 12pt, double-spaced, 0pt space after, 0.5" first-line indent, justified body, centered headings.
3. **Margins correct** — Top 1", Bottom 1", Left 1.5", Right 1".
4. **No placeholder text** — No `[insert citation]`, `(Author, Year)`, or `TODO` markers remain anywhere in the document.
5. **All citations are real** — Every in-text citation matches a verified reference with a working DOI.
6. **Date range respected** — All cited sources are from 2021–2026.
7. **Both local and foreign sources** — Each RRL section includes Philippine and international references.
8. **Reference list matches** — Every in-text citation has a corresponding entry in the reference list, and vice versa.
9. **No content lost** — Chapters or sections from the previous version were not accidentally removed or truncated.
10. **File saved to correct location** — New version is in `papers/AIMS/revisions/` with the correct version number.

If any check fails, fix it before delivering the file.

---

## What NOT to Do

- Do not modify `cha1&2.docx` (original)
- Do not use any citation outside 2021–2026
- Do not suggest references without verified DOIs
- Do not leave placeholder text like `[insert citation]` or `(Author, Year)` in any document
- Do not reformat existing paragraphs unless explicitly asked
- Do not add new sections or objectives not in the 5-module structure above
- Do not output a file that contains only one chapter when the previous version had multiple chapters

---
name: study-guide
description: Write an intuition-first study guide (black-and-white academic PDF, diagrams, depth tags, review questions, interview corner) for a hands-on project, so the learner understands why things work. Use when the user asks for a study guide, learning material, or "help me understand" a project they are building.
---

# Study Guide

Write a study guide for the user's project. The goal is **understanding and intuition**, not build steps. The reader is hands-on with the project and wants to know *why* things work, not only *what to type*.

## 1. Ask first (before writing anything)

Ask these in one short message and wait for the answers:

1. **Project / topic**, and what the user has built or learned so far (ask for file or folder paths if they exist).
2. **Level** on the main topics (new, some experience, comfortable).
3. **Goal**: what they want to use this understanding for (a job role, a course, an interview, a thesis). This shapes the interview corner.
4. **Reference file?** Ask exactly: "Do you want to give me a reference file (book, paper, datasheet, notes)? yes / no". If no, use only the project itself and well-known sources. If yes, ask for the path (and which chapters or sections matter, if known). If the file is a scanned PDF, say that it has to be read page by page as images, which is slower. Use the reference as the main source for the topics it covers, and state in the guide which parts came from it and which pages you actually read.
5. **Output folder.**
6. **Flashcards?** Ask exactly: "Do you want the review questions exported as flashcards? yes / no". Do nothing about flashcards until they answer. If no, skip section 5 completely.

## 2. Style rules

- **Simple language.** Short sentences. Explain every term the first time it appears.
- **Intuition before formulas.** For each idea: a plain picture or analogy first, then the precise version, then a worked example with numbers.
- **"Engineering intuition" boxes.** At least one per major topic: the analogy that makes the idea feel obvious.
- **Diagrams** wherever a picture teaches faster than words (block diagrams, timing diagrams, flows, plots).
- **Black and white, academic paper look.** Serif text, numbered headings, captioned figures and tables, grayscale only.
- **Honest labels.** Mark numbers that are estimates ("to be measured"). Never state a number you did not verify or derive. If you did not read a source page, do not cite it.
- **No build steps** unless the user asks. Explain concepts, not procedures.

## 3. Structure

1. Title and short abstract
2. "How to read this guide" (including the depth-tag legend, section 4)
3. Chapters, from fundamentals toward the project. Each chapter has:
   - the explanation (intuition boxes, figures, worked examples)
   - depth tags (section 4)
   - **Interview corner** (section 6)
   - **Review questions** (5 to 8, a mix of concept and calculation)
4. A concept map: what depends on what
5. Glossary
6. Answer key (review questions and interview questions)
7. Reading list (real, checkable sources only)

## 4. Depth tags (every section gets one)

Put a tag right under each section heading and explain the tags once in "How to read":

| Tag | Meaning |
|---|---|
| **[Core]** | Must understand to follow the project. Read first. |
| **[Good to know]** | Makes you faster and less surprised. Read on the second pass. |
| **[Deep dive]** | Extra depth for curiosity or interviews. Safe to skip at first. |

Rules: every section has exactly one tag, every chapter has at least one [Core] section, and "How to read" gives a first-pass path that uses only the [Core] sections.

## 5. Flashcards (only if the user said yes)

- One card per review question, per interview question, and per glossary term.
- Export `flashcards.csv` with columns `front,back,tag,chapter` (tag = the depth tag), plus the same data as `flashcards.json`. These import into Anki and most flashcard apps.
- If the user names a specific app, check what import format it accepts and adapt the files. Say which format you used.
- Keep each card short and self-contained: it must make sense without the chapter next to it.

## 6. Interview corner (every chapter)

2 to 4 questions per chapter, written the way an interviewer for the user's stated goal would ask them:

- one "explain it simply" question (explain the idea to a non-expert in one minute)
- one "why did you choose this" question about a design decision in the user's project
- one "what would break if..." question
- optionally one "how would you do it differently at real scale"

In the answer key give a short model answer for each, plus 3 or 4 bullet points on what a strong answer must contain.

## 7. Suggested toolchain

Use whatever the user already has. A combination that works well:

- **PDF:** Typst (`typst compile guide.typ`). LaTeX or Pandoc also work. Make the intro heading unnumbered so chapter numbers match the text.
- **Figures:** matplotlib to SVG in a `figs/` folder, with small helpers (box, arrow, text). Serif font, grayscale only. Avoid unicode arrows in matplotlib text; use mathtext.
- **Checking the result:** do not trust a build that you have not looked at. Render pages to PNG (for example `typst compile --ppi 60 guide.typ "pg/p{0p}.png"`), build contact sheets with Pillow, and look at them. Check for overlapping labels, clipped text and wrong cross-references.
- **Scanned books (no text layer):** if no OCR is available, render pages to PNG with PyMuPDF and read them as images. Find the offset between printed page numbers and PDF page index first.
- **Typst gotchas:** quote words in math (`"NM"_H`, `V_("DD")`); avoid `*`, `_`, `@`, `$` in plain text; a `<` followed by a word can be read as a label.
- **Scripts with backslashes:** write such files with a file-writing tool rather than a shell heredoc, because escape sequences can get mangled.
- Keep scratch files out of the project folder and delete leftovers at the end.

## 8. Quality checks before saying "done"

- The document compiles with no errors, and you have actually looked at the rendered pages.
- Every worked example and every answer-key number was recomputed.
- Every cross-reference (chapter numbers, figure mentions) is correct.
- Depth tags are on all sections, and every chapter has an interview corner.
- The final message is short: where the files are, what is inside, and anything uncertain.

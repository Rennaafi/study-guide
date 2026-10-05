# study-guide

An agent skill that writes a **study guide for the project you are building**, so you understand *why* things work, not only *what to type*.

It produces a black-and-white, academic-paper-style PDF with plain-language explanations, diagrams, worked examples, review questions with an answer key, and interview questions.

## Why

Building a project by following steps teaches you the steps. Understanding comes from intuition: the picture in your head that lets you predict what will happen before you press run. This skill makes the agent explain things in that order: **intuition first, then the precise version, then a worked example.**

## What you get

- A PDF study guide: abstract, how-to-read, chapters, concept map, glossary, answer key, reading list
- **Depth tags** on every section so you can read in passes:
  - `[Core]`: must understand to follow the project
  - `[Good to know]`: makes you faster and less surprised
  - `[Deep dive]`: curiosity and interview depth
- **Engineering intuition** boxes: the analogy that makes an idea obvious
- **Review questions** (concept and calculation) with answers
- **Interview corner** in every chapter, aimed at the goal you state
- Optional **flashcards** (CSV and JSON, Anki-friendly)

## How it works

The skill starts by asking you a few questions, then writes the guide:

1. What is the project and what have you built so far?
2. What is your level?
3. What is your goal? (a job, a course, an interview, a thesis)
4. **Reference file?** yes / no. If yes, you give a path (book, paper, datasheet, notes) and the guide is grounded in it. Scanned PDFs are read page by page as images.
5. Where should the output go?
6. **Flashcards?** yes / no. Nothing is exported unless you say yes.

## Install

**Claude Code (as a skill):**

```bash
mkdir -p ~/.claude/skills/study-guide
cp SKILL.md ~/.claude/skills/study-guide/SKILL.md
```

Then ask: "Make a study guide for my project." (or invoke `/study-guide`).

**Any other agent or chat tool:** paste the contents of `SKILL.md` (or point the agent at the file) and say: "Make a study guide for my project using these instructions."

## Requirements

None for the instructions themselves. The suggested toolchain is [Typst](https://typst.app) for the PDF and Python with matplotlib and Pillow for figures and page checks, but the skill tells the agent to use what you already have installed.

## Design choices

- **Understanding over procedure.** The guide has no build steps unless you ask.
- **Honest numbers.** Estimates are labelled as estimates, and sources the agent did not read are not cited.
- **Looks checked.** The agent must render and look at the pages before saying it is done.
- **Small and editable.** One markdown file. Change the style rules to fit how you like to learn.

## License

MIT, see [LICENSE](LICENSE).

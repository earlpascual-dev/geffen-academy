# Geffen Academy

A self-contained study platform for Generative AI — documentation, practice quizzes, and a timed, Mettl-style certification exam — in a single `index.html` file. No build step, no backend, no auth.

Styled after Ragnarok Online's Geffen town: purple towers, green fields, gold trim, parchment panels.

## Features

- **Study (Archives)** — 9 topics covering generative AI fundamentals: what generative AI is, LLMs, embeddings & semantic search, prompt engineering, diffusion models, AI agents & multimodal models, practical usage tips, ethics/limitations, and privacy & security.
- **Practice Test** — pick a topic (or all) and a question count, get instant per-question feedback with explanations, then a scored review. Not saved to history.
- **Certification Exam** — a timed (45-minute), 54-question assessment that mimics an online proctored exam: a pre-exam rules/agreement screen, a countdown timer, a question navigator (answered / visited / marked for review), Save & Next / Mark for Review / Clear Response controls, tab-switch detection logged as an "integrity flag," a submit confirmation modal, and a full report (score, pass/fail, per-topic breakdown, detailed answer review). Attempts are saved to `localStorage` and shown on the home dashboard.

All 28+ questions and all documentation content are original, written to explain foundational generative AI concepts — not sourced from any specific test bank or real assessment.

## Running it

Just open `index.html` in a browser, or serve the directory:

```bash
npx http-server . -p 8124
```

## Architecture

- `DOCS` and `QUESTIONS` hold all content for the `genai` subject. Adding a new subject means adding a matching key to both, plus `SUBJECT_META` and `TOPIC_LABELS` — the rest of the UI (study nav, practice setup, exam) is subject-agnostic.
- A single `state` object drives a manual view-dispatch `render()` — no framework. Clicks are handled by one delegated listener keyed on `data-action` attributes.
- `prepareQuestions()` shuffles both question order and each question's option order (remapping the correct-answer index) so practice/exam runs never repeat the same arrangement.
- Exam attempts (score, percent, date, duration) persist to `localStorage` under `geffen_study_exam_history`.

## Extending

Three "Coming Soon" subject placeholders (Data Structures & Algorithms, Cloud Computing, Cybersecurity Fundamentals) are shown on the home screen to hint at where this can grow — add a real subject the same way `genai` is defined.

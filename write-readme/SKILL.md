---
name: write-readme
description: Generate a structured, audience-aware README.md for any project. Use when the user wants to create or generate a README for their project.
---

# write-readme

Generate a structured, audience-aware README.md for any project.

## When to Use This Skill

Invoke `/write-readme` when you want to generate a README.md for a project. Run it from the project's root directory.

## Protocol

Follow every step in order. Do not skip steps. Do not ask multiple questions in one message.

---

### Step 1 — Scan the codebase (automatic, no prompts)

Read the following files if they exist, in this priority order:

| Priority | File | What to extract |
|---|---|---|
| 1 | `package.json` | name, scripts, dependencies, devDependencies |
| 2 | `requirements.txt` / `pyproject.toml` | Python dependencies |
| 3 | `Cargo.toml` | Rust dependencies |
| 4 | `go.mod` | Go dependencies |
| 5 | `Dockerfile` | runtime, base image |
| 6 | `Makefile` | build/run targets |
| 7 | `index.js`, `main.py`, `main.rs`, `app.py`, `index.ts`, `main.go` | exports, CLI commands, API routes, component names |
| 8 | `README.md` (existing) | any existing content to preserve or reference |

**If none of the above files exist**, ask:
> "I couldn't find any config files. What language/framework is this project using?"

---

### Step 2 — Ask: audience (always ask this first, before any other question)

> "Is this a: (A) Portfolio project, (B) Open source library, or (C) Internal/team project?"

Store the answer. Use it in Step 5 (tone matrix).

---

### Step 3 — Section inference rules

For each section, use this table to decide whether to infer or ask:

| Section | Strategy | Fallback if unanswered |
|---|---|---|
| Title | Infer from `name` in package.json or current folder name | Ask |
| Technologies | Infer from dependency files | Ask: "What technologies does this use?" |
| Features | Infer from exports, routes, CLI commands, component names | Ask: "List the main features" |
| Uses | Cannot infer — ask | Write `_Coming soon._` if user skips |
| Process | Cannot infer — ask | Write `_Coming soon._` if user skips |
| Learnings | Cannot infer — ask | Write `_Coming soon._` if user skips |
| How can it be improved? | Cannot infer — ask | Write `_Coming soon._` if user skips |
| Running the project | Infer from scripts/Makefile/Dockerfile. Priority: Docker > npm/yarn > make > direct command | Ask if nothing found |
| Video | Cannot infer — ask | Omit section entirely if user says skip |

---

### Step 4 — Ask questions sequentially (one at a time, never in bulk)

Ask only what could not be inferred in Step 3. Use this exact order and wording:

1. "What is this project used for? Who uses it?"
2. "Briefly describe how you built it — decisions, approach, tools."
3. "What did you learn building this?"
4. "Any known limitations or ideas for future improvement?"
5. "Do you have a demo video? Enter the URL or type 'skip'."
   - If URL given → ask: "Should I show it as a (A) plain link or (B) clickable thumbnail?"

**Never ask about something already extracted from code.**
**Never ask two questions in the same message.**

---

### Step 5 — Apply tone per audience

Use the audience answer from Step 2 to adjust the framing of each section:

| Section | Portfolio (A) | Open Source (B) | Internal (C) |
|---|---|---|---|
| Features | Benefit-first — what it does *for the user* | API surface + capabilities — technical precision | Workflow-focused — what the team gains |
| Uses | Who would hire someone with this skill | Who would import or use this package | Which team or system depends on this |
| Process | Story-driven, shows growth and decisions | Technical rationale + architecture decisions | Implementation approach + constraints |
| Learnings | Personal growth + skills gained | Technical insights useful for contributors | Lessons for the team, what to do differently |
| How can it be improved? | Honest reflection, shows self-awareness | Roadmap + contribution opportunities | Known limitations + next sprint priorities |

---

### Step 6 — Technologies format

Render each technology as a shield.io badge, one per line:

```markdown
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
```

Use the correct shield.io badge for each detected technology. If unsure of the exact badge URL, use:
`https://img.shields.io/badge/{{Name}}-grey?style=for-the-badge`

---

### Step 7 — Video section format

**Plain link:**
```markdown
## Video
[Watch the demo](URL)
```

**Clickable thumbnail — YouTube URL:**
Extract VIDEO_ID from the YouTube URL (`v=` parameter or path after `youtu.be/`).
```markdown
## Video
[![Demo Video](https://img.youtube.com/vi/VIDEO_ID/0.jpg)](URL)
```

**Clickable thumbnail — non-YouTube URL:**
```markdown
## Video
[![Demo Video](https://img.shields.io/badge/Watch-Demo-red?style=for-the-badge&logo=youtube)](URL)
```

**Skipped:** Do not write the Video section at all. No placeholder. No `_Coming soon._`

---

### Step 8 — Write README.md

Write the file using this exact template. Fill every `{{placeholder}}`. Do not leave any placeholder unfilled. Do not change section names or order.

```markdown
# {{TITLE}}

## Technologies
{{TECHNOLOGIES: one shield.io badge per line, see Step 6}}

## Features
{{FEATURES: bullet list, 3-7 items, tone adjusted per Step 5}}

## Uses
{{USES: 2-3 sentences, tone adjusted per Step 5}}

## Process
{{PROCESS: 2-4 sentences, tone adjusted per Step 5}}

## Learnings
{{LEARNINGS: bullet list or short paragraph, tone adjusted per Step 5}}

## How can it be improved?
{{IMPROVEMENTS: bullet list, 2-5 items, tone adjusted per Step 5}}

## Running the project
{{RUNNING: fenced code blocks with commands, up to 3 run methods in priority order}}

## Video
{{VIDEO: apply format from Step 7, or omit this section entirely if skipped}}
```

**Rules:**
- If a section has no answer and no inferred content → write `_Coming soon._`
- Never omit a section except Video (only when user explicitly said skip)
- Never invent features, tools, or behavior not present in the actual code

---

### Step 9 — Confirm

After writing README.md, say:

> "README.md written. Review it and let me know if you want any changes — or run /publish-readme when you're ready to push to GitHub."

---

## Anti-patterns

- Do not invent features not present in the code
- Do not skip sections (except Video when user says skip)
- Do not ask multiple questions in one message
- Do not ask for something already extracted from code

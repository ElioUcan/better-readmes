# better-readmes

[![skills.sh](https://skills.sh/b/ElioUcan/better-readmes)](https://skills.sh/ElioUcan/better-readmes)

## 🛠️ Technologies
![Claude Code](https://img.shields.io/badge/Claude_Code-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![GitHub CLI](https://img.shields.io/badge/GitHub_CLI-181717?style=for-the-badge&logo=github&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)

## ✨ Features

- **`/write-readme`** — scans your codebase, then asks only what it can't infer to generate a structured README.
- **Audience-aware tone** — adapts every section's framing for Academic, Business, or Personal/open-source projects.
- **Optional sections** — choose upfront which sections to skip; skipped ones are omitted cleanly with no placeholders.
- **Optional emojis** — turn emoji section headers on or off with a single prompt.
- **Hero image + video** — add a banner image at the top and a demo video (plain link or clickable thumbnail).
- **Shield.io badges** — renders detected technologies as `for-the-badge` shields automatically.
- **`/publish-readme`** — pushes the README to GitHub, creating the repo if needed and setting the About description and topics via the GitHub CLI.

## 🎯 Uses

For developers who want better README structure and GitHub publication without the manual effort — while keeping full control over what the project describes. You answer a few targeted questions, review the result, and decide when it's published; the skills handle the structure, badges, and repo metadata so you don't have to.

## 🔧 Process

Built as two Claude Code skills, each defined by a strict step-by-step Markdown protocol that the model follows in order. The design is inference-first: `/write-readme` scans config and entry-point files to fill in everything it can before asking the user, and only prompts one question at a time for what genuinely can't be inferred. `/publish-readme` is structured as a guarded pipeline — prerequisite checks, remote detection, then metadata generation — so it stops with clear instructions rather than failing midway.

## ▶️ Running the project

Install the skills from the [skills.sh](https://skills.sh/ElioUcan/better-readmes) registry:

```bash
npx skills add ElioUcan/better-readmes@write-readme
npx skills add ElioUcan/better-readmes@publish-readme
```

**Step 1 — Generate the README.** From your project directory, run:

```
/write-readme
```

**Step 2 — Publish to GitHub.** When you're happy with the README, run:

```
/publish-readme
```

> `/publish-readme` requires the [GitHub CLI](https://cli.github.com) installed and authenticated (`gh auth login`).

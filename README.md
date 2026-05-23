# better-readmes

Two Claude Code skills that generate structured, audience-aware README files and publish them to GitHub automatically.

## Skills

### `/write-readme`
Scans your codebase, asks only what it can't infer, and generates a structured README with these sections: Title, Technologies (shield.io badges), Features, Uses, Process, Learnings, How can it be improved?, Running the project, Video.

### `/publish-readme`
Takes your README.md and pushes it to GitHub — creating the repo if needed, setting the About description, and tagging topics automatically using the GitHub CLI.

## Install

```bash
npx skills add ElioUcan/better-readmes@write-readme
npx skills add ElioUcan/better-readmes@publish-readme
```

## Usage

**Step 1 — Generate the README:**
Navigate to your project directory and run:
```
/write-readme
```

**Step 2 — Publish to GitHub:**
When happy with the README, run:
```
/publish-readme
```

## Requirements for `/publish-readme`

- [GitHub CLI](https://cli.github.com) installed and authenticated (`gh auth login`)

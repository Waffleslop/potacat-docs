# docs.potacat.com — agent instructions

Read the workspace file first: `../AGENTS.md` (until the folder move it lives at
`D:\Projects\potacat\AGENTS.md`). This is the POTACAT Users Guide, an mdBook (book.toml; pages in
src/, navigation in src/SUMMARY.md). Public repo.

## Build and deploy
`mdbook build` (CI); `mdbook serve` locally if mdbook is installed. Push to main deploys to GitHub
Pages at docs.potacat.com (CNAME). Push only when Casey says; work on a branch
(`docs-<issue>-<slug>`) and open a PR.

## Rules
- Every feature page is written from a DESKTOP_TO_DOCS handoff or the release notes, never from memory;
  radio menu paths are quoted from the handoff or the manual.
- changelog.md follows the desktop release notes one to one.
- Explainers that should rank on Google belong on potacat.com (the website repo), linked both ways;
  the guide stays a reference. No refund language. No emoji.
- .discord-scrape/ holds the Discord export scripts; its output is not committed.

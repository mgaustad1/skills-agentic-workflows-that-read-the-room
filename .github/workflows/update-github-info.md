---
name: update-github-info
description: Propose concise, source-backed updates to Mona's GitHub Info page.
intent: Keep Mona's GitHub Info page current with practical, source-backed guidance that helps developers learn GitHub.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
engine:
  id: copilot
  copilot-sdk: true
safe-outputs:
  create-pull-request:
    title-prefix: "[GitHub Info] "
    reviewers:
      - mona
    draft: false
    allowed-files:
      - site/content/github-info.md
  noop:
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before
making any changes. Web-fetch both `https://github.blog/latest/` and
`https://github.blog/changelog/` for current, official source material.

Update only `site/content/github-info.md`. Add or revise content only when the
sources support a useful, practical update for GitHub developers. Keep summaries
short and include a direct source link for every change based on the GitHub Blog
or Changelog. Preserve Mona's editorial angle and existing page structure.

Use the edit tool for the file change, then propose it with the configured
`create-pull-request` safe output so Mona can review it; never write directly to
the default branch or use another write path. If neither source has a relevant
update, no meaningful edit is warranted, or the source evidence is unavailable,
make no changes and call `noop` with a brief reason.

---
name: update-github-info
description: Refresh the GitHub Info page with practical updates from official GitHub sources.
intent: Review current official GitHub news and propose a concise, sourced update to the GitHub Info page for Mona's review.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
strict: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  web-fetch:
  edit:
safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` before making any decisions about the content or tone.

Use web-fetch to read all three official sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Use the GitHub repository API tools for repository guidance and reference files; do not use terminal, CLI, or sandboxed commands for that repository reading.

Update only `site/content/github-info.md` with short, practical information that helps developers learn GitHub faster. Keep the existing editorial angle, cite the relevant GitHub Blog or GitHub Changelog source for every new item, and preserve useful existing content. Inspect the current file before editing it.

When there is a meaningful, well-supported update, use the configured `create-pull-request` safe output to propose the change for Mona to review. Give the pull request a clear title and explain the sources and edits in its body. Do not write directly to the default branch.

Call `noop` with a short reason when the sources do not contain a meaningful update, the evidence is insufficient, or the proposed content would only duplicate the current page.
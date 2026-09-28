---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical updates from official GitHub sources.
model: copilot/gpt-4.1
on:
  workflow_dispatch:
  schedule: daily

permissions:
  contents: read
  pull-requests: read

tools:
  edit:
  web-fetch:

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` before making any changes. Use Mona's notes as editorial guidance, and preserve the page's existing focus on practical GitHub guidance.

Fetch all three sources using only the `web-fetch` tool. Do not use shell commands,
`curl`, `wget`, or another tool to retrieve these URLs. If `web-fetch` cannot
retrieve a source, report the failed URL and do not try another retrieval method.

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Review recent items and select only updates that are useful to developers learning GitHub. Verify every factual claim against the fetched source. Keep summaries short and practical, and include a direct source link for each update. Do not invent details, repeat stale items, or rewrite unrelated page content.

Edit only `site/content/github-info.md`. If there is no worthwhile update, leave the file unchanged and do not open a pull request. Otherwise, prepare a concise draft pull request for Mona to review through the configured `create-pull-request` safe output. Summarize the page changes and cite the official source URLs in the pull request description. Never write directly to the default branch or merge the pull request.
---
name: update-github-info
description: Keep the GitHub Info content current with practical, sourced updates from the GitHub Blog and Changelog.
intent: Update the GitHub Info page with useful official GitHub updates and propose the changes for Mona's review.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before making any changes.

Use web-fetch to read both official sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Identify recent updates that are both new to the current page and useful to developers learning GitHub. Keep additions short and practical, preserve the page's existing editorial direction, and cite the relevant GitHub Blog or Changelog source with each update. Do not add claims that the sources do not support.

Edit only `site/content/github-info.md`. If either source cannot be fetched, or if there is no distinct, useful update to add, leave the file unchanged and call `noop` with a short reason.

When you make a substantive update, use the configured `create-pull-request` safe output to open a non-draft pull request for Mona to review. Include a concise summary and links to the sources in the pull request description. Do not merge the pull request or write directly to the default branch.
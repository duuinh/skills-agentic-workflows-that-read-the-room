---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
   workflow_dispatch: null
   schedule:
      - cron: '17 9 * * *'
safe-outputs:
   create-pull-request:
      title-prefix: "[mona] "
      draft: true
      fallback-as-issue: false
tools:
   edit: {}
   web-fetch: {}
network:
   allowed:
      - github.com
      - github.blog
      - awesome-copilot.github.com
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making changes.

Use these sources:
- `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
 - GitHub Changelog: https://github.blog/changelog/
 - Awesome Copilot Workflows: https://awesome-copilot.github.com/workflows/

Web-fetch instruction:

- Web fetch https://awesome-copilot.github.com/workflows/ and include any relevant workflow listings or summaries as additional sources; when using content from that page, cite it in the updates.

Update `site/content/github-info.md` with concise,
practical updates for readers and include source context when content comes
from the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review. 
Use a pull request title that mentions Mona or GitHub Info. 
Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`.

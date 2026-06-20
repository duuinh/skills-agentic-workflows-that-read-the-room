---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
  workflow_dispatch: {}
  schedule:
    - cron: "17 6 * * *"
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github
steps:
  - name: Prepare data files
    run: |
      mkdir -p /tmp/gh-aw/data
      cp notes/mona-notes.md /tmp/gh-aw/data/mona-notes.md || true
      curl -fsSL https://github.blog/latest/ -o /tmp/gh-aw/data/github-latest.html || true
      curl -fsSL https://github.blog/changelog/ -o /tmp/gh-aw/data/github-changelog.html || true

---

# Update GitHub Info

## Task

Read the following inputs and update `site/content/github-info.md` with any relevant, concise updates suitable for the website. Prepare changes as a draft and open a pull request for Mona to review — do not push directly to `main`.

Inputs (already saved to `/tmp/gh-aw/data/` by `steps:`):
- notes/mona-notes.md (local repo file)
- https://github.blog/latest/ (saved as `/tmp/gh-aw/data/github-latest.html`)
- https://github.blog/changelog/ (saved as `/tmp/gh-aw/data/github-changelog.html`)

Processing instructions for the agent:

- Read `/tmp/gh-aw/data/mona-notes.md` to learn Mona's intent and any hand-authored copy or links.
- Scrape the GitHub Blog latest page and the Changelog page saved above; extract only short, user-facing highlights that are directly relevant to Mona's audience.
- Update `site/content/github-info.md` with a clear summary section that includes:
  - short headline (one line)
  - 1–3 bullet highlights
  - links to source posts (where applicable)
- Keep tone consistent with the site's style and keep edits minimal and reviewable.
- If no substantive changes are found, call `noop` with a one-line reason.

Safe outputs
- Use the configured `create-pull-request` safe-output to create a PR with the proposed edits. The PR should:
  - have a short descriptive title like "chore(site): update GitHub info from blog & notes"
  - include a short body describing sources used: `notes/mona-notes.md`, `github.blog/latest`, `github.blog/changelog`
  - target branch: `main` (use the default PR branch naming the agent runtime provides)

## Notes

- This file is the agentic workflow definition — do not compile it here. The repository maintainer will run `gh aw compile` when ready.

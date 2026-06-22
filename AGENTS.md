## Learned User Preferences

- Profile README should mirror t3dotgg structure: one-line identity, "Checkout my …" links, `## Current Projects` with `### Products` and `### Everything Else`, then automated GitHub activity below.
- Curated intro and project copy belong in `README.md.tpl`; iterate there and let readme-scribe regenerate `README.md`.
- Surface website (tushar-6666.vercel.app), blog (tushard.bearblog.dev), and Twitter (x.com/tusharhq) in the intro; keep other personal links on the website when possible.
- Use Jujutsu (`jj`) for version control in this repo, not `git commit`.
- Start new work from fetched GitHub main (`jj git fetch`, then `jj new main@origin` or rebase onto `main@origin`).
- Resolve conflicted `main??` by aligning local `main` with GitHub: `jj git fetch && jj bookmark set main -r main@origin`.
- Land changes on protected `main` via a feature bookmark and GitHub PR (`jj git push --bookmark <name>`), not a direct push to `main`.
- When the user says "do it", run the full workflow (commit, rebase, push or open PR) instead of stopping at instructions.

## Learned Workspace Facts

- `tusharhqq` is the GitHub profile README repo; it uses jj with Git colocation and the user’s jj config sets `trunk()` to `main@origin`.
- `.github/workflows/readme-scribe.yml` runs markscribe (`README.md.tpl` → `README.md`) on `main` push, hourly cron, and `workflow_dispatch`; it opens squash-merge PRs on `readme-scribe/update`.
- `PERSONAL_GITHUB_TOKEN` is required for markscribe GitHub API access; `GITHUB_TOKEN` is used for PR creation and auto-merge.
- GitHub `main` is branch-protected; direct `jj git push --bookmark main` is rejected without a PR.
- `.gitignore` excludes `.cursor/` so local Cursor hook and state files are not committed.
- The template combines static curated sections with markscribe `recentReleases` and `recentPullRequests` blocks after a `---` separator.
- readme-scribe bot updates land as immutable commits from github-actions[bot] and can advance `main@origin` independently of local template work.

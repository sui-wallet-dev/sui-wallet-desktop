# How to run github-setup.ps1

## Quick start

1. Extract this zip to your Downloads folder (or anywhere — but see "paths with spaces" below).
2. Open Windows PowerShell.
3. Allow scripts for this session only:
   `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Bypass -Force`
4. Change directory into the extracted folder.
5. Edit `github-setup.ps1` in Notepad: set `$GH_USER` to your bare username (e.g. `alice`, NOT `https://github.com/alice`) and `$GH_TOKEN` to your `ghp_...` classic token. The token needs scopes `repo`, `user`, and `delete_repo`.
6. Run: `.\github-setup.ps1`
7. After success, revoke or delete the GitHub token.

## Paths with spaces (common gotcha)

If the folder you extracted to contains a space in its name (for example, "backlinks My Algo"), you MUST wrap the path in double quotes when using `cd`:

  WRONG: cd C:\Users\you\Desktop\backlinks My Algo\sui-wallet-desktop-github-windows-setup
  RIGHT: cd "C:\Users\you\Desktop\backlinks My Algo\sui-wallet-desktop-github-windows-setup"

Without quotes, PowerShell sees "My" and "Algo" as extra arguments to cd and errors out with:
  "A positional parameter cannot be found that accepts argument 'My'."

The simplest workaround is to put the folder somewhere with no spaces in the path, such as ~\Downloads.

## What the script does

1. Cross-checks `$GH_USER` against the token owner via `GET /user`; aborts cleanly if they do not match.
2. Updates your GitHub profile (name = "Sui Wallet Desktop", bio = USP, company = "Wallet Connections LLC", website = https://suiwallet.net/).
3. Creates the output repo (or uses an existing one), with `auto_init=true` so a default branch exists immediately.
4. Polls the new repo until GitHub returns a `default_branch` (avoids the propagation-lag 404s).
5. Sets 12 repository topics derived from the product keyword set.
6. Uploads every file: README.md, LICENSE, HOW-TO-RUN.md, and all 12 articles in `docs/`.
7. Creates / updates your profile README repo with 10-15 sitemap links.
8. Enables GitHub Pages on the `main` branch.
9. Stars the repo.
10. Creates Release v1.0.0.

## If something goes wrong

- **Re-run the script.** It is idempotent: it catches HTTP 422 ("already exists") on repo creation and HTTP 409 / 404 ("file conflict" / "backend not yet propagated") on uploads, so re-runs are safe. If a previous run created the repo with no default branch, the script heals it on the next run.
- **"(400) Bad Request" on repo creation:** the JSON body is malformed. Check that no PowerShell `$true` / `$false` variables were interpolated into the body string.
- **"(401) Unauthorized":** the token is wrong, expired, or missing required scopes (`repo`, `user`, `delete_repo`).
- **"(404) Not Found" on every step after step 2:** `$GH_USER` does not match the token owner. Edit `$GH_USER` to match the username the token was issued for and re-run.
- **"Cannot overwrite variable HOME because it is read-only or constant":** the script has a bug — it is assigning to a PowerShell automatic variable. Report it; do not edit and retry.
- **The script seems to do nothing:** check `Get-ExecutionPolicy` — it should be `Bypass` for the current session.

## After running

- Visit https://github.com/[your-username] to confirm the new repo, profile updates, and release.
- Delete the `github-setup.ps1` file (it contains your token in plain text), or revoke the token at https://github.com/settings/tokens and generate a fresh one if you plan to re-run.

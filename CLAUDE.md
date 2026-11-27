## Git and pull requests
- This repo only allows "Rebase and merge". Never put a merge commit on a PR branch:
  GitHub cannot rebase a branch that contains one, and shows "Merge conflicts".
- Keep PR branches linear: rebase onto the latest main instead of merging main in.
- If a branch's PR has already been merged (the remote branch may be deleted), restart the
  branch from the latest main and cherry-pick only the unmerged commits. Don't re-push old history.
- Before opening or updating a PR, check the diff against main contains only the intended change,
  and grep for conflict markers (<<<<<<<, =======, >>>>>>>).
- You may force-push `claude/*` branches, with --force-with-lease, and only those. Never force-push main.

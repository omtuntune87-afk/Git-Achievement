# Troubleshoot common Git problems

Start with `git status` and read the complete error before changing anything.
Commit or otherwise preserve unrelated work before switching branches or
attempting a recovery. Replace sample paths and branch names with your own.

## A commit reports an unknown author identity

Configure your own name and a verified GitHub email for this repository:

```bash
git config user.name "Your Name"
git config user.email "YOUR_VERIFIED_EMAIL"
```

Use your GitHub-provided no-reply address if you want to keep your email private.
This affects future commits; it does not change existing authorship. Never use
someone else's identity to claim contribution credit.

## A push is rejected as non-fast-forward

Someone may have updated the remote branch. Fetch and inspect both histories:

```bash
git fetch origin
git log --oneline --graph --left-right HEAD...origin/main
```

For a feature branch, compare against its matching remote branch instead of
`origin/main`. With a clean working tree, merge that remote branch into your
local branch, resolve any conflicts, and push again. If your project requires
rebasing instead, follow its documented workflow. Avoid force-pushing a shared
branch to bypass the rejection.

## A merge has conflicts

```bash
git status
git diff --name-only --diff-filter=U
```

Open each conflicted file, choose the intended final content, and remove conflict
markers. Run the relevant checks, stage only the resolved files, then finish:

```bash
git add README.md
git merge --continue
```

To cancel an in-progress merge instead, use `git merge --abort`. Git may be
unable to reconstruct pre-existing uncommitted edits, which is why a clean
working tree matters before starting a merge.

## The wrong file was staged

```bash
git restore --staged README.md
git diff -- README.md
```

This preserves your working copy. In a repository with no first commit yet,
use `git rm --cached -- README.md` to unstage a newly added file instead.

## A published commit introduced a mistake

Find the specific commit with `git log --oneline`, then create a new undo commit:

```bash
git revert COMMIT_SHA
```

Replace `COMMIT_SHA` with the offending ordinary commit. Reverting a merge
requires choosing a mainline parent; ask the maintainer before doing that.
If a normal revert conflicts, resolve and stage the affected files, then run
`git revert --continue`, or use `git revert --abort` to cancel it.

A revert preserves published history. It does not remove leaked credentials
from earlier commits: revoke exposed credentials immediately and coordinate
history cleanup with the repository owner.

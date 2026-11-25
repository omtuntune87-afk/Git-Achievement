# Everyday Git commands

For rejected pushes, conflicts, or mistakes, see the [troubleshooting guide](troubleshooting.md).

Run these commands from inside your repository. Replace example branch names and paths with your own.

## Inspect your work

```bash
git status
git diff
git diff --staged
git log --oneline -5
```

`git diff` shows unstaged changes; `git diff --staged` shows what the next commit will contain.

## Make a focused commit

Start from a clean working tree so unrelated changes stay separate.

```bash
git switch -c docs/improve-guide
# Edit the file before staging it.
git add README.md
git diff --staged
git commit -m "docs: improve setup instructions"
git push -u origin docs/improve-guide
```

Pushing requires write access to the remote. Contributors without access should push to their own fork and open a pull request.

## Update your local main branch

Commit your work before switching branches.

```bash
git switch main
git pull --ff-only origin main
```

If the pull reports diverging branches, stop and inspect the history before choosing a merge or rebase.

## Unstage a file without deleting edits

```bash
git restore --staged README.md
```

This removes the file from the staging area while preserving its working-tree changes.

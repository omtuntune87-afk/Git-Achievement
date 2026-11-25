# Practice a complete Git workflow locally

This exercise uses a new temporary directory and a local bare repository as a
remote. It does not publish anything to GitHub or modify an existing project.
Use Bash or Zsh on macOS or Linux with Git installed.

## Create a practice remote and clone

```bash
practice_dir=$(mktemp -d)
git init --bare "$practice_dir/remote.git"
git clone "$practice_dir/remote.git" "$practice_dir/work"
cd "$practice_dir/work"
git switch --orphan main
```

An empty-repository warning from the clone is expected. If Git cannot determine
your identity, configure your own name and verified email locally before committing:

```bash
git config user.name "Your Name"
git config user.email "YOUR_VERIFIED_EMAIL"
```

Replace both placeholders. These settings apply only to this practice clone.

## Publish an initial commit

```bash
printf '# Practice project\n' > README.md
git add README.md
git commit -m "docs: initialize practice project"
git push -u origin main
```

## Create, inspect, and publish a branch

```bash
git switch -c docs/add-goal
printf '\nGoal: learn a reviewable Git workflow.\n' >> README.md
git diff
git add README.md
git diff --staged
git diff --cached --check
git commit -m "docs: add learning goal"
git push -u origin docs/add-goal
```

## Review and merge locally

```bash
git switch main
git diff main...docs/add-goal
git merge --no-ff docs/add-goal -m "Merge learning goal"
git push origin main
git status --short
git log --oneline --graph --all -5
```

The status output should be empty. The log should contain two content commits
and a merge commit. On GitHub, a pull request lets collaborators discuss and
review a branch before the merge; this local exercise does not create a PR or
qualify for GitHub achievements.

Keep the directory for more practice. It lives at the path printed by
`printf '%s\n' "$practice_dir"` in the same shell session.

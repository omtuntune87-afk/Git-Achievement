# Practice resolving a merge conflict

Use Bash or Zsh with Git installed. This exercise creates a separate temporary
repository and does not change an existing project or publish to GitHub.

## Set up two conflicting edits

```bash
conflict_dir=$(mktemp -d)
cd "$conflict_dir"
git init -b main
```

Before committing, configure your own name and verified email locally if Git
does not already know your identity. Follow the identity instructions in the
[troubleshooting guide](troubleshooting.md).

```bash
printf 'Topic: Git basics\n' > topic.txt
git add topic.txt
git commit -m "docs: add initial topic"
git switch -c docs/advanced-topic
printf 'Topic: Advanced Git\n' > topic.txt
git add topic.txt
git commit -m "docs: propose advanced topic"
git switch main
printf 'Topic: Beginner Git\n' > topic.txt
git add topic.txt
git commit -m "docs: clarify beginner topic"
```

## Trigger and inspect the conflict

```bash
git merge docs/advanced-topic
```

This command is expected to fail with a content conflict. Stop here if the error
is anything else; do not continue blindly after a failed command.

```bash
git status
git diff --name-only --diff-filter=U
cat topic.txt
```

The unresolved file list should contain `topic.txt`. The file will contain
conflict markers surrounding the two versions. Neither version is automatically
the right answer: choose content that satisfies the intended behavior.

## Resolve and verify

For this exercise, retain both learning levels in a single line:

```bash
printf 'Topic: Beginner and advanced Git\n' > topic.txt
git add topic.txt
git diff --cached --check
git -c core.editor=true merge --continue
git status --short
git log --oneline --graph -5
cat topic.txt
```

The working tree should be clean and the final line should read
`Topic: Beginner and advanced Git`. The history should include a merge commit
with two parents. `core.editor=true` accepts Git's default merge message for
this one command; it does not change your editor configuration.

To abandon the exercise while the merge is still unresolved, run
`git merge --abort` instead of the resolution commands. That returns to the
committed `main` version. After a merge is completed, `--abort` no longer applies.

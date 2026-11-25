# Contributing

Choose a small improvement with a clear purpose. For larger features, open an issue first to agree on scope.

## Workflow

1. Clone the repository, or fork it first if you do not have write access.
2. Create a branch from an up-to-date `main` with a clean working tree.
3. Make one focused change and review the diff.
4. Run any checks documented for the files you changed.
5. Commit with a descriptive message, push your branch, and open a pull request.

Use messages such as `docs: clarify setup` or `fix: handle empty input`.
Each commit should represent a useful change that can be reviewed on its own.

## Before opening a pull request

- Explain what changed and why.
- Include the commands used to validate the change and their results.
- Check Markdown links, examples, and command accuracy for documentation changes.
- Run `git diff --check` before committing to catch whitespace errors.
- Exclude credentials, personal data, local environment files, and generated output.

There is currently no automated test suite. New runnable examples should include
setup instructions and a repeatable validation command.

## Review

Keep feedback specific and respectful. Resolve correctness or security problems
before merging, and update documentation whenever usage changes.

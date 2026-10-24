# Task: Build a CI workflow with GitHub Actions

In this task you will add a continuous integration (CI) workflow to your
private copy of this repository. The workflow must run the project's style
checks and tests automatically, but only for the events described below.

Before you start, make sure that `uv sync`, `uv run ruff check .`,
`uv run ruff format --check .` and `uv run pytest` all succeed on your
machine. Those are exactly the commands your workflow will run (see the
`uv` section of `README.md`).

## Requirements

Create the file `.github/workflows/ci.yml` in your repository. The workflow
must satisfy all of the following.

### 1. Run for pull requests, not for ordinary pushes

The workflow must run every time a pull request targeting `main` is opened
or receives new commits. A plain push to `main`, or to any branch that does
not match requirement 2, must **not** start the workflow.

### 2. Run for pushes to `feature/...` branches

In addition to pull requests, the workflow must run on every push to a
branch whose name starts with `feature/`, for example `feature/login-form`
or `feature/issue-42/fix-typo`. Pushes to branches with any other prefix
(`fix/...`, `test/...`, `main`, ...) must be ignored.

### 3. At least three independent jobs

The workflow must define **at least three jobs** that do not depend on each
other, so that GitHub runs them in parallel. The following three are
mandatory:

| Job      | What it does                                   |
|----------|------------------------------------------------|
| `lint`   | runs `uv run ruff check .`                     |
| `format` | runs `uv run ruff format --check .`            |
| `test`   | runs `uv run pytest`                           |

Each job needs its own checkout step, `uv` installation and
`uv sync --locked` step. "Independent" means a failing `lint` job must not
prevent the `test` job from running, and vice versa.

## Acceptance criteria

Your submission is complete when all of these are true. Check each of them
yourself before submitting.

- [ ] A push to a branch named `feature/<anything>` starts the workflow.
- [ ] A push to a branch named `fix/<anything>` does **not** start the
      workflow.
- [ ] A push directly to `main` does **not** start the workflow.
- [ ] Opening a pull request into `main` starts the workflow, and every new
      commit pushed to that pull request starts it again.
- [ ] The Actions page shows three (or more) jobs running at the same time;
      none of them waits for another one.
- [ ] All jobs are green on the final commit of your pull request.
- [ ] Introduce a deliberate style error (for example, a line longer than 88
      characters or an unused import), push it, and confirm that the `lint`
      job fails while the `test` job still runs and passes. Then fix the
      error and push again.

## What to submit

1. A pull request from a `feature/...` branch into `main` of **your private
   repository** containing `.github/workflows/ci.yml`.
2. In the pull request description, paste links to:
   - one workflow run started by a push to your `feature/...` branch;
   - one workflow run started by the pull request itself;
   - the run where the `lint` job failed on purpose.
3. One or two sentences in the pull request description answering: when you
   push a commit to a `feature/...` branch that already has an open pull
   request, how many workflow runs start, and why?

Do not push to the course repository. Your remote named `course` has pushes
disabled on purpose (see `README.md`).

## Hints

- The event for pull requests is `pull_request`. Its `branches` filter
  refers to the **target** (base) branch of the pull request, not to the
  branch you push to.
- The `push` event accepts a `branches` filter with glob patterns. Read
  the documentation carefully about the difference between `*` and `**`
  when a branch name contains a slash.
- Jobs are independent unless you connect them with `needs`.
- Use `astral-sh/setup-uv` to install `uv` on the runner. Pin it to a full
  version, for example `astral-sh/setup-uv@v10.3.2`; the short `@v10` tag
  does not exist for this action.
- `.python-version` in the repository tells `uv` which Python to install, so
  you do not need `actions/setup-python`.
- Workflow syntax is validated only when the file reaches GitHub. Commit
  small changes and read the error messages on the Actions page.

## Optional extensions (not graded)

- Add a fourth job `build` that runs `uv run check-manifest`, `uv build` and
  `uv run twine check dist/*`.
- Run the `test` job on a matrix of `ubuntu-latest`, `macos-latest` and
  `windows-latest`.
- Add a job that runs only after `lint`, `format` and `test` have all
  succeeded, and explain in the pull request how it differs from the
  independent jobs.

## Further reading

- [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [Events that trigger workflows](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows)
- [Filter pattern cheat sheet](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#filter-pattern-cheat-sheet)
- [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv)

# A sample Python project template

![Python Logo](https://www.python.org/static/community_logos/python-logo.png "Sample inline image")

A sample project that exists as an aid to the [Python Packaging User
Guide][packaging guide]'s [Tutorial on Packaging and Distributing
Projects][distribution tutorial].

This is the updated clone of original [sampleproject](https://github.com/pypa/sampleproject) template

### Clone the Course Repository
To clone the repository, follow this  [guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

**Important**: Please do not fork the repository.

The course repository is [here](https://github.com/Mexmath-Foundation/python-project-template).
You can either use Intellij IDE or do it manually.
For manually cloning create a new folder called `python-project-template`, move to the folder and run
````shell
git clone https://github.com/Mexmath-Foundation/python-project-template.git
````
in the commandline

### Verify the cloned repository
#### Check the remote
To check the remote repositories run the following command
```shell
git remote -v
```
in the commandline, the output should be
```shell
origin https://github.com/Mexmath-Foundation/python-project-template.git (fetch)
origin https://github.com/Mexmath-Foundation/python-project-template.git (push)
```
#### Check the branches
To check the branches run the following command
```shell
git branch
```
in the commandline, the output should be
```shell
* main
```

### Secure the original repository
Students **not allowed** to push the changes to the original course repository.
To prevent accidental pushes, it is necessary to detach the original repository from your private repository.
To do this, rename the `origin` and disable `push` to the original course repository.

#### Rename origin
To rename the origin run the following command
```shell
git remote rename origin course
```
in the commandline.

Run `git remote -v` in the commandline, the output should be
```shell
course https://github.com/Mexmath-Foundation/python-project-template.git (fetch)
course https://github.com/Mexmath-Foundation/python-project-template.git (push)
```
#### Disable pushes
To prevent pushing to the course repository replace push url by any non-existent url, i.e. DISABLED run the following command
```shell
git remote set-url --push course DISABLED
```
in the commandline.

Run `git remote -v` in the commandline, the output should be
```shell
course https://github.com/Mexmath-Foundation/python-project-template.git (fetch)
course DISABLED (push)
```

### Link the local repository to your private repository
To link the local repository to your private GitHub repository add new `origin`.

#### Open the newly created repository
Open your new GitHub repository web page and follow the instructions in `…or push an existing repository from the command line` section.
There should be a list of commands:
```shell
git remote add origin <your private repository>
git branch -M main
git push -u origin main
```
Run each command one-by-one in the commandline.

Execute `git remote -v` in the commandline, the output should be
```shell
course https://github.com/Mexmath-Foundation/python-project-template.git (fetch)
course DISABLED (push)
origin https://github.com/<your github account>/python-project-template.git  (fetch)
origin https://github.com/<your github account>/python-project-template.git (push)
```

## uv

This project uses [uv](https://docs.astral.sh/uv/) to manage the virtual
environment, dependencies, tests, linting and packaging.

### Install uv

**Unix/macOS**
```shell
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows**
```shell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

See the [uv installation guide](https://docs.astral.sh/uv/getting-started/installation/)
for other options (Homebrew, pipx, winget, ...).

### Create the virtual environment and install dependencies
```shell
uv sync
```
This creates `.venv/`, installs Python 3.13 (see `.python-version`) if it is
not available, installs the project in editable mode together with the development
dependencies from the `[dependency-groups]` table, and keeps everything in sync
with `uv.lock`.

There is no need to activate the virtual environment: prefix commands with
`uv run` and they execute inside it.

### Run tests
```shell
uv run pytest
```

### Check code style
The style of the Python code is checked with [ruff](https://docs.astral.sh/ruff/).

Lint (pycodestyle, pyflakes and import ordering rules):
```shell
uv run ruff check .
```

Check formatting:
```shell
uv run ruff format --check .
```

Fix what can be fixed automatically:
```shell
uv run ruff check --fix .
uv run ruff format .
```

### Build and check the package
```shell
uv run check-manifest
uv build
uv run twine check dist/*
```

* [uv](https://docs.astral.sh/uv/)
* [ruff](https://docs.astral.sh/ruff/)
* [pytest](https://docs.pytest.org/)
* [check-manifest](https://pypi.org/project/check-manifest/)


### Description

This project does not aim to cover best practices for Python project
development as a whole. For example, it does not provide guidance or tool
recommendations for version control, documentation, or testing.

[The source for this project is available here][src].

The metadata for a Python project is defined in the `pyproject.toml` file,
an example of which is included in this project. You should edit this file
accordingly to adapt this sample project to your needs.

----

This is the README file for the project.

The file should use UTF-8 encoding and can be written using
[reStructuredText][rst] or [markdown][md use] with the appropriate [key set][md
use]. It will be used to generate the project webpage on PyPI and will be
displayed as the project homepage on common code-hosting services, and should be
written for that purpose.

Typical contents for this file would include an overview of the project, basic
usage examples, etc. Generally, including the project changelog in here is not a
good idea, although a simple “What's New” section for the most recent version
may be appropriate.

[packaging guide]: https://packaging.python.org
[distribution tutorial]: https://packaging.python.org/tutorials/packaging-projects/
[src]: https://github.com/pypa/sampleproject
[rst]: http://docutils.sourceforge.net/rst.html
[md]: https://tools.ietf.org/html/rfc7764#section-3.5 "CommonMark variant"
[md use]: https://packaging.python.org/specifications/core-metadata/#description-content-type-optional

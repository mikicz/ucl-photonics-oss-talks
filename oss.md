---
lineNumbers: true
download: true
theme: dracula
highlighter: shiki
favicon: '/favicon.png'
fonts:
  sans: "Barlow"
---

# **Good practices for making reproducible open source code** 
## UCL Photonics Society Transferable Skills Workshop Series

---

# Why this workshop?

- As a student or researcher, you produce code for your projects
- Reproducibility and readability are key aspects of good scientific research
- Reproducibility and readability are key aspects of working in a team
- There is a software engineering skill gap between accademia and industry
- This workshop aims at teaching you good software engineering practices
- These skills will improve the quality of your projects, and foster collaboration

--- 

# Who am I?

- Mikuláš Poul, go by Miki (he/him)
- Bsc Software Engineering at CTU in Prague, Czech Republic
- Msc Data Science at UCL (graduated 2019)
- 10+ years professional experience in Python
- Currently Staff Engineer at Xelix 
- Maitain several OSS libraries in Python

---

# What is open source

- Source code made available publicly
- Modification and redistribution under certain conditions
- Invites collaboration
- Extremely common for
  - programming languages
  - libraries
- Quite common for
  - operating systems
  - projects
 
---

# Successes of open source in research

- Opensource has allowed for successful international research collaborations
- In AI -> PyTorch, Tensorflow, Gymnasium (RL), Llama...
- In Neuroscience -> Fruit Fly Brain Observatory
- In Biochemistry -> alphafold
- *TBD: more examples?*

---

# How to share open source

- Installable libraries are most commonly shared in repositories
  - For example PyPI for Python, npmjs for JavaScript
- Source code is most commonly shared using git
- Git is a distributed version control system
- GitHub is the most popular platform for working with git
  - Other popular choices are GitLab and BitBucket
- Provides access control, issue tracking, wiki, CI and other functionality
- Most features are free public repositories

--- 

# Intro to GitHub

- *Repository* - a collection of files, main unit on GitHub
- *Commit* - a change to some number of files
- *Branch* - collection of commits
- *Pull Request* - a request to merge one branch into another one

---

# How to structure a good opensource project on Github?

- Linting and formatting
- Library vs project
- Good repository structure
- Dependency management with virtual environments (Python)
- Testing
- OSS Licenses

---

# Linting

- Linting is analysing and finding issues in code using static code analysis
- Linters are tools which read the code (without execution) and raise issues
- Ranges from basic to quite sofisticated
  - Check no line has training spaces
  - Check all used code is imported
  - Checking for inefficient code
- Better linters even fix the issue for you

---

# Linting
## Reasons to use linters

- To enforce standard ways of doing things
- to keep the codebase consistent
- to reduce bugs
- to make pull requests easier
- to make the code faster
- to use latest language features
- to prevent silly mistakes

---

# Linting
## Linters and linting utils

- `pre-commit` - tool for running linters before commiting new code
- `ruff` - new linter which implements most standard Python linters very fast
- `nbQA` - tool for running linters on jupyter notebooks

--- 

# Formatting

<img src="https://i.imgur.com/vOWAAUK.png" alt="Python Environment" style="max-width: 75%; margin: 0 auto;">

---

# Formatting

- Each code has some formatting
- Each programmer writes slightly differently
- When collaborating, common formatting is important
  - for the code to work correctly
  - for pull requests to be readable
  - for new collaborators to be able to read all code easily
  - *TBD*
- Modern way of doing things is to use automated formatters

---

# Formatting
## Automatic formatting

- Forever removes the arguments over tiny details
- Should be run before every commit
- Should be enforced on GitHub through CI
- In Python, very popular choice is `black`
  - The only configuration is line length
- Currently, I would reccommend `ruff format` - compatible with `black` but faster

---

# Formatting
## Example - bad

```python
if (__name__ == "__main__"):

    for (library, purpose) in [
        ("pandas", "dataframes"),
        (
            "numpy", "multi-dimensional arrays"
        ),
("tensorflow", "deep learning")
                ]:
        print(
          library, purpose
        )
```

---

# Formatting
## Example - ruff reformatted

```python
if __name__ == "__main__":
    for library, purpose in [
        ("pandas", "dataframes"),
        ("numpy", "multi-dimensional arrays"),
        ("tensorflow", "deep learning"),
    ]:
        print(library, purpose)
```

---

# Library vs project

---

# Good repository structure

---

# Dependency management with virtual environments
## Python environments

- ... can be a mess

---

# Dependency management with virtual environments
## Python environments

<img src="https://imgs.xkcd.com/comics/python_environment_2x.png" alt="Python Environment" style="max-width: 45%; margin: 0 auto;">

---

# Dependency management with virtual environments
## Python environments

- ... can be a mess
- *In general*, Python packages belong to an environment
- *In general*, the default is the "global environment"

---

# Dependency management with virtual environments
## Problems with global environment

- The system itself uses Python from global environment
- Different things you install need different dependencies
- Different things you install need different Python versions
- Solution -> "virtual environments"

---

# Dependency management with virtual environments
## Virtual environments

- A way to separate dependencies between projects
- **Absolutely** the way to go
- Allows different Python versions and dependencies
- Activation sets the environment for your current shell
- `python -m venv venv` or `py -3 -m venv venv` (Windows)
- `source venv/bin/activate` or `venv\Scripts\activate` (Windows)

---

# Dependency management with virtual environments
## Defining dependencies

- Your project/libraries have dependencies
- To allow reproducibility, those need to be defined

--- 

# Dependency management with virtual environments
## Defining dependencies - level 1

> (Not an actual recommendation!)

Just include it in the README, awful, but better than nothing.

```markdown
-- README.md 

## Dependencies

To run this program, install `pandas`.
```

---

# Dependency management with virtual environments
## Defining dependencies - level 2

Define `requirements.txt`

```text
pandas
scikit-learn
```

To install

```bash
$ pip install -r requirements.txt
```

---

# Dependency management with virtual environments
## Issues with requirements.txt

- Ok, but what version of `pandas`?
  - Versions of libraries can have significant differences between versions
  - Even `pandas<2` or `pandas>2` can eventually break
- What about the dependencies of `pandas`?
  - A dependency of `pandas` can break `pandas` itself 
  - If not listed what version should be installed?
  - Transitive dependencies can be silently updated changing dependencies.
  - `pip freeze > requirements-all.txt`

--- 

# Dependency management with virtual environments
## Issues with requirements.txt

- What if I need some dependencies just for tests?
  - `requirements-test.txt`
  - `requirements-profiling.txt`
  - ...
- -> Not fit for purpose anymore 

---

# Dependency management with virtual environments
## Defining dependencies - level 3

- Using a dependency manager
  - `poetry` / `pipenv` / `uv`
- Usual features
  - Define top-level dependencies
  - Split dependencies into groups
  - All (including transitive) dependencies and versions in a lock file
- They often do extra stuff
  - Manage virtual envs
  - Make publishing easier
  - Install Python

---

# Dependency management with virtual environments
## Using poetry

- `poetry add pandas`
- `poetry add 'pytest>8' --dev`

```toml
[tool.poetry]
...

[tool.poetry.dependencies]
pandas = "^2.2.3"

[tool.poetry.group.dev.dependencies]
pytest = ">8"
```

---

# Dependency management with virtual environments
## Using poetry

```toml
[[package]]
name = "pytest"
version = "8.3.3"
description = "pytest: simple powerful testing with Python"
optional = false
python-versions = ">=3.8"
files = [
    {file = "pytest-8.3.3-py3-none-any.whl", hash = "sha256:a6853c7375b2663155079443d2e45de913a911a11d669df02a50814944db57b2"},
    {file = "pytest-8.3.3.tar.gz", hash = "sha256:70b98107bd648308a7952b06e6ca9a50bc660be218d53c257cc1fc94fda10181"},
]

[package.dependencies]
colorama = {version = "*", markers = "sys_platform == \"win32\""}
iniconfig = "*"
packaging = "*"
pluggy = ">=1.5,<2"

[package.extras]
dev = ["argcomplete", "attrs (>=19.2)", "hypothesis (>=3.56)", "mock", "pygments (>=2.7.2)", "requests", "setuptools", "xmlschema"]
```

---

# Dependency management with virtual environments
## Defining dependencies - level 3

- Easier dependency management
- Easier to produce reproducable builds

---

# Dependency management with virtual environments
## What about non-python projects?

*TBD: add tips or tool name for Matlab, C, C++...*

---

# Testing

---

# OSS Licenses

- Define the conditions under which the software is shared
- Differ in restrictiveness
- Copyleft vs permissive
  - Copyleft requires keeping same license for derivitive work (e.g. GPL, AGPL)
  - Permissive lets you do lot more (MIT, Apache, BSD)
- Packages in Python ecosystem primarily use permissive (~70%)
  - MIT is the most popular choice
- https://choosealicense.com/ 


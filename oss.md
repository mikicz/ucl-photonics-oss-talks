---
lineNumbers: true
download: true
theme: dracula
highlighter: shiki
favicon: '/favicon.png'
fonts:
  sans: "Barlow"
addons:
  - slidev-component-progress
---

# **Good practices for making reproducible open source code** 
## UCL Photonics Society Transferable Skills Workshop Series

---

# Why this workshop?

<v-clicks>

- As a student or researcher, you produce code for your projects
- Reproducibility and readability are key aspects of good scientific research
- Reproducibility and readability are key aspects of working in a team
- There is a software engineering skill gap between accademia and industry
- This workshop aims at teaching you good software engineering practices
- These skills will improve the quality of your projects, and foster collaboration

</v-clicks>

--- 

# Who am I?

<v-clicks>

- Mikuláš Poul, go by Miki (he/him)
- Bsc Software Engineering at CTU in Prague, Czech Republic
- Msc Data Science at UCL (graduated 2019)
- 10+ years professional experience in Python
- Currently Staff Engineer at Xelix 
- Maitain several OSS libraries in Python


</v-clicks>

---
layout: section
---

# Open source

---

# What is open source

<v-clicks>

- Source code made available publicly
- Modification and redistribution under certain conditions
- Invites collaboration
- Extremely common for
  - programming languages
  - libraries
- Quite common for
  - operating systems
  - projects
  
</v-clicks>
 
---

# Successes of open source in research

- Opensource has allowed for successful international research collaborations
- In Mathematics -> Numpy
- In AI -> PyTorch, Tensorflow, Gymnasium (RL)
- In Neuroscience -> Fruit Fly Brain Observatory
- In Biochemistry -> alphafold

---

# How to share open source

<v-clicks>

- Installable libraries are most commonly shared in repositories
  - tor example PyPI for Python, npmjs for JavaScript
- Source code is most commonly shared using git
- Git is a distributed version control system
- GitHub is the most popular platform for working with git
  - other popular choices are GitLab and BitBucket
- Provides access control, issue tracking, wiki, CI and other functionality
- Most features are free public repositories

</v-clicks>

--- 
layout: section
---

# GitHub

---

# Intro to GitHub

<v-clicks>

- *Repository* - a collection of files, main unit on GitHub
- *Commit* - a change to some number of files
- *Branch* - collection of commits
- *Pull Request* - a request to merge one branch into another one

</v-clicks>

---

# How to structure a good opensource project on Github?

<v-clicks>

- Formatting and linting
- Library vs project
- Good repository structure
- Dependency management with virtual environments
- Testing
- OSS Licenses

</v-clicks>

--- 
layout: section
---

# Formatting
---

# Formatting

<img src="https://i.imgur.com/vOWAAUK.png" alt="Python Environment" style="max-width: 75%; margin: 0 auto;">

---

# Formatting

<v-clicks>

- Each code has some formatting
- Each programmer writes slightly differently
- When collaborating, common formatting is important
  - for the code to work correctly
  - for pull requests to be readable and easier to manage
  - for new collaborators to be able to read code easily
- Modern way of doing things is to use automated formatters

</v-clicks>

---

# Formatting
## Automatic formatting

<v-clicks>

- Forever removes the arguments over tiny details
- Should be run before every commit
- Should be enforced on GitHub through CI
- In Python, very popular choice is `black`
  - the only configuration is line length
- Currently, I would reccommend `ruff format` - compatible with `black` but faster

</v-clicks>

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
layout: section
---

# Linting
---

# Linting

<v-clicks>

- Linting is analysing and finding issues in code using static code analysis
- Linters are tools which read the code (without execution) and raise issues
- Ranges from basic to quite sofisticated
  - check no line has training spaces
  - check all used code is imported
  - check for inefficient code
- Better linters even fix the issue for you

</v-clicks>

---

# Linting
## Reasons to use linters

<v-clicks>

- To enforce standard ways of doing things
- To keep the codebase consistent
- To reduce bugs
- To make pull requests easier
- To make the code faster
- To use latest language features
- To prevent silly mistakes

</v-clicks>

---

# Linting
## Linters and linting utils

<v-clicks>

- `pre-commit` - tool for running linters before commiting new code
- `ruff` - new linter which implements most standard Python linters very fast
- `nbQA` - tool for running linters on jupyter notebooks

</v-clicks>

---
layout: section
---

# Library vs project

---

# Library vs project

<v-clicks>

- Library is some code which provides specific funcionality
  - used as components while building other software
  - for example Pandas, Numpy, Tensorflow, etc.
- Project is standalone piece of software designed
  - used directly by end user 
  - for example Firefox, Blender, VLC media player, etc.
- Libraries often use more libraries
- Projects usually use many libraries

</v-clicks>

---

# Library vs project

<v-clicks>

- Both libraries and projects can be open source
- Similar principles apply for sharing and collaborating
- Major diffences come when it comes to publishing

</v-clicks>

---
layout: section
---

# Repository structure

---

# Good repository structure

<v-clicks>

- Important to make collaboration easier
  - easier for new collaborators to explore and navigate
  - easier to decide where new code should go
  - easier to maintain long term
- Can make publishing and testing easier

</v-clicks>

---

# Good repository structure

- Root of the repository should contain
  - README, LICENSE
  - configuration files
  - few core folders
  - TBD main entry point

---

# Good repository structure
## README

<v-clicks>

- The first thing most people see
- Usually written in Markdown
- Should contain
  - what does it do
  - how to install it
  - basic usage
  - typical development tasks
- Larger projects have dedicated READMEs for changelog and contributing

</v-clicks>

---

# Good repository structure
## Configuration files

<v-clicks>

- Version control configuration)
  - `.gitignore`
- Dependency management files
  - `requirements.txt`, `pyproject.toml`
- Code style & linting configuration
  - `.pre-commit-config.yaml`, `pyproject.toml`
- CI & Github configuration
  - `.github`

</v-clicks>

---

# Good repository structure
## Core folders

<v-clicks>

- Primary source code, usually `src/` or `lib/`
  - for python packages often the name of the package, e.g. `pandas`
- Tests, usually `tests/`
- Documentation, usually `docs/` or `examples/`
- Publishing / deployment, `scripts/` or `dist/` or `build/`

</v-clicks>

---
layout: section
---

# Dependency management with virtual environments

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

<v-clicks>

- *In general*, Python packages belong to an environment
- *In general*, the default is the "global environment"

</v-clicks>

 
---

# Dependency management with virtual environments
## Problems with global environment

<v-clicks>

- The system itself uses Python from global environment
- Different things you install need different dependencies
- Different things you install need different Python versions
- Solution -> "virtual environments"

</v-clicks>

---

# Dependency management with virtual environments
## Virtual environments

<v-clicks>

- A way to separate dependencies between projects
- **Absolutely** the way to go
- Allows different Python versions and dependencies
- Activation sets the environment for your current shell
- `python -m venv venv` or `py -3 -m venv venv` (Windows)
- `source venv/bin/activate` or `venv\Scripts\activate` (Windows)

</v-clicks>

---

# Dependency management with virtual environments
## Defining dependencies

<v-clicks>

- Your project/libraries have dependencies
- To allow reproducibility, those need to be defined

</v-clicks>

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

<v-clicks>

- Ok, but what version of `pandas`?
  - versions of libraries can have significant differences between versions
  - even `pandas<2` or `pandas>2` can eventually break
- What about the dependencies of `pandas`?
  - a dependency of `pandas` can break `pandas` itself 
  - if not listed what version should be installed?
  - transitive dependencies can be silently updated changing dependencies.
  - `pip freeze > requirements-all.txt`

</v-clicks>

--- 

# Dependency management with virtual environments
## Issues with requirements.txt



- What if I need some dependencies just for tests?
  - `requirements-test.txt`
  - `requirements-profiling.txt`
  - ...

<v-click>

- -> Not fit for purpose anymore

</v-click>

---

# Dependency management with virtual environments
## Defining dependencies - level 3

<v-clicks>

- Using a dependency manager
  - `poetry` / `pipenv` / `uv`
- Usual features
  - define top-level dependencies
  - split dependencies into groups
  - all (including transitive) dependencies and versions in a lock file
- They often do extra stuff
  - manage virtual envs
  - make publishing easier
  - install Python

</v-clicks>

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

<v-clicks>

- Easier dependency management
- Easier to produce reproducable builds

</v-clicks>

---

# Dependency management with virtual environments
## Non-python projects

<v-clicks>

- Most languages have some sort of package manager
- They differ in functionality by language
- Some languages have more of a standard manager than others
- Dependencies will always be an issue, always worth investing into it

</v-clicks>

---
layout: section
---

# Automated Testing

---

# Automated testing
## Why testing is important

<v-clicks>

- Increases trust in code
- Makes it easier to update code
- Makes it easier to manage a project
- Serves as additional documentation

</v-clicks>

---

# Automated testing
## Types of tests

<v-clicks>

- Unit tests
  - test smallest components (functions, methods, classes)
  - verify the core logic
  - test various edge cases
- Integration tests
  - test integration of components
- End-to-end tests
  - test full application on all levels

</v-clicks>

---

# Automated testing
## Continuous integration

<v-clicks>

- CI is a set of tools to run tests automatically
- For example running tests on code in pull requests
- Can be checking linting and formatting as well

</v-clicks>

---

# Automated testing
## Pytest

<v-clicks>

- Python's inbuilt solution is hard to use
- Pytest is an alternative open source solution
- Simpler setup and easier to write tests

</v-clicks>

---

# Automated testing
## Pytest example

```python
class Cat:
    def make_sound(self) -> str:
        return "mňau"
```

```python
def test_cat_sound() -> None:
    assert Cat().make_sound() == "mňau"
```

```python
@pytest.fixture
def cat() -> Cat:
    return Cat()

def test_cat_sound(cat: Cat) -> None:
    assert cat.make_sound() == "mňau"
```

---
layout: section
---

# OSS Licenses

---

# OSS Licenses

<v-clicks>

- Define the conditions under which the software is shared
- Differ in restrictiveness
- Copyleft vs permissive
  - copyleft requires keeping same license for derivitive work (e.g. GPL, AGPL)
  - permissive lets you do lot more (MIT, Apache, BSD)
- Packages in Python ecosystem primarily use permissive (~70%)
  - MIT is the most popular choice
- https://choosealicense.com/ 

</v-clicks>

---
layout: section
---

# Workshop


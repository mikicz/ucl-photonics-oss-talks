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
- However, there is a huge software engineerings skill gap between accademia and industry
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

# Intro to GitHub


---

# How to structure a good opensource project on Github?
- Linting and formatting
- Library vs project
- Good repository structure
- Dependency management with virtual environments (Python)
- Testing
- OSS Licenses


---
# Linting and formatting

---

# Library vs project


---

# Good repository structure

---
# Dependency management with virtual environments (Python)
## Python environments

- ... can be a mess

---
# Dependency management with virtual environments (Python)
## Python environments

<img src="https://imgs.xkcd.com/comics/python_environment_2x.png" alt="Python Environment" style="max-width: 50%; margin: 0 auto;">

---
# Dependency management with virtual environments (Python)
## Python environments

- ... can be a mess
- *In general*, Python packages belong to an environment
- *In general*, the default is the "global environment"

---
# Dependency management with virtual environments (Python)
## Problems with global environment

- The system itself uses Python from global environment
- Different things you install need different dependencies
- Different things you install need different Python versions
- Solution -> "virtual environments"

---
# Dependency management with virtual environments (Python)
## Virtual environments

- A way to separate dependencies between projects
- **Absolutely** the way to go
- Allows different Python versions and dependencies
- Activation sets the environment for your current shell
- `python -m venv venv` or `py -3 -m venv venv` (Windows)
- `source venv/bin/activate` or `venv\Scripts\activate` (Windows)

---
# Dependency management with virtual environments (Python)
## Defining dependencies

- Your project/libraries have dependencies
- To allow reproducibility, those need to be defined

--- 
# Dependency management with virtual environments (Python)
## Defining dependencies - level 1

> (Not an actual recommendation!)
> 
> Just include it in the README, awful, but better than nothing.

```markdown
-- README.md 

## Dependencies

To run this program, install `pandas`.
```

---
# Dependency management with virtual environments (Python)
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
# Dependency management with virtual environments (Python)
## Issues with requirements.txt

- Ok, but what version of `pandas`?
  - Versions of libraries can have significant differences between versions?
  - Even `pandas<2` or `pandas>2` can eventually break
- What about the dependencies of `pandas`?
  - A dependency of `pandas` can break `pandas` itself 
  - If not listed what version should be installed?
  - Transitive dependencies can be silently updated changing dependencies.
  - `pip freeze > requirements-all.txt`

--- 
# Dependency management with virtual environments (Python)
## Issues with requirements.txt

- What if I need some dependencies just for tests?
  - `requirements-test.txt`
  - `requirements-profiling.txt`
  - ...
- -> Not fit for purpose anymore 

---
# Dependency management with virtual environments (Python)
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
# Dependency management with virtual environments (Python)
## Using poetry

- `poetry add pandas`
- `poetry add 'pytest>8' --dev`

```toml
[tool.poetry]
...

[tool.poetry.dependencies]
pandas = "^2.2.3"

[tool.poetry.group.dev.dependencies]
pytest = "pytest>8"
```

---
# Dependency management with virtual environments (Python)
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
# Dependency management with virtual environments (Python)
## Defining dependencies - level 3

- Easier dependency management
- Easier to produce reproducable builds

---


# Testing

---

# OSS Licenses

- Define the conditions under which the software is shared
- Differ in restrictiveness
- Copyleft vs permissive
- Copyleft requires keeping same license for derivitive work ???????? (e.g. GNU)
- Permissive lets you do lot more (MIT, Apache ????????)
- Stats??? 

---



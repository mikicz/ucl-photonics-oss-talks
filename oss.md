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

---

# Workshop Intruction

...

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

# OSS Licenses

- Define the conditions under which the software is shared
- Differ in restrictiveness
- Copyleft vs permissive
- Copyleft requires keeping same license for derivitive work ???????? (e.g. GNU)
- Permissive lets you do lot more (MIT, Apache ????????)
- Stats??? 

---

# Library vs project


---

# Python environments

- ... can be a mess

---

# Python environments

<img src="https://imgs.xkcd.com/comics/python_environment_2x.png" alt="Python Environment" style="max-width: 50%; margin: 0 auto;">

---

# Python environments

- ... can be a mess
- *In general*, Python packages belong to an environment
- *In general*, the default is the "global environment"

---

# Problems with global environment

- The system itself uses Python from global environment
- Different things you install need different dependencies
- Different things you install need different Python versions
- Solution -> "virtual environments"

---

# Virtual environments

- A way to separate dependencies between projects
- **Absolutely** the way to go
- Allows different Python versions and dependencies
- Activation sets the environment for your current shell
- `python -m venv venv` or `py -3 -m venv venv` (Windows)
- `source venv/bin/activate` or `venv\Scripts\activate` (Windows)

---

# Defining dependencies

- Your project/libraries have dependencies
- To allow reproducibility, those need to be defined

--- 

# Defining dependencies - level 1

> (Not an actual recommendation!)
> 
> Just include it in the README, awful, but better than nothing.

```markdown
-- README.md 

## Dependencies

To run this program, install `pandas`.
```

---

# Defining dependencies - level 2

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

# Issues with requirements.txt

- Ok, but what version of `pandas`?
  - Versions of libraries can have significant differences between versions?
  - Even `pandas<2` or `pandas>2` can eventually break
- What about the dependencies of `pandas`?
  - A dependency of `pandas` can break `pandas` itself 
  - If not listed what version should be installed?
  - Transitive dependencies can be silently updated changing dependencies.
  - `pip freeze > requirements-all.txt`

--- 

# Issues with requirements.txt

- What if I need some dependencies just for tests?
  - `requirements-test.txt`
  - `requirements-profiling.txt`
  - ...
- -> Not fit for purpose anymore 

---

# Defining dependencies - level 3

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

# Using poetry

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

# Using poetry

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

# Defining dependencies - level 3

- Easier dependency management
- Easier to produce reproducable builds

---

# Repository structure

---

# Testing

---

# Linting and formatting

---

# Intro to GitHub

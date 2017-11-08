# doc-basics

[![Documentation Status](http://readthedocs.org/projects/doc-basics/badge/?version=latest)](http://doc-basics.readthedocs.io/en/latest/?badge=latest)

A minimal Sphinx documentation structure.

Features:

- Python 3
- Sphinx >= 1.6
- `docs`: the root directory for documentation
- intersphinx using Python 3
- supports markdown and restructured text
- rtd yml build file
- conda `environment.yml`
- pip `requirements_docs.txt`

## Installation

1. Clone the repo from GitHub

```bash
git clone https://github.com/willingc/doc-basics.git
```

2. Change directory to `doc-basics`.

```bash
cd doc-basics
```

3. Create and activate a virtual environment

```bash
python3 -m venv mydocenv
source mydocenv/bin/activate
```

4. Install requirements.

```bash
python3 -m pip install -r docs/requirements_docs.txt
```

## Build documentation

From the `docs` directory:

| Task | Command |
| ---- | :-----: |
| Clean out prior doc builds | `make clean` |
| Build docs (in html format) | `make html` |
| Check links in docs | `make linkcheck` |
| View docs | `open _build/html/index.html` |


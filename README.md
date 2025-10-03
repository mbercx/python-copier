[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-black.json)](https://github.com/copier-org/copier)

# `python-copier`

Template for Python packages based on [`copier`](https://copier.readthedocs.io/en/latest/).

## Features

* 📦 **Package management**:
    - Develop with your preferred tools (extras, [`uv`](https://docs.astral.sh/uv/) or [Hatch](https://hatch.pypa.io/)).
    - Build your package with [Hatch](https://hatch.pypa.io/). 
* 🧹 [**Pre-commit**](https://pre-commit.com/): Format and lint your code with [Ruff](https://docs.astral.sh/ruff/).
* 🧪 **Tests**: Write tests with [`pytest`](https://docs.pytest.org/en/stable/).
* 📚 **Documentation**: Write docs in [MyST](https://mystmd.org/) or [MkDocs](https://www.mkdocs.org/).
* ⚙️ **GitHub Actions**:
    * Deploy documentation to [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site) or [Read the Docs](https://about.readthedocs.com/).
    * Run pre-commit checks and tests on every pull request.

## Usage

Follow the [`copier` installation instructions](https://copier.readthedocs.io/en/latest/#installation).
Then simply run

```
copier copy https://github.com/mbercx/python-copier <package_name>
```

And answer the questions to generate a new Python package.

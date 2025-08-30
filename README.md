[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-black.json)](https://github.com/copier-org/copier)

# `python-copier`

Template for Python packages based on [`copier`](https://copier.readthedocs.io/en/latest/).

## Features

* 📦 **Package management**: Test, build, and deploy your package with [Hatch](https://hatch.pypa.io/) environments.
*  📚 **Documentation**: Use [MyST](https://mystmd.org/) or [MkDocs](https://www.mkdocs.org/) to document your package.
* 🧹 **Pre-commit**: Format and lint your code with [Ruff](https://docs.astral.sh/ruff/).
* ⚙️ **GitHub Actions**:
    * Deploy your documentation on [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

## Usage

Follow the [`copier` installation instructions](https://copier.readthedocs.io/en/latest/#installation).
Then simply run

```
copier copy https://github.com/mbercx/python-copier <package_name>
```

And answer the questions to generate a new Python package.

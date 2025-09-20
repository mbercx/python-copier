# Introduction

A `copier`-based template for Python packages.

## Features

* 📦 **Package management**: Test, build, and deploy your package with [Hatch](https://hatch.pypa.io/) environments.
* 📚 **Documentation**: Document your package with [MyST](https://mystmd.org/) or [MkDocs](https://www.mkdocs.org/).
* 🧹 **Pre-commit**: Format and lint your code with [Ruff](https://docs.astral.sh/ruff/).
* ⚙️ **GitHub Actions**:
    * Deploy documentation to [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).
    * Run pre-commit checks on every pull request.

## Usage

Follow the [`copier` installation instructions](https://copier.readthedocs.io/en/latest/#installation).
Then simply run

```
copier copy https://github.com/mbercx/python-copier <package_name>
```

And answer the questions to generate a new Python package.

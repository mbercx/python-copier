# Introduction

A `copier`-based template for Python packages.

## Features

* 📦 **Package management**: Test, build, and deploy your package with [Hatch](https://hatch.pypa.io/) environments.
* 📚 **Documentation**: Document your package in [MyST](https://mystmd.org/) or [MkDocs](https://www.mkdocs.org/).
* 🧹 **Pre-commit**: Format and lint your code with [Ruff](https://docs.astral.sh/ruff/).
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

## Next steps

After copying the template, you might still have to do some additional configuration.

### Deploy documentation

#### Read the Docs

1. Push your code to GitHub.
2. Go to [Read the Docs](https://readthedocs.org/) (RTD) and [import your project](https://docs.readthedocs.com/platform/stable/tutorial/index.html#importing-the-project-to-read-the-docs).
   The build will use the included `.readthedocs.yaml` automatically.
3. Set the RTD settings to [build from GitHub pull requests](https://docs.readthedocs.com/platform/stable/tutorial/index.html#triggering-builds-from-pull-requests).

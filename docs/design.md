# Design

## Build system

This template uses **[Hatch](https://hatch.pypa.io/)** as the build backend and project manager.

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```

### ✅ Why choose Hatch?

Hatch is a modern, [PEP 517](https://peps.python.org/pep-0517/)-compliant build backend.
Main features:

**Tool consolidation**

Hatch can also manage virtual environments, test runners, and formatters (e.g. `hatch fmt`), reducing reliance on multiple tools.

**[PEP 621](https://peps.python.org/pep-0621/) support**

Clean, declarative configuration in `pyproject.toml`.
Keeping the number of configuration files minimal.

**Integrated versioning**

Instead of hardcoding the version number in `pyproject.toml`, we delegate it to a separate file (`__about__.py`) inside the source tree.
This pattern has a few advantages:

* **Single source of truth**: The version lives inside your package, making it accessible at runtime via `import`.
* **Tool-friendly**: Hatch can automatically read and update this file using `[tool.hatch.version]`, supporting both static and dynamic versioning.
* **Clean packaging**: Keeps `pyproject.toml` minimal, and avoids cluttering the `__init__.py` with metadata.

## Documentation

We use [MyST Markdown](https://mystmd.org/) for our Python package documentation.
We want to use a Markdown-based documentation tool for simplicity, avoiding Sphinx' reStructuredText format.
The main reason to use this over [MkDocs](https://www.mkdocs.org/) to test the Jupyter notebook integration, especially the "executable content".
MyST is also easy to integrate with Sphinx, which has a lot of powerful tools, especially for scientific software.

## DevOps

This template includes development automation tools that ensure code quality, consistency, and developer efficiency.

### Pre-commit hooks

We use [`pre-commit`](https://pre-commit.com/) to run automated checks before each commit.
The configuration is stored in `.pre-commit-config.yaml`, and only uses `hatch fmt` in two separate steps:

* `hatch fmt -f`
* `hatch fmt -l`

The steps are separated in first _formatting_ the code, then _linting_ it to check for issues.

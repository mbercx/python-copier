# Introduction

A `copier`-based template for Python packages.

## Features

* 📦 **Package management**:
    - Develop with your preferred tools (extras, [`uv`](https://docs.astral.sh/uv/) or [Hatch](https://hatch.pypa.io/)).
    - Automatic changelog generation from emoji-typed commit messages.
    - Build your package with [Hatch](https://hatch.pypa.io/). 
* 🧹 [**Pre-commit**](https://pre-commit.com/): Format and lint your code with [Ruff](https://docs.astral.sh/ruff/).
* 🧪 **Tests**: Write tests with [`pytest`](https://docs.pytest.org/en/stable/), with optional coverage reporting (basic summary or [Codecov](https://about.codecov.io/) integration).
* 📚 **Documentation**: Write docs in [MyST](https://mystmd.org/) or [MkDocs](https://www.mkdocs.org/).
* ⚙️ **GitHub Actions**:
    * Deploy documentation to [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site) or [Read the Docs](https://about.readthedocs.com/).
    * Run pre-commit checks and tests on every pull request.
    * Publish to [PyPI](https://pypi.org/) on `vX.Y.Z` tags via [Trusted Publishing](https://docs.pypi.org/trusted-publishers/) — no API tokens.
    * Optional automatic template updates via a bot.

## Usage

Follow the [`copier` installation instructions](https://copier.readthedocs.io/en/latest/#installation).
Then simply run

```
copier copy https://github.com/mbercx/python-copier <package_name>
```

And answer the questions to generate a new Python package.

## Next steps

After copying the template, you might still have to do some additional configuration.

### Publish to PyPI

The generated package ships with a `cd.yaml` workflow that publishes to PyPI on `vX.Y.Z` tag pushes via [Trusted Publishing](https://docs.pypi.org/trusted-publishers/).
See [Publishing to PyPI](publishing.md) for the one-time setup steps.

You don't have to publish right away, but if you care about the project name, push an early `0.0.1` release to claim it on PyPI before someone else does.

### Deploy documentation

#### Read the Docs

1. Push your code to GitHub.
2. Go to [Read the Docs](https://readthedocs.org/) (RTD) and [import your project](https://docs.readthedocs.com/platform/stable/tutorial/index.html#importing-the-project-to-read-the-docs).
   The build will use the included `.readthedocs.yaml` automatically.
3. Set the RTD settings to [build from GitHub pull requests](https://docs.readthedocs.com/platform/stable/tutorial/index.html#triggering-builds-from-pull-requests).

### Coverage with Codecov

If you selected `coverage=codecov` when generating, the CI workflow uploads coverage data to [Codecov](https://about.codecov.io/) after every test run.
To get this working:

1. Sign up at [codecov.io](https://codecov.io/) and connect your GitHub account.
2. Add your repository on the Codecov dashboard — it will start receiving uploads automatically.

No repository secret is needed for public repos.
For private repos, add a `CODECOV_TOKEN` secret to your repository and pass it in the workflow's `codecov-action` step.

### Automatic template updates

The template can optionally add a `copier-update.yaml` workflow that checks for upstream template changes every week, runs `copier update`, and opens a PR with the proposed changes.
This feature is controlled by the hidden `auto_update` question (set via `--data auto_update=<value>` when copying or updating):

- `none` (default) — no workflow is added.
- `github-token` — uses the default `GITHUB_TOKEN`. Zero setup, but PRs created this way [won't trigger other CI workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow#triggering-a-workflow-from-a-workflow).
- `pat` — uses a Personal Access Token stored as a `COPIER_UPDATE_TOKEN` repository secret. PRs will trigger CI normally.

To enable it on an existing project, run:

```
copier update --data auto_update=github-token
```

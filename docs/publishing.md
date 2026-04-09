# First publication to PyPI

The generated package ships with a `.github/workflows/cd.yaml` workflow that publishes to PyPI on `vX.Y.Z` tag pushes, via [PyPI Trusted Publishing](https://docs.pypi.org/trusted-publishers/) — so you never need to store a PyPI API token as a repository secret.

Before the **first** release can succeed, you have to do the steps below once.
Subsequent releases only require a tag push; see the generated package's own developer guide for that.

## One-time setup

1. **Push the generated package to GitHub.**
2. **Create a PyPI project** (or a [pending publisher](https://docs.pypi.org/trusted-publishers/creating-a-project-through-oidc/) if the project doesn't exist yet).
3. **Register the Trusted Publisher.** On PyPI, go to *Your projects → Publishing* and add a new publisher with:
    - **Owner**: your GitHub user or organisation
    - **Repository**: the generated repository name
    - **Workflow name**: `cd.yaml`
    - **Environment name**: `pypi`
4. **Create the `pypi` environment** on the GitHub repository (*Settings → Environments → New environment*).
   The environment name must match what you registered on PyPI, and must exist before you push your first release tag — otherwise the `publish` job will fail to start.

You can optionally add required reviewers on the `pypi` environment to gate releases on manual approval.

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

The user can select which documentation engine they prefer.
Some information on the two options is already provided below, this will be fleshed out more as both frameworks are tested more rigorously.

## MyST Markdown

[MyST Markdown](https://mystmd.org/) is a Markdown-based documentation tool that avoids Sphinx' reStructuredText format while preserving most of its power.
The main reason to use this over [MkDocs](https://www.mkdocs.org/) to test the Jupyter notebook integration, especially the "executable content".
MyST is also easy to integrate with Sphinx, which has a lot of powerful tools, especially for scientific software.

## MkDocs

[MkDocs](https://www.mkdocs.org/) is another Markdown-based documentation tool that focusses even more on simplicity.
Some features:

1. Very simple to build and write, not too much faff.
1. Builds/serves very fast (faster than MyST in my experience).
1. Static pages, easy to host.
1. Sleek look, using [Material for MkDocs](https://github.com/squidfunk/mkdocs-material).

## DevOps

This template includes development automation tools that ensure code quality, consistency, and developer efficiency.

### Pre-commit hooks

We use [`pre-commit`](https://pre-commit.com/) to run automated checks before each commit.
The configuration is stored in `.pre-commit-config.yaml`, and only uses `hatch fmt` in two separate steps:

* `hatch fmt -f`
* `hatch fmt -l`

The steps are separated in first _formatting_ the code, then _linting_ it to check for issues.

## Development standards

Good development standards make for better code.

**Versioning**: We try to adhere to [SemVer](https://semver.org/).

### Commit messages

> A well-cared for log is a beautiful and useful thing

This quote comes from the following article, which should be considered a mandatory read for anyone maintaining a package:

[https://cbea.ms/git-commit/](https://cbea.ms/git-commit/)

The summary, slightly adapted by personal preferences (indicated in boldface):

* [Separate subject/title from body with a blank line](https://cbea.ms/git-commit/#separate).
* [Limit the subject line to 50 characters](https://cbea.ms/git-commit/#limit-50) **if possible, 72 is a hard limit**.
* [Capitalize the subject line](https://cbea.ms/git-commit/#capitalize) and [do not end it with a period](https://cbea.ms/git-commit/#end).
* [Use the imperative mood in the subject line](https://cbea.ms/git-commit/#imperative).
* [Wrap the body at](https://cbea.ms/git-commit/#wrap-72) **88 characters**.
* [Use the body to explain what and why vs. how](https://cbea.ms/git-commit/#why-not-how).

In addition, try to make [atomic commits](https://www.freshconsulting.com/insights/blog/atomic-commits/) when possible.

#### Specifying the type of change

!!!note

    The stipulations below are based on experience, but are still evolving.
    This text is mainly here to provide a starting point for discussion with collaborators.
    TODO: Look into [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#specification) and see if we want to use/adapt their specification.

Specifying the type of change in a commit can be useful for several reasons:

- Understanding the changes of a commit.
- Where to (automatically) put the commit in the changelog, if at all.
- What to include in a support branch for a previous major release.
- Encouraging atomic commits.
- What the priority should be when reviewing open PRs. 

We use **exactly one leading** emoji per commit to indicate the type of change.
Some advantages:

- Only a single character needed!
  Save precious space in the subject line.
- A clear visual indicator of the type of change.
- Clearly separates type from scope/content.
- Language-agnostic.
- They look great. At least on macOS.

!!! important

    Although we are in favor of using emojis in the subject line, we do **not** allow emojis in the body.
    This makes it easier to `grep` for commit types.

| Emoji | Meaning                                                          | Similar to [Angular type](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) | In changelog summary?  |
| ----- | ---------------------------------------------------------------- | ----------------------------------------- | ------------------------- |
| 💥    | introduce a backward-incompatible (breaking) change / remove deprecated code | `\<type>!` (use `!` + `BREAKING CHANGE:`) | **Yes**                   |
| ✨    | introduce new features                                           | `feat`                                    | **Yes**                   |
| 👌    | improve an existing code/feature (no breaking)                   | `perf`/`feat`                             | **Yes**                   |
| 🐛    | fix a code bug                                                   | `fix`                                     | **Yes**                   |
| ❌    | mark code as deprecated (note removal version/replacement)       | `refactor`                                | **Yes**                   |
| 📦    | update or change a dependency                                    | `build`                                   | **Yes**                   |
| 📚    | add or adapt documentation                                       | `docs`                                    | No                        |
| 🔄    | refactor existing code with no behavior change                   | `refactor`                                | No                        |
| 🧪    | add or adapt tests                                               | `test`                                    | No                        |
| 🚀    | bump the package version for release                             | `chore`                                   | No                        |
| 🧹    | clean up comments / small formatting                             | `style`                                   | No                        |
| ⏪    | revert a previous commit                                         | `revert`                                  | No                        |
| 🔧    | devops-related changes (pre-commit, CI/CD, etc.)                 | `ci`                                      | No                        |
| 🐭    | minor changes (typos etc.; exclude from changelog)               | `chore`                                   | No                        |
| ❓    | anything not covered above (last resort)                         | `chore`                                   | No                        |

!!!note

    We are aware of other standards like [GitMoji](https://gitmoji.dev/), but limit the number in order to avoid choice overload.
    Too many options make it difficult for contributors to know all of them, makes changelogs too fragmented and leads to decision paralysis.
    Moreover, we avoid emojis that typically have width issues in some terminals.

!!!note

    Not everyone likes emojis. In the dropdown below you can find some common concerns.

    ??? "Common concerns"

        > Tooling can’t parse emojis.
        
        We haven't needed to use much tooling so far, and built our own for e.g. the changelog.

        > Search/grep is harder.
        
        You can grep for emojis too!
        Moreover, the body of the commit should not contain any emojis, so it's quite easy to look for commit types:

            git log | grep '[💥✨👌🐛❌📦]'

        > Accessibility / screen readers read ‘sparkles’
        
        This is a fair point.
        In case we start working with collaborators that rely on such tools we will adapt.

        > Rendering/width issues in some terminals.
       
        We selected emojis with default emoji presentation (no variation selector), which render correctly in modern terminals.

        > Ambiguity / overchoice
        
        This just depends on conventions.
        You can have _more_ ASCII keywords to choose from. If we keep a small, fixed set, like the one above, this is not an issue.

        > Not serious/professional.

        The icon is metadata, not decoration.
        It improves triage and doesn’t replace clear subjects/bodies.

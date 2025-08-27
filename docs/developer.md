# Developer Guide

!!! Info

    Just to clarify: this guide is for developers of the `copier` template, not Python package developers.

This template package uses several [Hatch environments](https://hatch.pypa.io/latest/environment/) to execute developer tasks or "scripts".
To see the environments and their corresponding scripts, run:

    hatch env show

You can also find the definition of all the environments and their script in the `pyproject.toml`.

!!! Info

    Hatch creates its own isolated Python environments behind the scenes to run the corresponding scripts. This means your current environment will not be affected.

## Default - Template scripts

The default Hatch environment defines a set of scripts related to the template, for example:

    hatch run copy <target_directory>

Will copy the fully rendered template as the `py-package` package in the `<target_directory>`.
Other scripts for the default environment:

* `check`: Copy/Update the template in the `.tmp` directory and check the rendered files by linting them with `hatch fmt -l`.
* `clean`: Remove the `.tmp` directory and any Ruff caches.
* `docs`: Copy/Update the template in the `.tmp` directory and serve the documentation with `myst start`.
* `install`: Copy/Update the template in the `.tmp` directory and install it with `uv pip install`.

## Documentation

The `docs` Hatch environment can be used to `build`, `serve` and `deploy` the documentation of this template package (which you are reading right now).
To run these scripts, you need to specify the `docs` environment in the `hatch run` command:

    hatch run docs:serve

!!! Warning

    The `docs:deploy` script will use `mkdocs gh-deploy` to deploy the documentation as a GitHub Pages website.
    This should rarely be done manually, since we have a GitHub Action set up to do this.

## Release

To make a new release of the template package, simply tag the commit you want to release:

    git tag -a v0.3.0 -m '🚀 Release `v0.3.0`'

And then push the tag to the remote, here named `origin`:

    git push origin --tags

You can the go to the [Github releases](https://github.com/mbercx/python-copier/releases) and make a new release based on the new tag.

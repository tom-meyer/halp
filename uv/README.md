# Basics

uv does "just in time" resolution of python versions, so explicity
installing a specific version is not neccessary. For example, run
a REPL with the default python:

    uv run python

Or fire up 3.9 (it will be downloaded if not installed):

    uv run -p 3.9 python

But a specific version can still be explicitly installed:

    uv python install 3.13.2

Show the local/installed versions (managed by uv as well as system installs):

    uv python list
    uv python list --all-versions
    uv python find 3.11  # show the path of a specific version (if present)

Requesting a version for most uv commands is possible with the `--python`/`-p` flag,
but it will also respect a `.python-version` file as well as the `UV_PYTHON` env
variable.


## uvx

The uvx command invokes a tool without installing it.

    uvx ruff
    uv tool run ruff  # this does the same

Actually install a tool:

    uv tool install ruff

## uv run

By default, `uv run` tries hard to discover a project, but sometimes isolation is desired
even when a project is present. A handly invocation for isolated ad-hoc environment:

    uv run ---isolated -no-project --with pyjwt,boto3 --directory ~/projects/auth python3

# build

[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/pypa/build/main.svg)](https://results.pre-commit.ci/latest/github/pypa/build/main)
[![CI test](https://github.com/pypa/build/actions/workflows/test.yml/badge.svg)](https://github.com/pypa/build/actions/workflows/test.yml)
[![codecov](https://codecov.io/gh/pypa/build/branch/main/graph/badge.svg)](https://codecov.io/gh/pypa/build)

[![Documentation Status](https://readthedocs.org/projects/pypa-build/badge/?version=latest)](https://build.pypa.io/en/latest/?badge=latest)
[![PyPI version](https://badge.fury.io/py/build.svg)](https://pypi.org/project/build/)
[![Discord](https://img.shields.io/discord/803025117553754132?label=Discord%20chat%20%23build)](https://discord.gg/pypa)

A simple, correct Python build frontend.

See the [documentation](https://build.pypa.io) for more information.

### Installation

`build` can be installed via `pip` or an equivalent via:

```console
$ pip install build
```

### Usage

```console
$ python -m build
```

This will build the package in an isolated environment, generating a
source-distribution and wheel in the directory `dist/`. See the
[documentation](https://build.pypa.io) for full information. Build is also
available via the command line as `pyproject-build` once installed.

### Common arguments

- `--sdist` (`-s`): Produce just an SDist
- `--wheel` (`-w`): Produce just a wheel
- `-C<option>=<value>`: A Config-setting, the PEP 517 way of passing options to a backend. Can be passed multiple times. Matching options will make a list. Note that setuptools has very limited support.
- `--config-json=<value>`: An alternative way to pass in complex config settings as JSON strings. Can't be used with `-C`.
- `--installer`: Pick an installer for the isolated build (`pip` or `uv`).
- `--no-isolation` (`-n`): Disable build isolation.
- `--skip-dependency-check` (`-x`): Disable dependency checking when not isolated; this should be done if some requirements or version ranges are not required for non-isolated builds.
- `--outdir` (`-o`): The output directory (defaults to `dist`)

Some common combinations of arguments:

- `--sdist --wheel` (`-sw`): Produce and SDist and a wheel, both from the source distribution. The default (if no flag is passed) is to build an SDist and then build a wheel _from_ the SDist.
- `-nx`: Disable build isolation and dependency checking. Identical to pip and uv's `--no-build-isolation` flag.

### Integration with other tools

#### pipx

If you use [pipx][], such as in GitHub Actions, the following command will download
and run build in one step:

```console
$ pipx run build
```

#### uv

If you want to use [uv][] to speed up the virtual environment creation, you can
use `--installer=uv`. You can get a Python wheel for `uv` with the `[uv]`
extra. For example, using pipx like above:

```console
$ pipx run 'build[uv]' --installer uv
```

If you already have uv, you don't need the extra. For example:

```console
$ uvx --from build pyproject-build --installer uv
```

#### cibuildwheel

If you are using [cibuildwheel][], build is integrated and the default builder in 3.0+. If you want to use `uv` as the installer, you can use:

```toml
[tool.cibuildwheel]
build-frontend = "build[uv]"
```

(Be sure to pre-install uv before running cibuildwheel for this one!)

#### Conda-forge

On conda-forge, this package is called [python-build][].

### Code of Conduct

Everyone interacting in the build's codebase, issue trackers, chat rooms, and mailing lists is expected to follow
the [PSF Code of Conduct].

[psf code of conduct]: https://github.com/pypa/.github/blob/main/CODE_OF_CONDUCT.md
[pipx]: https://pipx.pypa.io
[uv]: https://docs.astral.sh/uv/
[cibuildwheel]: https://cibuildwheel.pypa.io
[python-build]: https://github.com/conda-forge/python-build-feedstock

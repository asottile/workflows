[![build status](https://github.com/asottile/workflows/actions/workflows/main.yml/badge.svg)](https://github.com/asottile/workflows/actions/workflows/main.yml)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/asottile/workflows/main.svg)](https://results.pre-commit.ci/latest/github/asottile/workflows/main)

workflows
=========

reusable github workflows / actions

## job templates

### .github/workflows/tox.yml

_new in v1.0.0_

this job template will install python and invoke tox

#### parameters

- `env`: (json list of strings) the list of `tox` environment names to run
- `os`: (default: `ubuntu-latest`) passed through to [`runs-on`]
- `arch`: (json list of strings, default: '["x64"]') only used on windows to
  select the python executable
- `wheel-tags`: (default: `false`) whether to make a `wheels` artifact on tags
- `submodules`: (default: `false`) _new in v1.1.0_ passed along to
  [`actions/checkout`]

this action auto-detects python versions via the env name.  here are some
examples:

- `py310`: will run with python 3.10
- `py310-wat`: will also run with python 3.10
- `pypy3`: will run using pypy 3.9
- `wat`: will run with python 3.11
- `py312`: will install nightly 3.12 from [deadsnakes] and use that

[`runs-on`]: https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on
[deadsnakes]: https://github.com/deadsnakes/action
[`actions/checkout`]: https://github.com/actions/checkout

#### example

```yaml
jobs:
  main:
    uses: asottile/workflows/.github/workflows/tox.yml@v1.5.0
    with:
      env: '["py37", "py38", "pypy3"]'
```

## actions

### .github/actions/latest-git

_new in v1.2.0_

install the latest version of `git`

#### example

```yaml
    steps:
    - uses: asottile/workflows/.github/actions/latest-git@v1.5.0
```

### .github/actions/fast-checkout

_new in v1.3.0_

a replacement for `actions/checkout` that is [way less slow]

[way less slow]: https://github.com/actions/checkout/issues/1150

#### example

```yaml
    steps:
    - uses: asottile/workflows/.github/actions/fast-checkout@v1.5.0
```

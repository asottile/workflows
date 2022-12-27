workflows
=========

reusable github workflows / actions

## job templates

### .github/workflows/tox.yml

_new in v0.0.1_

this job template will install python and invoke tox

#### parameters

- `env`: (json list of strings) the list of `tox` environment names to run
- `os`: (default: `ubuntu-latest`) passed through to [`runs-on`]
- `arch`: (json list of strings, default: '["x64"]') only used on windows to
  select the python executable
- `wheel-tags`: (default: `false`) whether to make a `wheels` artifact on tags

this action auto-detects python versions via the env name.  here are some
examples:

- `py310`: will run with python 3.10
- `py310-wat`: will also run with python 3.10
- `pypy3`: will run using pypy 3.9
- `wat`: will run with python 3.11
- `py312`: will install nightly 3.12 from [deadsnakes] and use that

[`runs-on`]: https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on
[deadsnakes]: https://github.com/deadsnakes/action

#### example

```yaml
jobs:
  main:
    uses: asottile/workflows/.github/workflows/tox.yml@v0.0.1
    with:
      env: '["py37", "py38", "pypy3"]'
```

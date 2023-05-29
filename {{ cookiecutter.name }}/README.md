# {{ cookiecutter.name }} server

{{ cookiecutter.description }}

## Running unit tests

```shell
tox -e py39
```

## Running integration tests

```shell
tox -e integration
```

## Linting code

### Run once:

```shell
tox -e linters
# or
pre-commit run --all-files
```

### Automatically run on `git commit`

```shell
pre-commit install
```
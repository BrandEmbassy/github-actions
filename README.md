# Reusable GitHub Workflows

Common reusable GitHub workflows that can be shared across Brand Embassy repositories.

For details how to build reusable workflows see
[GitHub documentation](https://docs.github.com/en/actions/using-workflows/reusing-workflows).

## Limitations

All reusable workflows have to meet the following requirements:

* be in the root of the `.github/workflows` directory;
* implement `on.workflow_call` event;
* the maximum of four levels of workflows nesting is currently supported;

For the most recent details, please, see the documentation.

## Workflow call example

```yaml
on:
  pull_request:
    branches:
      - master

jobs:
  reusable_test:
    name: test
    uses: BrandEmbassy/github-actions/.github/workflows/js-test.yml@master
    secrets:
      NPM_AUTH_TOKEN: ${{ secrets.NPM_AUTH_TOKEN }}
```

## Workflow sections

* [JS workflows](./README_JS.md)

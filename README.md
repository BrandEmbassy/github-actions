# github-actions
Common reusable github wokflows
https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Limitations
All reusable workflows have to meet these requirements
* be in the root of the .github/workflows directory
* begin with ```on:
  workflow_call:```


## Workflows examples

### Run tests

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

### Publish to Github Package Registry

It will first install dependencies with `yarn`, then trigger `yarn build`, and finally pushes to the GPR.

```yaml
on:
  push:
    tags:
      - '**'

jobs:
  publish-gpr:
    name: Publish to Github Packages
    uses: BrandEmbassy/github-actions/.github/workflows/publish-gpr.yml@master
    secrets:
      NPM_AUTH_TOKEN: ${{ secrets.NPM_AUTH_TOKEN }}
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
``` 

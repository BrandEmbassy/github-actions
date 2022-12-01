# JS common workflows

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

### Node setup and install
```yaml
on:
...

jobs:
  job_name:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: BrandEmbassy/github-actions/.github/workflows/js-node-setup.yml@master
      - uses: BrandEmbassy/github-actions/.github/workflows/js-yarn-install.yml@master
```

### Run lint
run linter (yarn lint) with all checkout and setup steps
```yaml
on:
...

jobs:
  job_name:
    runs-on: ubuntu-latest
    steps:
      - uses: BrandEmbassy/github-actions/.github/workflows/js-lint.yml@master
```

By default, there is maxWarnings set to 0. To override this behavior, you need to pass maxWarnings value

```yaml
jobs:
  job_name:
    runs-on: ubuntu-latest
    with: 
      maxWarnings: 10
    steps:
      - uses: BrandEmbassy/github-actions/.github/workflows/js-lint.yml@master
```

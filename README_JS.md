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

### Run lint
run linter (yarn lint) with all checkout and setup steps
```yaml
on:
...

jobs:
  lint:
    name: Lint codestyle
    uses: BrandEmbassy/github-actions/.github/workflows/js-lint.yml@master
```

By default, there is maxWarnings set to 0. To override this behavior, you need to pass maxWarnings value

```yaml
jobs:
  lint:
    name: Lint codestyle with max warnings
    uses: BrandEmbassy/github-actions/.github/workflows/js-lint.yml@master
    with:
      maxWarnings: 42
    secrets:
      NPM_AUTH_TOKEN: ${{ secrets.NPM_AUTH_TOKEN }}
```

### Version increase

Create new version

```yaml
jobs:
  version:
    name: Create new version
    uses: BrandEmbassy/github-actions/.github/workflows/js-version.yml@master
  sectets:
    NPM_AUTH_TOKEN: ${{ secrets.NPM_AUTH_TOKEN }}
```
with version type (default: minor)

```yaml
jobs:
  version:
    name: Create new patch version
    uses: BrandEmbassy/github-actions/.github/workflows/js-version.yml@master
    with:
      VERSION_TYPE: patch
    sectets:
      NPM_AUTH_TOKEN: ${{ secrets.NPM_AUTH_TOKEN }}
```

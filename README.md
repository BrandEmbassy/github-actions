# github-actions
Common reusable github wokflows
https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Limitations
All reusable workflows have to meet these requirements
* be in the root of the .github/workflows directory
* begin with ```on:
  workflow_call:```


## Example usage

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

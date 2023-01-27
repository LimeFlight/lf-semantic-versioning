# LimeFlight Semantic Versioning Action

Based on [LimeFlight/openapi-diff](https://github.com/LimeFlight/openapi-diff).

This GitHub Action will read the labels of your pull request and fetch the latest prerelease version. It will bump the version number according to those.

`fix` -  patch version bump  
`compatible` - minor version bump  
`breaking` - major version bump  

## Usage

Your workflow needs to check out a repo and then call this action. You have to set the ref input in the checkout action, otherwise it will use the default branch.

### Inputs:

- `github-token` _(required)_: Must be in form `${{ github.token }}` or `${{ secrets.GITHUB_TOKEN }}`; This token is used to add labels and comments to pull requests. It is built into Github Actions and does not need to be manually specified in your secrets store. [More Info](https://help.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#github-context)

### Example:

```yaml
name: Semantic Versioning
on: [pull_request]

jobs:
  versioning:
    runs-on: ubuntu-latest
    steps:
      # Check out the repository
      - uses: actions/checkout@v3
        with:
          ref: ${{ github.head_ref }}
          token: ${{ secrets.SEMANTIC_VERSIONING_CI }}
      # Read and validate the labels from the pull request
      - name: LimeFlight Semantic Versioning
        uses: LimeFlight/lf-semantic-versioning@v1.0.0
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

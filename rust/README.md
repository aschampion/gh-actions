# Rust Workflows

### Example `.github/workflows/ci.yml`
```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    uses: aschampion/gh-actions/.github/workflows/rust-test.yml@v0
    with:
      msrv: 1.56

  publish:
    uses: aschampion/gh-actions/.github/workflows/rust-publish.yml@v0
    needs: [test]
    if: github.event_name == 'push' && contains(github.ref, 'refs/tags/v')
    secrets: inherit

  dist:
    uses: aschampion/gh-actions/.github/workflows/rust-dist.yml@v0
    needs: [publish]
    if: github.event_name == 'push' && contains(github.ref, 'refs/tags/v')
    with:
      proj_name: example-bin
    secrets: inherit
```

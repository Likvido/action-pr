# Likvido github action for pr checks

```
jobs:
  pr:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Build & test
        uses: likvido/action-pr@v1
        with:
          working-directory: src
          docker-file: src/Likvido.Project/Dockerfile
          docker-file-target: test
```


# Releasing new version

Either create the new release + new version tag directly in the Github UI, or create it like this:

1. Commit and push your changes
2. Create a new tag: `git tag -a -m "Description of this release" <version>`
3. Push the tag: `git push --follow-tags`

## Example

```
git tag -a -m "First version" v1
git push --follow-tags
```

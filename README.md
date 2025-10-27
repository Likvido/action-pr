# Likvido github action for pr checks

This action builds Docker images to a specified target for pull request validation.

## Features

- ✅ Builds Docker images to a specific target stage for testing
- ✅ Optional registry-based build cache for faster PR builds

## Usage

### Basic Usage

```yaml
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

### With Registry Build Cache

To enable faster builds using Azure Container Registry as a build cache:

```yaml
- name: Build & test
  uses: likvido/action-pr@v1
  with:
    working-directory: src
    docker-file: src/Likvido.Project/Dockerfile
    docker-file-target: test
    use-registry-cache: 'true'
    app-name: my-app
    acr-registry: likvido
    azure-service-principal-id: ${{ secrets.AZURE_SERVICE_PRINCIPAL_ID }}
    azure-service-principal-password: ${{ secrets.AZURE_SERVICE_PRINCIPAL_PASSWORD }}
```

The cache is scoped per application using the `app-name` input.

## Inputs

See `action.yml` for all available inputs.


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

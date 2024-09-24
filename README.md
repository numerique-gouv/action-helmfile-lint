# Action-helmfile-lint

**action-helmfile-lint** is a github action that lint configuration for all environments in a helmfile.yml

## Inputs

```yaml
- name: Run helmfile lint on all environments
  uses: numerique-gouv/action-helmfile-lint@main
  with:
    #Github app id to be able to clone repos
    app-id: ${{ secrets.APP_ID }}
    #Age private key to decrypted sops file
    age-key: ${{ secrets.SOPS_PRIVATE }}
    #Private key of the github app
    private-key: ${{ secrets.PRIVATE_KEY }}
    #Path where is the helmfile.yaml
    helmfile-src: "src/helm"
    #Github repos for the token
    repositories: "people,secrets"
```

## Exemple

```yaml
name: Helmfile lint
run-name: Helmfile lint

on:
  pull_request:
    branches:
      - 'main'

jobs:
  helmfile-lint:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/helmfile/helmfile:latest
    steps:
      -
        uses: numerique-gouv/action-helmfile-lint@main
        with:
          app-id: ${{ secrets.APP_ID }}
          age-key: ${{ secrets.SOPS_PRIVATE }}
          private-key: ${{ secrets.PRIVATE_KEY }}
          helmfile-src: "src/helm"
          repositories: "people,secrets"
```

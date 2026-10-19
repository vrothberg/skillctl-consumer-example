# skillctl-consumer-example

Example consumer repository demonstrating how [skillctl](https://github.com/vrothberg/skillctl) tracks OCI-based AI agent skills and integrates with Renovate for automated version updates.

## How it works

1. `skillctl.yaml` pins the example skill to a specific OCI tag and digest
2. Renovate detects the OCI image reference and monitors for new tags
3. When a new version is pushed to the registry, Renovate opens a PR to bump the tag
4. CI runs `skillctl pull` to update the extracted skill files

## Setup

```console
$ skillctl init
$ skillctl pull quay.io/vrothberg/skillctl-example-skill:v1.0.0
```

## Simulating an update

In the [skillctl](https://github.com/vrothberg/skillctl) repo:

```console
# Bump the counter
echo 2 > hack/example-skill/counter.txt

# Build and push a new version
./hack/build-example-skill.sh v1.0.1
```

Renovate will detect the new tag and open a PR in this repo to update `skillctl.yaml`.

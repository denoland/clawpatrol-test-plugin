# clawpatrol-test-plugin

A small clawpatrol plugin used to exercise GitHub-based plugin
distribution: semver resolution against release tags, checksum
verification, and build-provenance attestation.

It is the [example plugin][ex] from the clawpatrol SDK, built and
released here as a standalone module. It declares one credential type
(`example_magic_token`), one tunnel type (`example_passthrough`), and
three endpoint types (`example_https`, `example_smtp`, `example_echo`).

[ex]: https://github.com/denoland/clawpatrol/tree/main/pluginsdk/example

## Using it

```hcl
plugin "example" {
  source  = "github.com/denoland/clawpatrol-test-plugin"
  version = "~> 0.2"
}
```

Then `clawpatrol plugins install <config.hcl>`.

## Releasing

Pushing a `v*` tag runs `.github/workflows/release.yml`, which builds
every platform, packages each as
`clawpatrol-test-plugin_<version>_<os>_<arch>.tar.gz` plus a
`SHA256SUMS`, attaches a build-provenance attestation, and publishes the
release — the layout clawpatrol downloads and verifies.

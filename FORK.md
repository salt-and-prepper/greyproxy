# salt-and-prepper/greyproxy

A fork of [GreyhavenHQ/greyproxy](https://github.com/GreyhavenHQ/greyproxy)
that keeps greyproxy's dependencies current. Upstream's last release (v0.4.5,
2026-06-02) carries known high-severity advisories in its Go toolchain and
`golang.org/x` modules, and its release binaries are UPX-packed, which hides
their build information from vulnerability scanners.

What differs from upstream:

- **Dependencies:** Go toolchain and `golang.org/x/*` modules updated (see
  the commit log). No functional changes.
- **Releases:** tags `v<upstream version>-ellwood.<n>` build static
  `linux/amd64` and `linux/arm64` binaries with
  [`.github/workflows/release.yml`](.github/workflows/release.yml). They are
  not UPX-packed, and each archive has a build provenance attestation:

  ```sh
  gh attestation verify greyproxy_<version>_linux_amd64.tar.gz --repo salt-and-prepper/greyproxy
  ```

  Archive layout matches upstream's (`greyproxy`, `LICENSE`, `README.md` at
  the top level).
- **Workflows:** upstream's goreleaser, nightly, docs-notification and
  container image workflows are removed; `ci.yml` is unchanged.

Consumers: the apps-catalog `apps/paperclip` egress lock and the
coder-templates `greywall` module.

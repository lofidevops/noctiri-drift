# Noctiri Drift &nbsp; [![build badge](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml/badge.svg)](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml)

A Fedora Atomic custom image combining the [Niri](https://niri-wm.github.io/niri/) compositor and the [Noctalia](https://noctalia.dev) shell.

**Base:** Fedora Atomic ([Universal Blue](https://universal-blue.org/) `base-main`)

**Key packages:**
- [niri](https://niri-wm.github.io/niri/) — scrollable-tiling Wayland compositor
- [noctalia-shell](https://noctalia.dev) — desktop shell for Niri
- [greetd](https://sr.ht/~kennylevinsen/greetd/) + [tuigreet](https://github.com/apognu/tuigreet) — login manager

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/lofidevops/noctiri-drift:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/lofidevops/noctiri-drift:latest
  ```
- Reboot again to complete the installation:
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If built on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/lofidevops/noctiri-drift
```

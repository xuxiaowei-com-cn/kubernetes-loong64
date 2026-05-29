# Kubernetes for LoongArch64

[English](README.md) | [中文](README-zh.md)

Build [Kubernetes](https://github.com/kubernetes/kubernetes) binaries for the **LoongArch64 (loong64)** architecture via CI/CD.

## How it works

A GitHub Actions workflow clones the specified Kubernetes version, applies a patch to enable loong64 compilation, and cross-compiles with `gcc-loongarch64-linux-gnu` in a Debian 13 container. Target platform: `linux/loong64`.

## Branch naming

Create a branch named `loong64/<kubernetes-version>` (e.g. `loong64/v1.36.1`) to trigger a build.

## Release

Push a tag matching `release-loong64/<kubernetes-version>/<sequence>` (e.g. `release-loong64/v1.36.1/alpha.1`) to publish a GitHub Release with the built binaries.

## License

[Apache License 2.0](LICENSE)

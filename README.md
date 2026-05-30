# Kubernetes for LoongArch64

[English](README.md) | [中文](README-zh.md)

Build [Kubernetes](https://github.com/kubernetes/kubernetes) binaries and Docker images for the **LoongArch64 (loong64)** architecture via CI/CD.

## How it works

A GitHub Actions workflow clones the specified Kubernetes version, applies a patch to enable loong64 compilation, and cross-compiles with `gcc-loongarch64-linux-gnu` in a Debian 13 container. Target platform: `linux/loong64`.

## Branch naming

Create a branch named `loong64/<kubernetes-version>` (e.g. `loong64/v1.36.1`) to trigger a build.

## [Release](https://github.com/xuxiaowei-com-cn/kubernetes-loong64/releases)

Push a tag matching `release-loong64/<kubernetes-version>/<sequence>` (e.g. `release-loong64/v1.36.1/1-alpha.1`) to publish a GitHub Release with the built binaries.

The suffix in the sequence indicates the release stage:

| Suffix  | Stage         |
|---------|---------------|
| `alpha` | Internal beta |
| `beta`  | Public beta   |
| `rc`    | Pre-release   |
| (none)  | Stable        |

## Verify releases

Releases are signed with GPG. Download the public key from [keys.openpgp.org](https://keys.openpgp.org) [F3693AB74BBA0D84C227AB34F3A4B5061568FC57](https://keys.openpgp.org/debug?q=F3693AB74BBA0D84C227AB34F3A4B5061568FC57)：

```shell
gpg --keyserver keys.openpgp.org --recv-keys F3693AB74BBA0D84C227AB34F3A4B5061568FC57
echo "F3693AB74BBA0D84C227AB34F3A4B5061568FC57:6:" | gpg --import-ownertrust
```

Each release includes a `signatures.tar.gz` containing detached signatures for all artifacts. To verify:

```shell
# Download signatures.tar.gz from the release, then:
tar -xzf signatures.tar.gz --strip-components=1
gpg --verify <file>.asc <file>
```

## License

[Apache License 2.0](LICENSE)

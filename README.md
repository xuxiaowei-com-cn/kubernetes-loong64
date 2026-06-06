# Kubernetes for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/Kubernetes%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=kubernetes&logoColor=white" alt="Kubernetes LoongArch64 龙芯架构发行版"></p>

Build [Kubernetes](https://github.com/kubernetes/kubernetes) binaries and Docker images for the **LoongArch64 (loong64)** architecture via CI/CD.

## How it works

A GitHub Actions workflow clones the specified Kubernetes version, applies a patch to enable loong64 compilation, and cross-compiles with `gcc-loongarch64-linux-gnu` in a Debian 13 container. Target platform: `linux/loong64`.

See [Discussion #6 — Why Use container: debian:13?](https://github.com/orgs/kubernetes-loong64/discussions/6) for the rationale behind the Debian 13 container choice.

## Branch naming

Push a branch named `loong64-<kubernetes-version>` (e.g. `loong64-v1.36.1`) to trigger a build.

## [Release](https://github.com/kubernetes-loong64/kubernetes-loong64/releases)

Push a tag matching `release-loong64-<kubernetes-version>+<sequence>` (e.g. `release-loong64-v1.36.1+1-alpha.1`) to publish a GitHub Release with the built binaries and Docker images.

The suffix in the sequence indicates the release stage:

| Suffix  | Stage         |
|---------|---------------|
| `alpha` | Internal beta |
| `beta`  | Public beta   |
| `rc`    | Pre-release   |
| (none)  | Stable        |

## Release artifacts

Each release includes the following files:

| File                          | Type          |
|-------------------------------|---------------|
| `apiextensions-apiserver`     | Binary        |
| `ginkgo`                      | Binary        |
| `go-runner`                   | Binary        |
| `kubeadm`                     | Binary        |
| `kube-aggregator`             | Binary        |
| `kube-apiserver`              | Binary        |
| `kube-controller-manager`     | Binary        |
| `kubectl`                     | Binary        |
| `kubectl-convert`             | Binary        |
| `kubelet`                     | Binary        |
| `kube-log-runner`             | Binary        |
| `kubemark`                    | Binary        |
| `kube-proxy`                  | Binary        |
| `kube-scheduler`              | Binary        |
| `mounter`                     | Binary        |
| `conformance-loong64.tar`     | Image tarball |
| `kube-apiserver.tar`          | Image tarball |
| `kube-controller-manager.tar` | Image tarball |
| `kubectl.tar`                 | Image tarball |
| `kube-proxy.tar`              | Image tarball |
| `kube-scheduler.tar`          | Image tarball |
| `pause-loong64.tar`           | Image tarball |

Each file has a corresponding `.asc` detached GPG signature.

## Docker images

Docker images are pushed to:

- [![kubernetesloong64/kube-apiserver](https://img.shields.io/docker/v/kubernetesloong64/kube-apiserver?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fkube-apiserver)](https://hub.docker.com/r/kubernetesloong64/kube-apiserver/tags)
- [![kubernetesloong64/kube-controller-manager](https://img.shields.io/docker/v/kubernetesloong64/kube-controller-manager?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fkube-controller-manager)](https://hub.docker.com/r/kubernetesloong64/kube-controller-manager/tags)
- [![kubernetesloong64/kube-scheduler](https://img.shields.io/docker/v/kubernetesloong64/kube-scheduler?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fkube-scheduler)](https://hub.docker.com/r/kubernetesloong64/kube-scheduler/tags)
- [![kubernetesloong64/kube-proxy](https://img.shields.io/docker/v/kubernetesloong64/kube-proxy?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fkube-proxy)](https://hub.docker.com/r/kubernetesloong64/kube-proxy/tags)
- [![kubernetesloong64/kubectl](https://img.shields.io/docker/v/kubernetesloong64/kubectl?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fkubectl)](https://hub.docker.com/r/kubernetesloong64/kubectl/tags)
- [![kubernetesloong64/pause](https://img.shields.io/docker/v/kubernetesloong64/pause?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fpause)](https://hub.docker.com/r/kubernetesloong64/pause/tags)
- [![kubernetesloong64/conformance](https://img.shields.io/docker/v/kubernetesloong64/conformance?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fconformance)](https://hub.docker.com/r/kubernetesloong64/conformance/tags)

| Image                                       | Description             |
|---------------------------------------------|-------------------------|
| `kubernetesloong64/kube-apiserver`          | kube-apiserver          |
| `kubernetesloong64/kube-controller-manager` | kube-controller-manager |
| `kubernetesloong64/kube-scheduler`          | kube-scheduler          |
| `kubernetesloong64/kube-proxy`              | kube-proxy              |
| `kubernetesloong64/kubectl`                 | kubectl                 |
| `kubernetesloong64/pause`                   | Pause container         |
| `kubernetesloong64/conformance`             | Conformance             |

All images are available under [kubernetesloong64](https://hub.docker.com/u/kubernetesloong64).

## Verifying releases

- Releases are signed with GPG.
- Download the public key from [keys.openpgp.org](https://keys.openpgp.org).
- Fingerprint: [FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)
- [Manual download](https://keys.openpgp.org/vks/v1/by-fingerprint/FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

Or download the key file manually and import it:

```shell
gpg --import /tmp/xxx
```

Each release artifact has a corresponding `.asc` detached signature. To verify, download both the file and its `.asc` signature from the release, then:

```shell
gpg --verify <file>.asc <file>
```

## License

[Apache License 2.0](LICENSE)

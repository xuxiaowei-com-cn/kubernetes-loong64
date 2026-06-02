# Kubernetes for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/Kubernetes%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=kubernetes&logoColor=white" alt="Kubernetes LoongArch64 龙芯架构发行版"></p>

通过 CI/CD 构建 [Kubernetes](https://github.com/kubernetes/kubernetes) 的 **LoongArch64 (loong64)** 架构二进制文件和 Docker 镜像。

## 工作原理

GitHub Actions 工作流克隆指定的 Kubernetes 版本，打上 loong64 适配补丁，在 Debian 13 容器中使用 `gcc-loongarch64-linux-gnu` 交叉编译。目标平台：`linux/loong64`。

关于 Debian 13 容器选型的理由，详见 [Discussion #6 — 为什么使用 container: debian:13？](https://github.com/orgs/kubernetes-loong64/discussions/6)。

## 分支命名

创建 `loong64/<kubernetes 版本>` 格式的分支（如 `loong64/v1.36.1`）即可触发构建。

## [发布](https://github.com/xuxiaowei-com-cn/kubernetes-loong64/releases)

推送 `release-loong64/<kubernetes 版本>/<序号>` 格式的标签（如 `release-loong64/v1.36.1/1-alpha.1`）即可自动创建 GitHub Release 并上传构建产物。

后缀表示发布阶段：

| 后缀      | 阶段   |
|---------|------|
| `alpha` | 内测版  |
| `beta`  | 公测版  |
| `rc`    | 预发布版 |
| （无后缀）   | 正式版  |

## 验证发布

- 发布文件使用 GPG 签名。
- 从 [keys.openpgp.org](https://keys.openpgp.org) 下载公钥。
- [FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

每个发布产物都有对应的 `.asc` 分离签名。验证时，从发布页面下载文件和对应的 `.asc` 签名文件，然后：

```shell
gpg --verify <文件>.asc <文件>
```

## 许可证

[Apache License 2.0](LICENSE)

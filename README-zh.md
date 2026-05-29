# Kubernetes for LoongArch64

[English](README.md) | [中文](README-zh.md)

通过 CI/CD 构建 [Kubernetes](https://github.com/kubernetes/kubernetes) 的 **LoongArch64 (loong64)** 架构二进制文件。

## 工作原理

GitHub Actions 工作流克隆指定的 Kubernetes 版本，打上 loong64 适配补丁，在 Debian 13 容器中使用 `gcc-loongarch64-linux-gnu` 交叉编译。目标平台：`linux/loong64`。

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

## 许可证

[Apache License 2.0](LICENSE)

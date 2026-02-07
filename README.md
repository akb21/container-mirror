# Container Mirror

这是一个基于 GitHub Actions 的容器镜像镜像工具，旨在自动将 Docker Hub 上的镜像同步到 GitHub Container Registry (GHCR)。

## 项目初衷

通过 GitHub Actions 定时将镜像镜像到 GHCR。

## 工作原理

项目使用 GitHub Actions 工作流：
1. **定时触发**：每天午夜自动运行。
2. **手动触发**：支持通过 `workflow_dispatch` 手动启动镜像任务。
3. **镜像流程**：
   - 从 Docker Hub 拉取 (Pull) 指定镜像和标签。
   - 重新打标签 (Retag) 为 GHCR 格式。
   - 推送 (Push) 到项目的 GHCR 仓库。

## 当前镜像列表

| 镜像名称 | 来源镜像 | 目标镜像 (GHCR) | 标签 (Tag) |
| :--- | :--- | :--- | :--- |
| AdGuard Home | `adguard/adguardhome` | `ghcr.io/${{ github.repository_owner }}/adguardhome` | `latest` |
| Grafana | `grafana/grafana` | `ghcr.io/${{ github.repository_owner }}/grafana` | `main` |
| Portainer CE | `portainer/portainer-ce` | `ghcr.io/${{ github.repository_owner }}/portainer-ce` | `lts` |

## 如何添加新镜像

1. 在 `.github/workflows/` 目录下参考现有文件创建一个新的 `.yml` 文件。
2. 建议命名格式为 `mirror-<image-name>.yml`。
3. 修改 `env` 部分的配置：
   ```yaml
   env:
     IMAGE_NAME: 原始镜像名称
     TARGET_IMAGE: ghcr.io/${{ github.repository_owner }}/目标镜像名
     TAG: 镜像标签
   ```
4. 提交更改后，GitHub Actions 将会自动识别并运行。

## 许可证

MIT License

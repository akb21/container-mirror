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

## 如何添加新镜像

1. 编辑 `.github/workflows/mirror.yml` 文件。
2. 在 `jobs.mirror.strategy.matrix.include` 列表中添加新镜像配置：
   ```yaml
   - src: 原始镜像名称 (例如: library/nginx)
     dst: 目标镜像名称 (例如: nginx)
     tag: 镜像标签 (例如: alpine)
   ```
3. 提交更改后，GitHub Actions 将会自动识别并运行。

## 许可证

MIT License

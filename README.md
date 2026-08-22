# flux-panel-node-assets

`flux-panel-node-assets` 是 `flux-panel_rev` 的节点资源仓库，只保存节点安装脚本、校验文件和多架构二进制。

## 项目功能

- 提供节点安装脚本 `install.sh`
- 提供 `SHA256SUMS` 校验文件
- 提供 `amd64`、`arm64`、`armv7`、`armv6` 节点二进制
- 供面板和节点安装器直接拉取资源

## 部署教程

直接使用下面的命令安装节点：

```bash
curl -L https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/install.sh -o install.sh && chmod +x install.sh && sudo ./install.sh install
```

资源目录：

- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/install.sh`
- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/releases/SHA256SUMS`
- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/releases/gost-linux-amd64`
- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/releases/gost-linux-arm64`
- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/releases/gost-linux-armv7`
- `https://raw.githubusercontent.com/w243420707/flux-panel-node-assets/refs/heads/main/releases/gost-linux-armv6`

## 更新日志

### 1.0.0 - 2026-08-22

- 首次独立发布节点资源仓库。
- 节点安装脚本默认优先使用本仓库资源，保留面板资源作为兜底。

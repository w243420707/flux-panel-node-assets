# flux-panel-node-assets

`flux-panel-node-assets` 是 `flux-panel_rev` 的节点资源仓库，只保存节点安装脚本、校验文件和多架构二进制。

## 项目功能

- 提供节点安装脚本 `install.sh`
- 提供 `SHA256SUMS` 校验文件
- 提供 `amd64`、`arm64`、`armv7`、`armv6` 节点二进制
- 供面板和节点安装器直接拉取资源
- 安装或更新时安全检查 Swap；保留已有 Swap，无 Swap 时根据内存和磁盘空间自动创建

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

## 双仓库维护规则

- 本仓库与 `w243420707/flux-panel_rev` 配套使用。
- 只要涉及节点端安装脚本、更新逻辑、通信协议或节点二进制修改，必须同步更新主仓库和本仓库。
- `install.sh`、四种架构二进制和 `SHA256SUMS` 必须保持同一版本，并在发布前完成校验。
- 面板专属功能可以只更新主仓库；节点资源不能只留在主仓库。

## 更新日志

### 1.0.6 - 2026-09-20

- 节点二进制版本更新到 `3.1.6`，支持面板的手动与定时 VPS 重启指令。
- 复用加密 WebSocket，先发送接收回执，再执行固定的 `systemctl reboot`；不接受任意 shell 命令或参数，执行失败会回报面板。
- 限 root 运行、systemd 管理的 Linux VPS；容器内节点不支持重启宿主机。四种架构二进制与校验文件同步更新。

### 1.0.5 - 2026-08-30

- 节点上报内存已用和总量，面板可显示实际占用量，例如 `812M / 2G`。
- 节点二进制版本更新到 `3.1.5`。

### 1.0.4 - 2026-08-30

- 节点安装和更新时自动检查 Swap，已有 Swap 保持不变，不执行全局 `swapoff` 或删除操作。
- 无可用 Swap 时按内存自动创建 `2GB`、`4GB` 或 `8GB` Swap；磁盘不足或宿主机不允许时只警告，不中断安装。
- 默认设置 `vm.swappiness=10`，并增加单独的 `swap` 菜单操作用于检查或补充 Swap。
- 节点新增 Swap 使用率、已用容量和总容量上报，节点二进制版本更新到 `3.1.4`。

### 1.0.3 - 2026-08-30

- 节点运行配置改为原子写入，避免保存中断留下空的或半截 `gost.json`。
- 节点启动时自动备份损坏配置并恢复为空配置，避免 systemd 持续重启失败。
- WebSocket 增加 Ping/Pong 保活，不再因长时间没有面板命令而误判离线。
- 安装器兼容 SHA256 清单中普通文件名和 `*` 文件名前缀两种格式。
- 节点二进制版本更新到 `3.1.3`。

### 1.0.2 - 2026-08-22

- 安装脚本增加 GitHub/本地资源来源模式，节点更新时会沿用安装时的选择。

### 1.0.1 - 2026-08-22

- 增加双仓库同步维护规则，避免节点端修改只更新主仓库。

### 1.0.0 - 2026-08-22

- 首次独立发布节点资源仓库。
- 节点安装脚本默认优先使用本仓库资源，保留面板资源作为兜底。

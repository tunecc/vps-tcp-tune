# BBR v3 精简加速版（中国大陆优化）v6.0.0

**只做一件事：XanMod 内核 + BBR v3 调优 + Realm timeout 修复。**

默认经 [proxyd.picpi.top](https://proxyd.picpi.top/) 加速关键下载（GitHub raw、XanMod 密钥/源、Speedtest CLI 等），失败自动直连回退。

> 由 Ultimate Edition 精简而来：**已移除** DNS 净化、代理部署、测速菜单、AI 工具箱、流量计费、一键 66 等全部无关功能。

---

## 一键安装（别名）

新机器若无 curl：

```bash
apt update -y && apt install curl -y
```

```bash
# 安装 bbr 别名（默认走 proxyd 拉主脚本）
bash install-alias.sh

source ~/.bashrc   # 或 source ~/.zshrc

bbr
```

本地直接运行：

```bash
chmod +x net-tcp-tune.sh
sudo bash net-tcp-tune.sh
```

---

## 推荐流程

1. **菜单 1**：安装 XanMod 内核 + BBR v3  
2. **必须重启** VPS  
3. **菜单 3**：BBR 直连/落地优化  
   - 小白：自动检测（Speedtest）  
   - 进阶：手动选带宽档（如 500M / 700M / 1G）  
   - 地区：亚太（标准缓冲）/ 美欧（大缓冲）  
4. 若使用 Realm 中转：**菜单 4**（原功能 6）

---

## 菜单

| 编号 | 功能 |
| :--: | --- |
| 1 | 安装/更新 XanMod 内核 + BBR v3 |
| 2 | 卸载 XanMod 内核 |
| 3 | BBR 直连/落地优化（智能带宽检测） |
| 4 | Realm 转发 timeout 修复（原编号 6） |
| 99 | 完全卸载脚本写入的配置/别名 |
| 0 | 退出 |

---

## 中国大陆加速（proxyd）

默认前缀：

```text
https://proxyd.picpi.top/https://<原始URL>
```

| 环境变量 | 含义 |
| --- | --- |
| `NETTCP_PROXYD=0` | 禁用 proxyd，全程直连 |
| `NETTCP_PROXYD_BASE=URL` | 更换加速节点根地址 |
| `NETTCP_NO_FALLBACK=1` | 禁止直连回退 |
| `NETTCP_SCRIPT_URL=URL` | 覆盖主脚本原始地址（文档/别名场景） |

示例：

```bash
NETTCP_PROXYD=0 sudo bash net-tcp-tune.sh
```

说明：

- 不修改系统全局 apt 源；仅本脚本写入的 XanMod 源可走 proxyd，失败回退官方 `deb.xanmod.org`
- Speedtest **测速流量本身**不走 proxyd（测的是真实链路）；仅 CLI 安装包下载走加速

---

## 命令行参数

```bash
sudo bash net-tcp-tune.sh -h        # 帮助
sudo bash net-tcp-tune.sh -v        # 版本
sudo bash net-tcp-tune.sh -i        # 非交互安装内核
sudo bash net-tcp-tune.sh --debug   # 调试日志
```

---

## 卸载

- **菜单 2**：卸载 XanMod 内核  
- **菜单 99**：清理本脚本写入的 sysctl / realm drop-in / bbr 别名 / 日志  
  - **不会**回滚 `/etc/realm/config.json`（避免误伤中转配置；备份见 `/root/.realm_fix_backup/`）  
- 别名卸载：`bash install-alias.sh uninstall`

---

## 已移除（不再提供）

DNS 净化、IPv6/优先级、临时 SOCKS5、虚拟内存独立菜单、Snell/Xray/SOCKS5/Sub-Store/反代、AI 工具箱、端口流量计费、各类 IP/回程/解锁检测、第三方脚本入口、一键全自动优化（原 66）。

完整历史实现见本地备份：`net-tcp-tune.sh.bak-full`（若存在）。

---

## 许可

见 `LICENSE`。

Sing-box 一键部署脚本（双栈 + REALITY）

支持 VLESS-TLS / VLESS-REALITY / Hysteria2
自动适配 IPv4 / IPv6 双栈
支持 域名 + Let's Encrypt 或 公网 IP + 自签证书
适合 新手一键部署 / 老手快速上线

✨ 功能特性

✅ 一键部署 sing-box

✅ 自动环境检测（root / IP / 端口 / 依赖）

✅ IPv4 + IPv6 双栈监听

✅ 三种协议同时运行：

VLESS TCP TLS

VLESS REALITY（Vision 流控）

Hysteria2（UDP）

✅ 支持两种模式：

域名模式（Let's Encrypt 正式证书）

IP 模式（自签证书 + 固定域名 www.epple.com）

✅ 自动生成：

UUID / 密码

REALITY 公私钥

节点 URI

二维码

订阅文件

✅ 自动配置防火墙（ufw）

✅ systemd 开机自启

📦 支持环境

系统：Ubuntu 20.04 / 22.04 / Debian 11 / 12 /...+

架构：x86_64 / ARM64

需要：

公网 IPv4（IPv6 可选）

root 权限

🚀 快速使用
1️⃣ 一键安装：
```
bash <(curl -Ls https://raw.githubusercontent.com/hooghub/updatensb/main/sb.sh)
```
2️⃣ 环境检查

脚本会自动检查：

root 权限

公网 IPv4 / IPv6

80 / 443 端口占用情况

缺失依赖并自动安装

确认无误后输入：

y

🔧 部署模式说明
模式 1：域名 + Let's Encrypt（推荐）

适合有域名的用户。

自动申请 ECC 证书

支持 IPv4 / IPv6

浏览器与客户端完全信任

你需要：

域名已解析到 VPS

80 / 443 端口未被占用

模式 2：公网 IP + 自签证书

适合 无域名 / 临时使用 / 测试环境。

使用固定域名：www.epple.com

SAN 自动包含：

公网 IPv4

公网 IPv6（如存在）

客户端需开启 insecure

🔑 协议与端口

脚本会提示你输入端口，支持 0 = 随机端口：

协议	IPv4	IPv6	说明
VLESS TLS	✔	✔	TCP + TLS
VLESS REALITY	✔	✔	Vision 流控
Hysteria2	✔	✔	UDP
🧠 REALITY 参数说明

部署时可自定义：

伪装站点（Handshake Server）
默认：www.speedtest.net

SNI
默认与伪装站点一致

脚本自动生成：

REALITY 公钥 / 私钥

Short ID

Vision 流控配置

📡 节点输出

部署完成后，终端会显示：

🔹 VLESS TLS 节点

URI

二维码

🔹 VLESS REALITY 节点

URI

二维码

🔹 Hysteria2 节点

URI

二维码

📄 订阅文件

自动生成订阅文件：

/root/singbox_nodes.json


内容示例：

vless://...
vless://...reality...
hysteria2://...


可直接导入支持文本订阅的客户端。

🔥 防火墙说明

如系统存在 ufw，脚本会自动放行：

TCP：80 / 443 / VLESS 端口

UDP：Hysteria2 端口

🛠 常用命令
# 查看状态
systemctl status sing-box

# 重启
systemctl restart sing-box

# 查看日志
journalctl -u sing-box -e

⚠️ 注意事项

JSON 不支持注释
脚本已自动移除 // 注释，避免 sing-box 启动失败

REALITY 不需要证书

自签模式客户端需开启 insecure

不要在已占用 443 的机器上直接运行



<h1 align="center">S-UI Clash</h1>

<p align="center">
  基于 <a href="https://github.com/Teminuosi/s-ui">Teminuosi/s-ui</a> 的二次开发版本，底层使用 <a href="https://github.com/SagerNet/sing-box">SagerNet/sing-box</a><br><br>
  <a href="https://github.com/fengyunzaidushi/s-ui-clash"><img alt="项目仓库" src="https://img.shields.io/badge/GitHub-fengyunzaidushi%2Fs--ui--clash-181717?style=flat-square&logo=github"></a>
  <a href="https://www.gnu.org/licenses/gpl-3.0.en.html"><img alt="License" src="https://img.shields.io/badge/license-GPL%20V3-blue.svg?longCache=true"></a>
</p>

<p align="center">
  一键安装 · 协议模板 · 中转管理 · 多服务器管理 · JSON / Clash 订阅规则模板
</p>

<p align="center">
  <a href="https://3yuedaohang.com/tms-download.html?ref=sui"><img alt="下载 TMS 客户端" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-TMS%20%E5%AE%A2%E6%88%B7%E7%AB%AF-2ea44f?style=for-the-badge&logo=windows&logoColor=white"></a>
  &nbsp;
  <a href="https://www.youtube.com/watch?v=bmcHIdvaic8&t=62s"><img alt="视频教程" src="https://img.shields.io/badge/%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B-YouTube-ff0000?style=for-the-badge&logo=youtube&logoColor=white"></a>
</p>

<p align="center">
  <a href="https://www.youtube.com/watch?v=bmcHIdvaic8&t=62s"><img src="https://img.youtube.com/vi/bmcHIdvaic8/maxresdefault.jpg" alt="TMS 客户端视频教程" width="720"></a><br>
  <sub>▶ 点击封面观看视频教程</sub>
</p>

---

## 项目关系

- **当前项目**：[fengyunzaidushi/s-ui-clash](https://github.com/fengyunzaidushi/s-ui-clash)
- **直接上游**：[Teminuosi/s-ui](https://github.com/Teminuosi/s-ui)
- **原始上游**：[alireza0/s-ui](https://github.com/alireza0/s-ui)
- **前端子模块**：[Teminuosi/s-ui-frontend](https://github.com/Teminuosi/s-ui-frontend)
- **内核**：[SagerNet/sing-box](https://github.com/SagerNet/sing-box)

本项目在保留上游 S-UI 面板能力的基础上，继续维护安装体验、协议快速创建、中转、多服务器管理，以及订阅规则模板等功能。项目内置的 [clash.yaml](clash.yaml) 和 [json.json](json.json) 会作为新安装实例的默认订阅规则模板。

> 仅供个人学习与交流，请遵守当地法律法规。请在充分测试后再用于生产环境。

## 快速安装

### Linux 全自动安装（默认推荐）

安装脚本默认是无人值守模式，会自动完成安装并生成随机管理员账号、密码、面板路径、可用端口和 API Token。安装结束时会打印访问信息。

```sh
bash <(curl -Ls https://raw.githubusercontent.com/fengyunzaidushi/s-ui-clash/main/install.sh)
```

### Linux 交互式安装

需要手动输入端口、路径或账号密码时，显式关闭自动模式：

```sh
SUI_AUTO=0 bash <(curl -Ls https://raw.githubusercontent.com/fengyunzaidushi/s-ui-clash/main/install.sh)
```

### 安装指定版本

```sh
bash <(curl -Ls https://raw.githubusercontent.com/fengyunzaidushi/s-ui-clash/main/install.sh) v1.4.2
```

版本号以当前仓库 Releases 中的 Tag 为准。

### Windows

1. 从 [当前项目 Releases](https://github.com/fengyunzaidushi/s-ui-clash/releases/latest) 下载 Windows 压缩包。
2. 解压后以管理员身份运行 `install-windows.bat`。

### Docker / 本地构建

```sh
git clone --recurse-submodules https://github.com/fengyunzaidushi/s-ui-clash
cd s-ui-clash
docker build -t s-ui-clash .
```

运行时至少映射面板端口和订阅端口，并持久化数据库与证书目录：

```sh
docker run -itd \
  -p 2095:2095 -p 2096:2096 \
  -v "$PWD/db:/app/db" \
  -v "$PWD/cert:/root/cert" \
  --name s-ui-clash --restart=unless-stopped \
  s-ui-clash
```

## 安装后的默认行为

| 项目 | 默认值 |
| --- | --- |
| 面板端口 | `2095`（自动安装会避让占用端口） |
| 面板路径 | `/app/`（自动安装会随机生成） |
| 订阅端口 | `2096`（自动安装会避让占用端口） |
| 订阅路径 | `/sub/` |
| 管理账号 | 自动安装随机生成 |
| API Token | 自动生成并在安装结束时打印 |
| JSON 订阅规则 | 自动填入 `json.json` 模板 |
| Clash 订阅规则 | 自动填入 `clash.yaml` 模板 |

升级时会保留已有账号、路径、端口和订阅设置。安装完成后可直接执行 `s-ui` 打开管理菜单。

如果安装中途失败，可使用不依赖已安装文件的彻底清理命令：

```sh
bash <(curl -Ls https://raw.githubusercontent.com/fengyunzaidushi/s-ui-clash/main/install.sh) purge
```

该命令会删除 S-UI 服务、数据库、程序文件和管理脚本；数据库删除后无法恢复，请先备份。

## 主要功能

- **一键协议模板**：VLESS + Reality、Hysteria2、TUIC、Trojan、AnyTLS，可自动创建入站、TLS 配置和客户端。
- **中转向导**：粘贴落地分享链接或 SOCKS5 地址，自动创建出站、入口和路由规则，并测试落地连通性。
- **多服务器管理**：通过 APIv2 Token 从一个面板切换管理多台 S-UI 服务器。
- **订阅规则模板**：默认提供 Clash YAML 和 sing-box JSON 规则模板；JSON 模板包含规则集、DNS 分流和应用／域名路由规则。
- **Clash 订阅选项**：支持禁用默认分组、将 `all` 展开为全部节点，以及默认启用 UDP。
- **分享与批量操作**：入站卡片二维码、订阅与链接批量导出、批量删除入站和中转。
- **面板维护**：Web 内版本检查与更新、随机凭据、API Token、端口冲突检测、安装失败清理和防火墙放行。
- **界面体验**：多语言、六套渐变皮肤、明暗主题和响应式管理界面。

## 支持的平台

| 平台 | 架构 | 状态 |
| --- | --- | --- |
| Linux | amd64 / arm64 / armv7 / armv6 / armv5 / 386 / s390x | ✅ |
| Windows | amd64 / 386 / arm64 | ✅ |
| macOS | amd64 / arm64 | 🚧 实验性 |

## 从源码构建

```sh
git clone --recurse-submodules https://github.com/fengyunzaidushi/s-ui-clash
cd s-ui-clash

# 前端
cd frontend
npm install
npm run build
cd ..

# 将前端静态文件复制到后端资源目录
rm -rf web/html/*
cp -R frontend/dist/* web/html/

go build -o sui main.go
./sui
```

前端目录是独立 Git 子模块；如果只需要构建后端，请确保 `web/html` 中已经存在前端构建产物。

## 环境变量

| 变量 | 取值 | 默认 |
| --- | --- | --- |
| `SUI_LOG_LEVEL` | `debug` / `info` / `warn` / `error` | `info` |
| `SUI_DEBUG` | `true` / `false` | `false` |
| `SUI_BIN_FOLDER` | 字符串 | `bin` |
| `SUI_DB_FOLDER` | 字符串 | `db` |
| `SINGBOX_API` | 字符串 | - |

## 致谢

- 当前项目：[fengyunzaidushi/s-ui-clash](https://github.com/fengyunzaidushi/s-ui-clash)
- 上游项目：[Teminuosi/s-ui](https://github.com/Teminuosi/s-ui)
- 原始项目：[alireza0/s-ui](https://github.com/alireza0/s-ui)
- 前端：[Teminuosi/s-ui-frontend](https://github.com/Teminuosi/s-ui-frontend)
- 内核：[SagerNet/sing-box](https://github.com/SagerNet/sing-box)
- [API 文档（上游 Wiki）](https://github.com/alireza0/s-ui/wiki/API-Documentation)
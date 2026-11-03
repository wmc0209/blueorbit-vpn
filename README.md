# BlueOrbit VPN

**版本 1.0.0** · 一个简洁的 Ubuntu 桌面代理工具，应用菜单中显示为 **VPN**。

- 支持添加和选择 SSR 单节点链接。
- 提供智能分流（中国大陆直连）、全局代理和直连三种模式。
- 测试 Google、GPT、Claude、Grok API 网络连通性，并检查约 9 秒的模拟持续连接。
- 显示节点 IP、出口 IP 及估算位置，支持顶部栏图标与系统浅色／深色主题。
- 切换整机网络前进行检查；切换失败时尝试回退。

## 安装

适用于 **Ubuntu 24.04、64 位 x86（amd64）**，使用 systemd、systemd-resolved 与 GNOME 桌面。
下载 `blueorbit-vpn_1.0.0_amd64.deb`，然后在下载目录执行：

```sh
sudo apt install ./blueorbit-vpn_1.0.0_amd64.deb
```

也可以在软件安装器中打开安装包。安装本身不会启动或切换系统代理。
从应用菜单打开 **VPN**，添加自己的 `ssr://` 节点，选择模式后点击“应用所选模式”。
切换整机网络时会弹出管理员认证；代理模式会先检查连接。

顶部栏的小地球显示状态并提供打开窗口的入口。关闭窗口只会收起界面；
通过图标选择“退出图标”不会关闭代理。桌面登录后图标自动启动。
选择代理模式后，服务会在开机时启动；选择直连会停止并禁用该服务。

## 测试结果与隐私

- 绿色表示三次短连接都可达且平均耗时低于 4 秒；黄色表示部分失败、较慢或持续连接待确认；红色表示未收到响应。
- GPT、Claude 和 Grok 使用未登录的 API 端点：HTTP 401 在这里表示端点可达，**不代表账号、地区资格或模型调用已通过**。
- 持续连接使用第三方 HTTP 测试服务，约 9 秒；它不能保证长时间任务稳定。
- 为查询出口 IP 和位置，程序会依次尝试 ipwho.is、IP.SB 和 IPify。第三方会看到所选节点的出口 IP；地理位置只是估算。
- 节点凭据保存在当前用户的 `~/.config/simple-mihomo/nodes.json`，目录权限为 700、文件权限为 600。整机代理配置保存在仅 root 可读的 `/etc/simple-mihomo`。
- 智能分流使用随程序附带的规则快照，**不会自动更新**，少数网站可能被误判。

## 从源码构建

需要 Python 3、`dpkg-deb` 和联网访问 GitHub：

```sh
python3 scripts/build-deb.py
```

构建脚本从 Mihomo 官方 v1.19.32 发布页下载 amd64 兼容版，校验压缩包和解压后二进制的 SHA-256，再制作 `.deb`。
已有官方压缩包时，可以传入 `--archive /path/to/mihomo.gz`。产物默认放在 `dist/`。
该内核版本与 V1.0 的测试版本一致，不会自动升级。

运行测试：

```sh
python3 -m unittest discover -s tests -v
```

## 限制

V1.0 仅支持 **SSR 单节点链接**，不支持订阅、Windows、macOS 或 ARM。它需要本机 TUN 和 systemd。
模式切换涉及系统路由和 DNS，可能短暂中断连接；在其他系统或复杂网络环境下尚未验证。
请勿将节点链接或 `nodes.json` 提交到公开仓库。

## 许可证

GPL-3.0，详见 [LICENSE](LICENSE)。内含 Mihomo 和分流数据的来源、校验值及许可证信息见 [THIRD_PARTY.md](THIRD_PARTY.md)。

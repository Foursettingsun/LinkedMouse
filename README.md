<p align="center">
  <img src="docs/images/icon.png" width="96" alt="LinkedMouse">
</p>

<h1 align="center">LinkedMouse</h1>

<p align="center"><strong>两台电脑，一个流畅的工作台。</strong></p>
<p align="center">蓝牙优先的鼠标、键盘、剪贴板与文件共享工具，面向 Windows 双机开发与日常办公。</p>

<p align="center">
  <img alt="Windows" src="https://img.shields.io/badge/Windows-10%20%2F%2011-548BFF?logo=windows&logoColor=white">
  <img alt="Architecture" src="https://img.shields.io/badge/架构-x64-9985E8">
  <img alt="Bluetooth" src="https://img.shields.io/badge/连接-Bluetooth%20LE-ED98C5?logo=bluetooth&logoColor=white">
  <img alt="Version" src="https://img.shields.io/badge/预览版本-v0.1.10-9985E8">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/License-GPL--3.0-548BFF"></a>
</p>

<p align="center">
  <a href="https://github.com/Foursettingsun/LinkedMouse/releases/tag/v0.1.10"><strong>下载 v0.1.10</strong></a> ·
  <a href="#第一次使用">连接步骤</a> ·
  <a href="#vpn-与连接方式">VPN 与连接</a> ·
  <a href="https://github.com/Foursettingsun/LinkedMouse/issues">反馈问题</a>
</p>

![LinkedMouse 设备连接界面](docs/images/overview.png)

## 下载

两台电脑使用同一版本。安装包与便携版都包含运行环境，无需额外安装 Node.js 或 .NET。

| 文件 | 用途 | 下载 |
| --- | --- | --- |
| Windows 安装包 | 按向导安装到电脑 | [LinkedMouse-0.1.10-setup.exe](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.10/LinkedMouse-0.1.10-setup.exe) |
| Windows 便携版 | 解压后运行 `LinkedMouse.exe` | [LinkedMouse-0.1.10-portable.zip](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.10/LinkedMouse-0.1.10-portable.zip) |
| SHA-256 校验值 | 校验下载文件完整性 | [SHA256SUMS.txt](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.10/SHA256SUMS.txt) |

系统要求：Windows 10 2004（19041）或更高版本 / Windows 11，x64。两端均需支持 Bluetooth LE，至少一端支持 BLE 外围设备广播角色。Wi-Fi Direct 加速另需兼容的无线网卡与驱动。

## 四项核心功能

| 功能 | 可以做什么 |
| --- | --- |
| 无界鼠标 | 指针跨越屏幕边缘后继续操作另一台电脑；支持左右上下位置、速度、边缘阻力与指针锁定。 |
| 键盘共享 | 键盘跟随鼠标，转发常用按键与组合键；提供快捷键返回与断线按键释放。 |
| 共享剪贴板 | 双向共享纯文字、截图与图片；文字上限 256 KB，图片上限 20 MB / 3200 万像素。 |
| 文件传输 | 选择或拖入文件、文件夹；接收确认、进度、取消、重新发送、同名保护与 SHA-256 校验。 |

还提供托盘驻留、开机启动、可信设备自动重连、内存中的最近共享记录，以及连接诊断导出。

## 0.1.10 快移拖尾、跨屏阻力同步与蓝牙异常恢复

**两台电脑从托盘退出旧版后升级到 0.1.10。配对信息和本机阻力值保留。**

- 修复快速移动、急转时的拖尾过冲和尾部整数像素跳动；复用透明图层缓冲，减少反复分配。拖尾仍只在接管后短暂显示，不给真实鼠标输入增加平滑等待。
- “鼠标与键盘”新增“跟随主控电脑的跨屏阻力”，默认开启，按配对设备保存。被控时临时使用主控值，关闭或结束控制后恢复本机值；覆盖普通接管、预热预测返回、角色互换和管理员输入助手。
- 蓝牙修复异常接收丢弃其他连接已完成字节、旧回调污染替换 TLS 管道、已关闭连接对象保留等问题。保留当前 8ms 输入批次、GATT 可靠写入、MTU 分片、加密和心跳参数。

已通过 76 组原生、20 项 Node、9 个双进程回环、真实 Electron 五页及 17 个原生透明合成场景。界面开关的实际点击、按设备保存、本机值和核心 PID 保留均已检查。

物理双机蓝牙延迟、吞吐和长期稳定性仍需实机对比；不将单机回环或离屏画笔数据当作蓝牙性能证明。出现可重复退化时可回退至上一版本。

## 第一次使用

1. 在两台电脑上运行 LinkedMouse，并打开 Windows 蓝牙。
2. 在“设备连接”页刷新附近设备，选择另一台电脑发起配对。
3. 核对两端六位数字，在两台电脑上分别点击“数字一致”。
4. 到“鼠标与键盘”页设置另一台电脑在本机的左、右、上或下方。
5. 把指针继续推向对应屏幕边缘，进入另一台电脑；键盘随之切换。
6. 复制文字或截图后，在另一台电脑粘贴；发送文件时打开“文件传输”页。

**连续轻按两次右 Ctrl，立即将鼠标和键盘带回本机。** 也可更换为右 Alt 或右 Shift，或从托盘菜单返回本机。

应用通过自己的 BLE 服务配对，无需在 Windows 蓝牙设置中把另一台电脑添加成“鼠标”。

## VPN 与连接方式

LinkedMouse 以蓝牙作为基础连接。蓝牙发现、配对与传输直接使用 Windows 蓝牙接口，不依赖两台电脑处于同一路由器或同一局域网。

“Wi-Fi 智能加速”默认关闭，可按需开启：先通过可信蓝牙连接协商，尝试可达的本地网络或 Wi-Fi Direct，经过设备身份验证后为图片与文件提供额外通道。无法建立加速通道时继续使用蓝牙。

Wi-Fi Direct 与现有上网连接能否并存，以及 VPN/TUN 是否拦截新接口，取决于两端驱动与网络策略，需要实机验证。当前版本不保证所有 VPN 模式下的 Wi-Fi 直连；蓝牙是主要保障路径。

## 界面预览

原创蓝粉渐变界面与双指针图标。以下图片为界面示意，使用通用设备名称与目录，不表示已完成物理双机连接或性能测试。

<details>
<summary>双向切换与 1 秒拖尾效果示意</summary>

离开端收拢，接管端扩散。下图为 0.1.9 在单机 200% 缩放下的真实控制器与绘制线程回放：左右两块受控区域分别表示两端，并包含返回方向。拖尾图同样来自本机真实合成；这些图片不是物理双机录屏。

![离开端蓝粉光晕](docs/images/departure.png)
![进入端蓝粉光圈](docs/images/arrival.png)
![接管后连续圆周拖尾](docs/images/trail.png)

</details>

<details>
<summary>顶部中文提示 · 蓝粉风格</summary>

![控制另一电脑中](docs/images/hud-using.png)
![鼠标共享已开启](docs/images/hud-sharing.png)

</details>

<details>
<summary>鼠标与键盘</summary>

![鼠标与键盘设置](docs/images/input.png)

</details>

<details>
<summary>共享剪贴板</summary>

![共享剪贴板](docs/images/clipboard.png)

</details>

<details>
<summary>文件传输</summary>

![文件传输](docs/images/files.png)

</details>

## 预览版状态

v0.1.10 已通过 76 组原生、20 项 Node、9 个双进程回环和真实 Electron 五页检查，17 个透明合成场景通过。覆盖快移急转拖尾、实际阻力开关、设备独立保存、角色互换、异常 GATT 接收及旧管道回调隔离。详情见[验证记录](docs/VALIDATION.md)。

两台物理电脑之间的 BLE 输入、不同缩放、VPN/Wi-Fi Direct 共存和长期稳定性仍需实机验收。本版没有完成同设备原版性能对照。

文件传输入口为选择文件或拖入发送页。资源管理器跨屏拖文件、文件 Ctrl+C/Ctrl+V、断点续传、锁屏及 UAC 安全桌面控制不包含在本版中。

## 隐私与问题反馈

配对后使用加密会话。每批文件需接收确认，剪贴板最近记录保存在内存，诊断不包含剪贴板正文或私钥。

反馈请使用 [Issues](https://github.com/Foursettingsun/LinkedMouse/issues)，注明两端版本、系统与复现步骤。可附偏好设置导出的诊断，分享前检查其中的设备名称、网络地址和文件路径。

## 许可与来源

应用遵循 [GNU GPL v3.0](LICENSE)，输入模块包含 [TwinDesk](https://github.com/InukaAsith/TwinDesk) / [Beamer](https://github.com/kalkman-code/beamer) 的贡献，见[第三方声明](THIRD_PARTY_NOTICES.md)。

Git 仓库仅提交介绍、图片与许可；对应版本完整源码、构建脚本和依赖清单在 [Release 源码包](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.9/LinkedMouse-0.1.9-source.zip) 中提供，源码不展开提交到 Git。

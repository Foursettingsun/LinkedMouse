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
  <img alt="Version" src="https://img.shields.io/badge/预览版本-v0.1.4-9985E8">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/License-GPL--3.0-548BFF"></a>
</p>

<p align="center">
  <a href="https://github.com/Foursettingsun/LinkedMouse/releases/tag/v0.1.4"><strong>下载 v0.1.4</strong></a> ·
  <a href="#第一次使用">连接步骤</a> ·
  <a href="#vpn-与连接方式">VPN 与连接</a> ·
  <a href="https://github.com/Foursettingsun/LinkedMouse/issues">反馈问题</a>
</p>

![LinkedMouse 设备连接界面](docs/images/overview.png)

## 下载

两台电脑使用同一版本。安装包与便携版都包含运行环境，无需额外安装 Node.js 或 .NET。

| 文件 | 用途 | 下载 |
| --- | --- | --- |
| Windows 安装包 | 按向导安装到电脑 | [LinkedMouse-0.1.4-setup.exe](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.4/LinkedMouse-0.1.4-setup.exe) |
| Windows 便携版 | 解压后运行 `LinkedMouse.exe` | [LinkedMouse-0.1.4-portable.zip](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.4/LinkedMouse-0.1.4-portable.zip) |
| SHA-256 校验值 | 校验下载文件完整性 | [SHA256SUMS.txt](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.4/SHA256SUMS.txt) |

系统要求：Windows 10 2004（19041）或更高版本 / Windows 11，x64。两端均需支持 Bluetooth LE，至少一端支持 BLE 外围设备广播角色。Wi-Fi Direct 加速另需兼容的无线网卡与驱动。

## 四项核心功能

| 功能 | 可以做什么 |
| --- | --- |
| 无界鼠标 | 指针跨越屏幕边缘后继续操作另一台电脑；支持左右上下位置、速度、边缘阻力与指针锁定。 |
| 键盘共享 | 键盘跟随鼠标，转发常用按键与组合键；提供快捷键返回与断线按键释放。 |
| 共享剪贴板 | 双向共享纯文字、截图与图片；文字上限 256 KB，图片上限 20 MB / 3200 万像素。 |
| 文件传输 | 选择或拖入文件、文件夹；接收确认、进度、取消、重新发送、同名保护与 SHA-256 校验。 |

还提供托盘驻留、开机启动、可信设备自动重连、内存中的最近共享记录，以及连接诊断导出。

## 0.1.4 快移、后台稳定性与蓝粉特效

**两端都从托盘退出旧版，再启动 0.1.4，核对界面页脚/偏好设置版本。** 关闭窗口会保留后台；直接启动新版时若旧核心仍在运行，会提示先退出，避免误测旧版。配对身份保留。

- 快移起步按显示距离逐步接近最新目标，定时器晚到也不按截止时间瞬间追到远处；进入正常控制后继续使用原速度倍率。现代协议返回本机也从边缘起步，不补放返回边界包的剩余位移。
- 键鼠采集、WM_INPUT、定位和计时运行在独立原生 STA；网络心跳独立调度。窗口失焦不改动监听，最小化/关闭到托盘只请求健康检查，不重置健康连接或控制权。
- 检查真实 Raw Input 注册、事件计数与输入线程心跳；异常重建先成功安装新钩子再释放旧钩子，失败保留旧资源。核心无响应时恢复核心，连接恢复遵循原自动重连设置。
- 主屏→副屏、副屏→主屏都有蓝粉边缘光晕与收拢/扩散光圈；预热期间不显示。接管后 1 秒内绘制短暂淡出拖尾，快速返回时清除上一屏旧效果。
- 特效使用独立绘制线程和鼠标穿透、不激活的透明覆盖层；只接收最新坐标，绘制失败单独停用效果。可在“鼠标与键盘 → 跨屏视觉效果”分别关闭动画和拖尾；遵循 Windows 动画效果设置。

完整优化需两端 0.1.4，双向预热保持开启。确认前的普通位移不回放；点击、滚轮和拖动保留位置顺序。Raw Input 不采用 Windows 鼠标加速曲线，远端倍率可通过“指针速度”调整。

45 组原生检查、11 项 Node 测试、8 个双进程回环场景及真实 Electron 窗口检查通过；包含 100 次后台健康请求、已连接窗口的最小化与 20 次关闭到托盘。物理双机蓝牙首个可见位置、长期后台手感及 VPN/TUN 仍需验收，见[验证记录](docs/VALIDATION.md)和[验收步骤](docs/TESTING.md)。

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

离开端收拢，接管端扩散；以下为应用同一绘制器生成的静态示意，不是实际双机录屏。

![离开端蓝粉光晕](docs/images/departure.png)
![进入端蓝粉光圈](docs/images/arrival.png)
![接管后短暂拖尾](docs/images/trail.png)

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

v0.1.4 已通过 45 组原生检查、11 项 Node 测试和 8 个双进程回环场景。真实 Electron 主窗口的 5 个页面、与另一原生进程配对后的最小化及 20 次关闭到托盘检查通过，连接与进程保持，未点击桌面。

两台物理电脑之间的实际蓝牙输入、图片粘贴、不同 VPN/TUN 配置及 Wi-Fi Direct 共存仍需联调。尚未完成与 TwinDesk 的同设备性能对照，不预先宣称优于原版。

当前文件传输入口是“选择文件 / 拖入发送页”。资源管理器跨屏拖文件、文件 Ctrl+C/Ctrl+V、断点续传、锁屏及 UAC 安全桌面控制不包含在此版本中。

## 隐私与问题反馈

- 配对后使用加密会话，并保存可信设备身份。
- 每批文件需要接收确认，同名项目保留原文件。
- 剪贴板最近记录保存在内存，退出后清除；已标记的敏感剪贴板内容会跳过。
- 诊断导出不包含剪贴板正文或私钥。

反馈请使用 [Issues](https://github.com/Foursettingsun/LinkedMouse/issues)，注明两端系统版本、蓝牙型号、VPN 模式及复现步骤。可附“偏好设置 → 导出诊断”生成的文件，提交前检查其中的设备名称、网络地址和文件路径。

## 许可与来源

应用遵循 [GNU GPL v3.0](LICENSE)。输入模块包含 [TwinDesk](https://github.com/InukaAsith/TwinDesk) 与 [Beamer](https://github.com/kalkman-code/beamer) 的贡献，见 [第三方声明](THIRD_PARTY_NOTICES.md)。

本仓库的 Git 提交仅用于发布介绍、图片和许可说明。对应本版本的完整源码、构建脚本与依赖清单以 [Release 源码压缩包](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.4/LinkedMouse-0.1.4-source.zip) 提供；源码不展开提交到 Git 仓库。

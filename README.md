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
  <img alt="Version" src="https://img.shields.io/badge/预览版本-v0.1.6-9985E8">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/License-GPL--3.0-548BFF"></a>
</p>

<p align="center">
  <a href="https://github.com/Foursettingsun/LinkedMouse/releases/tag/v0.1.6"><strong>下载 v0.1.6</strong></a> ·
  <a href="#第一次使用">连接步骤</a> ·
  <a href="#vpn-与连接方式">VPN 与连接</a> ·
  <a href="https://github.com/Foursettingsun/LinkedMouse/issues">反馈问题</a>
</p>

![LinkedMouse 设备连接界面](docs/images/overview.png)

## 下载

两台电脑使用同一版本。安装包与便携版都包含运行环境，无需额外安装 Node.js 或 .NET。

| 文件 | 用途 | 下载 |
| --- | --- | --- |
| Windows 安装包 | 按向导安装到电脑 | [LinkedMouse-0.1.6-setup.exe](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.6/LinkedMouse-0.1.6-setup.exe) |
| Windows 便携版 | 解压后运行 `LinkedMouse.exe` | [LinkedMouse-0.1.6-portable.zip](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.6/LinkedMouse-0.1.6-portable.zip) |
| SHA-256 校验值 | 校验下载文件完整性 | [SHA256SUMS.txt](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.6/SHA256SUMS.txt) |

系统要求：Windows 10 2004（19041）或更高版本 / Windows 11，x64。两端均需支持 Bluetooth LE，至少一端支持 BLE 外围设备广播角色。Wi-Fi Direct 加速另需兼容的无线网卡与驱动。

## 四项核心功能

| 功能 | 可以做什么 |
| --- | --- |
| 无界鼠标 | 指针跨越屏幕边缘后继续操作另一台电脑；支持左右上下位置、速度、边缘阻力与指针锁定。 |
| 键盘共享 | 键盘跟随鼠标，转发常用按键与组合键；提供快捷键返回与断线按键释放。 |
| 共享剪贴板 | 双向共享纯文字、截图与图片；文字上限 256 KB，图片上限 20 MB / 3200 万像素。 |
| 文件传输 | 选择或拖入文件、文件夹；接收确认、进度、取消、重新发送、同名保护与 SHA-256 校验。 |

还提供托盘驻留、开机启动、可信设备自动重连、内存中的最近共享记录，以及连接诊断导出。

## 0.1.6 离开屏幕时完整隐藏光标

**两台电脑均从托盘退出旧版，再启动 0.1.6。** 配对和个人设置保留。

- 修复副机作为接收端返回主机后，指针仍停在最边缘露出一截的问题；预测返回、普通边缘返回及手动/快捷键返回均管理离开端的隐藏状态。
- 停放窗口显式处理光标设置消息，保留透明光标后移除整个指针；用带自身标记的零位移鼠标消息刷新 Windows 光标归属，保持坐标和键盘焦点。
- 再次真正进入该电脑时显示光标，预热期间保持隐藏；操作该电脑自己的鼠标或键盘也会恢复，隐藏状态不接管该电脑的实体鼠标。
- 断线、超时、锁定、关闭鼠标共享和退出会释放隐藏状态；窗口最小化/关闭到托盘的健康检查保持当前状态。诊断新增隐藏状态与光标刷新成功/失败计数。

51 组核心、11 项 Node、8 个双进程回环及真实 Electron 窗口回归通过。21 个实际显隐场景在 200% 缩放下通过，并在三个独立进程中重复，包含 32/64/128 像素自定义光标、窗口边缘消息、恢复显示和过期消息；指针位置及前台焦点保持。物理双机 BLE、不同缩放组合和首次实体点击仍需验收，见[验证记录](docs/VALIDATION.md)和[验收步骤](docs/TESTING.md)。

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

离开端收拢，接管端扩散；以下为 0.1.5 本机 200% 缩放下，应用实际绘制线程覆盖在受控测试窗口上的合成截图；不是物理双机录屏。

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

v0.1.6 已通过 51 组核心、11 项 Node、8 个双进程回环及真实 Electron 窗口回归。新增 21 个本机实际显隐场景，覆盖后台指针归属、不同尺寸自定义光标、完整隐藏和返回恢复，三个独立进程重复通过。蓝粉特效沿用 0.1.5 的透明图层实现。

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

本仓库的 Git 提交仅用于发布介绍、图片和许可说明。对应本版本的完整源码、构建脚本与依赖清单以 [Release 源码压缩包](https://github.com/Foursettingsun/LinkedMouse/releases/download/v0.1.6/LinkedMouse-0.1.6-source.zip) 提供；源码不展开提交到 Git 仓库。

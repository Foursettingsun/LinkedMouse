# Third-party notices

LinkedMouse is distributed under GNU GPL v3.0. The complete license is in LICENSE.

Input capture, injection, key mapping and monitor geometry in third_party/twindesk
come from TwinDesk, Copyright (C) 2026 inukaasith, GPL-3.0.
Source: https://github.com/InukaAsith/TwinDesk
Pinned source commit: 129e97cf19155809263c73a5ef1e201b9f8cc13d.
Capture.cs and Inject.cs include portions adapted from Beamer,
Copyright (C) Kalkman Code, GPL-3.0: https://github.com/kalkman-code/beamer.
Original source headers and the upstream THIRD_PARTY_NOTICES are preserved.
Ble.cs in that directory is a reference; LinkedMouse's native Bluetooth transport
adapts its GATT service/characteristic and reliable write approach, with new
service UUIDs, an in-process stream, cancellation and bounded receive buffers.

Original LinkedMouse code and modifications: Copyright (C) 2026 LinkedMouse contributors.
The icon and interface assets were created for LinkedMouse.

Electron and its Chromium/Node.js components have their own licenses, which are
included in the built application's runtime distribution. electron-builder is MIT.
.NET and Windows SDK projection libraries retain their upstream license notices
in the published engine distribution.

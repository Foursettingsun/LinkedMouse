# Third-party notices

LinkedMouse is distributed under GNU GPL v3.0. The complete license is in LICENSE.

Input capture, injection, key mapping and monitor geometry in third_party/twindesk
come from TwinDesk, Copyright (C) 2026 inukaasith, GPL-3.0.
Source: https://github.com/InukaAsith/TwinDesk
Pinned source commit: 129e97cf19155809263c73a5ef1e201b9f8cc13d.
Capture.cs and Inject.cs include portions adapted from Beamer,
Copyright (C) Kalkman Code, GPL-3.0: https://github.com/kalkman-code/beamer.
Original source headers and the upstream THIRD_PARTY_NOTICES are preserved.
LinkedMouse 0.1.1 modifies Capture.cs to observe marked landing injections,
Inject.cs to check cursor placement and keep a per-route logical position,
and Screens.cs to allow isolated replay of monitor geometry.
LinkedMouse 0.1.2 further modifies Capture.cs for preparation probes, physical
button tracking and persistent background input; Inject.cs for modifier handoff;
and HideCursor.cs for preallocated cursor resources. These changes are dated
2026-10-27 in the modified source headers.
LinkedMouse 0.1.3 further modifies Capture.cs to capture ordered raw motion,
buttons and wheel without center-based hook deltas, and Native.cs to expose
raw-message timestamps. These changes are dated 2026-10-28 in their headers.
LinkedMouse 0.1.4 further modifies Capture.cs for health-based hook/raw-input
recovery and Native.cs for registered raw-device queries (2026-10-28).
PointerEffects.cs adapts the edge-glow/ring concept from TwinDesk Flash.cs;
its blue/pink painter, one-second trail and separate visual thread are new.
Ble.cs in that directory is a reference; LinkedMouse's native Bluetooth transport
adapts its GATT service/characteristic and reliable write approach, with new
service UUIDs, an in-process stream, cancellation and bounded receive buffers.

Original LinkedMouse code and modifications: Copyright (C) 2026 LinkedMouse contributors.
The icon and interface assets were created for LinkedMouse.

Electron and its Chromium/Node.js components have their own licenses, which are
included in the built application's runtime distribution. electron-builder is MIT.
.NET and Windows SDK projection libraries retain their upstream license notices
in the published engine distribution.

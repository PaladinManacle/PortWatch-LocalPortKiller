<p align="center">
  <img src="https://i.postimg.cc/WpQjLb84/banner.png" alt="PortWatch Local Port Inspector — Find & Free Blocked Windows TCP/UDP Ports in One Click" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Port%20%26%20PID%20Inspector-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-portwatch--v1.3-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# PortWatch Local Port Inspector — Find & Free Blocked Windows TCP/UDP Ports in One Click

**Getting 'Address already in use (EADDRINUSE)' on port 3000, 5173, 8080, or your Minecraft/Valheim/Enshrouded dedicated server port 25565 / 27015? Stop typing netstat -ano and taskkill commands—see every listening port, PID, and executable path visually.**

PortWatch Local Port Inspector replaces multi-step `netstat` + `tasklist` + `taskkill` terminal lookups with a clean, searchable Windows table: **listing every active TCP and UDP port, process name, PID, full executable path, and offering a 1-click 'Free Port' action with system-process protection**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) web developers, self-hosters, and dedicated game server admins** troubleshooting port conflicts locally.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Dev server fails with `EADDRINUSE: address already in use :3000` | Zombie `node.exe` or `python.exe` process still holding the port | Search `3000` in PortWatch and click **Free Port (End PID)** |
| Dedicated game server fails to bind UDP `25565` / `27015` / `7777` | Previous server instance didn't close cleanly or another app claimed the port | Filter by port number to see the exact conflicting `.exe` and path |
| Unsure which background app is listening on external interfaces | `0.0.0.0` listeners exposed on LAN without visibility | Filter between `127.0.0.1` (Localhost) and `0.0.0.0` (All Interfaces) |
| Typing `netstat -ano | findstr` every time is slow | Command-line output only shows numeric PIDs without process names | View live sortable table with process icons, paths, and copyable details |

## Download for Windows

[**Download PortWatch.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/PortWatch.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `PortWatch.exe`? (Key features)

- Lists all active **TCP (`LISTENING`)** and **UDP** endpoints with Port, Protocol, Local Address, PID, Process Name, and `.exe` Path.
- Instant search bar filters by port number (`3000`, `8080`, `25565`) or process name (`node`, `java`, `python`) as you type.
- One-click **Free Port** terminates zombie processes while guarding critical Windows system PIDs (`System`, `svchost`, `lsass`).
- Includes **Open File Location** and **Copy Port/PID Info** context actions.

### Sample Output

```text
[PortWatch] Active Listening Endpoints (TCP: 24 | UDP: 18)
[INFO] TCP :3000   | 127.0.0.1 | PID 14820 | node.exe (C:\Program Files\nodejs\node.exe)
[INFO] UDP :27015  | 0.0.0.0   | PID 8840  | EnshroudedServer.exe
[OK]   Action      : Terminated zombie PID 14820 -> Port 3000 is now free
```

The release ZIP is named `PortWatch.zip`; the Windows executable inside is named `PortWatch.exe`.

1. Close PortWatch before updating or replacing executable files.
2. Click **Download PortWatch.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `PortWatch.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit).

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `PortWatch.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Instant resolution of `EADDRINUSE` localhost port conflicts

Frees stuck dev servers and background workers in two seconds.

### Dedicated game server port troubleshooting

Confirms immediately whether your server binary successfully bound its TCP/UDP ports.

### Visibility into `0.0.0.0` vs. `127.0.0.1` bindings

Shows which services are reachable across your local network.

### Built-in protection against killing critical OS processes

Warns and blocks accidental termination of core Windows system services.

## Default folders and configuration paths

PortWatch runs as a standalone portable executable with zero installation:

```text
Portable (Queries Windows IP Helper API directly)
```

Typical directory layout:

```text
PortWatch Live Table
├── Filter: [Port / Process Name]  [TCP] [UDP] [Localhost Only]
├── Columns: Port | Proto | Address | PID | Process | Executable Path
└── Actions: Free Port (End PID) | Open Folder | Copy Info
```

Run PortWatch as Administrator if you want to inspect full `.exe` paths for elevated system services.

## Quick start guide

Follow these steps to get started:

1. **Extract `PortWatch.zip` and launch `PortWatch.exe`.** Active TCP/UDP ports load immediately.
2. **Type the conflicting port number (e.g., `3000`, `8080`, `25565`) into the search box.** Inspect the process name and executable path holding the port.
3. **Select the stuck process and click **Free Port**.** Confirm the port disappears from the listening list.
4. **Restart your development server or dedicated game server.** It will now bind the port cleanly.

### Data safety note

PortWatch queries Windows `GetExtendedTcpTable` / `GetExtendedUdpTable` APIs in read-only mode unless you click Free Port.

## What the status summary shows

PortWatch displays **listening TCP/UDP ports, bind addresses, PIDs, and full executable paths**.

## FAQ

**Does PortWatch scan external internet IPs?**

No. It strictly inspects local listening ports on your own Windows machine (`netstat` equivalent).

**Can it inspect both TCP and UDP ports?**

Yes—it displays both TCP listening sockets and UDP endpoints.

**Does it require installation?**

No. `PortWatch.exe` is completely portable.

## Useful reading

- [Microsoft Docs — GetExtendedTcpTable API](https://learn.microsoft.com/en-us/windows/win32/api/iphlpapi/nf-iphlpapi-getextendedtcptable)

## More Windows Desktop Utilities

- [HostsGuard-LocalDNSBlocker](../HostsGuard-LocalDNSBlocker) — Windows hosts file profile switcher & local domain blocker
- [NetPing-DNSGameSwitcher](../NetPing-DNSGameSwitcher) — Game server ping tester, Winsock reset & DNS switcher
- [PinTop-WindowAlwaysOnTop](../PinTop-WindowAlwaysOnTop) — Pin any window Always-on-Top & adjust transparency on Windows
- [ClipVault-OfflineClipboardHistory](../ClipVault-OfflineClipboardHistory) — Offline Windows clipboard history & plain-text snippet manager

*Independent open-source desktop utility for Windows.*

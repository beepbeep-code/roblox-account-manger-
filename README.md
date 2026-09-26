# Roblox Account Manager

A Windows desktop Roblox account manager built with **Electron + Playwright**.

Manage multiple Roblox sessions, launch accounts into specific experiences, automate relaunching, and optionally control the desktop app remotely through the Aureon Collective dashboard.

<p align="center">
  <a href="https://aureon-collective.xyz/">Website</a>
  •
  <a href="https://discord.gg/8wufyBp7P">Discord</a>
</p>

---

## ✨ Features

- **Multi-account management** — save and manage multiple Roblox accounts from one desktop app.
- **Direct launching** — launch an account into a Roblox experience using its Place ID.
- **Multi-instance support** — run multiple Roblox clients at the same time.
- **Multi-launch** — launch saved accounts together with a configurable delay.
- **Auto-relaunch** — automatically relaunch accounts after a real disconnect or process exit.
- **Server shuffle** — move accounts on the configured shuffle schedule.
- **Saved Place IDs** — keep frequently used Roblox experiences ready to launch.
- **Live account status** — see launching, queued, relaunching, and error states.
- **Launch queue** — see what is currently waiting to launch.
- **Minimize all Roblox clients** — quickly reduce GPU usage when running clients in the background.
- **System tray controls** — open, pause relaunching, close Roblox clients, or quit from the tray.
- **Import / export configuration** — move account configuration without exporting session cookies.
- **Optional remote control** — pair the desktop app with the Aureon Collective dashboard over an outbound WSS connection.
- **Dark desktop UI** — built for staying open while you manage multiple clients.

## 🔐 Security

The desktop application is designed so Roblox session data stays local to the PC.

- Session state is stored using Electron's OS-backed secure storage when available.
- The remote-control connection is **outbound WSS**; the desktop app does not expose a public HTTP server.
- Remote pairing uses a short-lived, single-use pairing code.
- The desktop generates an **Ed25519** identity locally.
- The relay receives the device's public key rather than the private key.
- Remote commands are signed, expire quickly, and use nonce replay protection.
- Remote commands are allowlisted; the protocol does not provide a remote shell, PowerShell passthrough, arbitrary executable execution, or arbitrary file access.
- Roblox cookies/session files are not sent to the remote relay.

> **Important:** The remote relay/backend implementation is not included in this desktop repository. The included `REMOTE_PROTOCOL.md` documents the desktop-side protocol.

## 🖥️ Requirements

- Windows
- [Node.js LTS](https://nodejs.org/)
- npm
- Internet connection for Roblox / remote features

## 🚀 Installation

### Easy install

1. Install **Node.js LTS**.
2. Download or clone this repository.
3. Run `install.bat`.
4. Run `run.bat`.

### Manual install

```bash
npm install
npx playwright install chromium
npm start
```

## 📁 Project Structure

```text
.
├── electron/
│   ├── main.js
│   └── preload.js
├── src/
│   ├── app.js
│   ├── index.html
│   └── styles.css
├── install.bat
├── run.bat
├── package.json
├── REMOTE_PROTOCOL.md
├── PATCH_NOTES.md
└── README.md
```

## 🌐 Remote Access

The desktop app can optionally connect to the Aureon Collective dashboard.

### Pairing

1. Open the Aureon Collective dashboard.
2. Go to **Remote Control → Connect Desktop**.
3. Generate a one-time pairing code.
4. Open **Remote access** in the desktop app.
5. Enter the dashboard/relay URL, device name, and pairing code.
6. Select **Pair this PC**.

The desktop maintains an outbound WSS connection to the relay while the app is running.

See [`REMOTE_PROTOCOL.md`](REMOTE_PROTOCOL.md) for the protocol details.

## ⚙️ Configuration

Account-specific settings include:

- Place ID
- Auto-relaunch
- Relaunch delay
- Server shuffle
- Relaunch controls

Global settings include launch behavior, instance limits, relaunch limits/cooldowns, and other desktop preferences.

Account/session data is stored under the Windows user's application data directory rather than being required to live beside the application.

## 🛠️ Development

This project uses:

- **Electron** — desktop application shell
- **Playwright** — Roblox browser/session automation
- **WebSocket (`ws`)** — remote relay connection
- **electron-store** — local application storage

Start the application in development with:

```bash
npm install
npx playwright install chromium
npm start
```

## 📌 Current Version

**v2.9.7**

The v2.9.7 patch includes fixes for Roblox multi-instance synchronization, an internal version mismatch, and improved remote WSS error reporting.

See [`PATCH_NOTES.md`](PATCH_NOTES.md) for the release notes.

## 🤝 Community

Have questions, want to request the open-source version, or want to follow development?

**Discord:** https://discord.gg/8wufyBp7P

**Website:** https://aureon-collective.xyz/

---

<p align="center">
  Built for Roblox account management • Aureon Collective
</p>

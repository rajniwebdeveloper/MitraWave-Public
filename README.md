# MitraWave

<img src="https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png" width="112" alt="MitraWave app icon" />

### Stay Connected, Even Offline.

**MitraWave** is a privacy-first messaging product being developed for Android, iOS, Web, Windows, Linux and macOS, with online chat and proximity-based encrypted mesh delivery as its intended capabilities.

[**Download latest Android APK (v0.4.0-dev)**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.4.0-dev/MitraWave-Android-v0.4.0-dev.apk) · [**Other platform UI previews**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.2.0-preview) · [**All releases**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases)

> **Important:** The currently available downloads are **UI previews, not functional encrypted messaging clients**. The Android v0.4.0-dev preview includes the branded icon, password-encrypted **local signing-key plus recovery-note** backup/import, and a **manual HTTPS/TCP backend health check** in Settings, but does not recover actual chats. Real sign-in in the apps, end-to-end encrypted messages, voice/video calls, Bluetooth mesh forwarding and live chat are not operational in these preview packages. Do not use the previews for sensitive communication.

## Downloads — Android v0.4.0-dev, other platforms v0.2.0-preview

| Platform | Public download | What it contains |
| --- | --- | --- |
| **Android (7.0+)** | [Download latest APK](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.4.0-dev/MitraWave-Android-v0.4.0-dev.apk) | Branded Android UI + encrypted identity backup/import + manual HTTPS Go-server diagnostics, min API 24, target API 36 |
| **Windows x64** | [Download Windows ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Windows-Desktop-Preview-amd64.zip) | `.exe` desktop UI preview launcher |
| **Linux x86-64** | [Download Linux tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-amd64.tar.gz) | Linux desktop UI preview executable |
| **Linux ARM64** | [Download ARM64 tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-arm64.tar.gz) | ARM64 desktop UI preview executable |
| **Linux ISO** | [Download ISO](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-DATA-ONLY.iso) | **Data ISO only; NOT bootable, NOT a Linux OS or installer** |
| **macOS Apple Silicon** | [Download macOS tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-macOS-Desktop-Preview-arm64.tar.gz) | Unsigned local desktop UI preview launcher |
| **Web** | [Download Web ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Web-UI-Preview.zip) | Static HTML + compiled Kotlin/JS browser preview |
| **iOS Simulator** | [Download Simulator ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-iOS-Simulator-UI-Preview.zip) | Unsigned **simulator-only** application, not an iPhone IPA |

[**SHA-256 checksums for all downloads**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/SHA256SUMS.txt)

The Windows, Linux and macOS desktop downloads run a local-only user interface in the default browser. They are *not* connected to the private Go backend. The current Android APK's internal version is `0.4.0-dev` (versionCode 4). The other downloadable previews are unchanged older builds.

## Android private-key import and local recovery (v0.4.0-dev)

The Android app now offers **Settings → Private key import / export**, with a password-encrypted `.mwbackup` that includes a local P-256 signing private key, its public key and a saved recovery note. The private key is encrypted locally using Android Keystore; the exported backup uses AES-256-GCM with a password-derived key. To import, select the saved `.mwbackup`, enter its password and confirm replacing the local identity.

**This does not restore chat history.** The prototype has no working encrypted chat database; restoring a key alone cannot retrieve messages that were never backed up. Real-device restore testing and a security audit remain outstanding. The backup and password should be kept private.

[View Android v0.3.0 release](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.3.0-dev) · [Download app icon](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png)

## Go backend/TCP connection status

MyServer82 runs a **Go HTTP + WebSocket gateway** at `127.0.0.1:18482`, with separate isolated Redis and PostgreSQL containers. Live integration tests have passed registration/login, key lookup, temporary ciphertext delivery, acknowledgement/deletion, and WebSocket upgrades. **This is an internal-only listener**, not a public mobile endpoint. The new Android Settings screen can test a user-provided HTTPS gateway address, but public domain/TLS routing and the actual chat client integration are not configured. The app is **not ready for public secure messaging**.

[View verified transport integration test](https://github.com/rajniwebdeveloper/MitraWave/actions/runs/40185251965) (requires private repo access).

## Features

MitraWave's product design covers the following experiences. **Feature descriptions do not mean they are implemented in the current downloadable previews.**

| Experience | Features |
| --- | --- |
| **Secure accounts** | Unique @username or email + password; no mandatory phone number or OTP; device session management |
| **Friends & verification** | Username search, requests and approvals, QR invitations, encryption identity verification |
| **Private conversations** | End-to-end encrypted private chats, local encrypted history, reactions, replies, receipts |
| **Internet chat** | Real-time message delivery, typing indicators, encrypted offline queues |
| **Offline nearby** | Bluetooth discovery and Wi-Fi capable device-to-device transfers with user permissions |
| **Mesh relay** | Optional encrypted store-and-forward through consenting nearby devices, with expiry and hop limits |
| **Media** | Photos, videos, documents, stickers, voice notes and emojis |
| **Voice & video** | Private calls with device-oriented security |
| **Groups & channels** | Communities, member permissions, topics, polls and moderation |
| **Privacy & settings** | App lock, expiring chats, key verification, light/dark themes |
| **Platforms** | Android, iOS, Web, Windows, Linux and macOS, within platform-specific offline limitations |

### How the mesh design works

**Alex → Alexa → Sam:** Alex addresses a cryptographically encrypted message to Sam. Alexa may voluntarily store and forward a ciphertext envelope while Sam has no internet connection. When Alexa and Sam are within range of a supported Bluetooth/Wi-Fi transport, the message could be forwarded without Alexa reading it. This is the proposed design; **it does not run in the preview downloads**.

## Installation notes

**Android:** Download the latest **v0.4.0-dev** APK and install using the system package installer. This is a development/debug-signed preview, not an official app-store release.

**Windows:** Extract the ZIP, then open `MitraWave-Desktop-Preview.exe`. It launches a UI preview in your default browser.

**Linux:** Extract the `.tar.gz`, then run `chmod +x MitraWave-Desktop-Preview && ./MitraWave-Desktop-Preview`. The ISO is a **nonbootable data container** for the Linux x86-64 preview, not an OS distribution.

**macOS:** Extract the ARM64 archive and run the preview launcher. This binary is unsigned and may be blocked by macOS Gatekeeper.

**Web:** Extract and serve the static `index.html` and `mitrawave.js` files. **iOS:** The Simulator archive is for developer testing on a Mac with Xcode; a signed iPhone IPA is not yet available.

## Repository policy

This public repository contains **only `README.md`**. Downloadable builds are distributed as **GitHub Release assets**, and the implementation source remains in a **separate private repository**. Backend server binaries and credentials are not included in these public downloads.

## Feedback

Submit issues via the [GitHub Issues tab](https://github.com/rajniwebdeveloper/MitraWave-Public/issues). Do not post passwords, personal conversations or encryption secrets.

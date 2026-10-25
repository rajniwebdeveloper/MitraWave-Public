# MitraWave

### Stay Connected, Even Offline.

**MitraWave** is a privacy-first messaging product being developed for Android, iOS, Web, Windows, Linux and macOS, with online chat and proximity-based encrypted mesh delivery as its intended capabilities.

[**Download multi-platform previews**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.2.0-preview) · [**All releases**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases)

> **Important:** The currently available downloads are **UI previews, not functional encrypted messaging clients**. Real sign-in in the apps, end-to-end encrypted messages, voice/video calls, Bluetooth mesh forwarding and live chat are not operational in these preview packages. Do not use the previews for sensitive communication.

## Downloads — v0.2.0-preview

| Platform | Public download | What it contains |
| --- | --- | --- |
| **Android (7.0+)** | [Download APK](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Android-v0.1.0-dev.apk) | Android UI preview, min API 24, target API 36 |
| **Windows x64** | [Download Windows ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Windows-Desktop-Preview-amd64.zip) | `.exe` desktop UI preview launcher |
| **Linux x86-64** | [Download Linux tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-amd64.tar.gz) | Linux desktop UI preview executable |
| **Linux ARM64** | [Download ARM64 tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-arm64.tar.gz) | ARM64 desktop UI preview executable |
| **Linux ISO** | [Download ISO](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-DATA-ONLY.iso) | **Data ISO only; NOT bootable, NOT a Linux OS or installer** |
| **macOS Apple Silicon** | [Download macOS tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-macOS-Desktop-Preview-arm64.tar.gz) | Unsigned local desktop UI preview launcher |
| **Web** | [Download Web ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Web-UI-Preview.zip) | Static HTML + compiled Kotlin/JS browser preview |
| **iOS Simulator** | [Download Simulator ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-iOS-Simulator-UI-Preview.zip) | Unsigned **simulator-only** application, not an iPhone IPA |

[**SHA-256 checksums for all downloads**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/SHA256SUMS.txt)

The Windows, Linux and macOS desktop downloads run a local-only user interface in the default browser. They are *not* connected to the private Go backend. The Android package's internal version remains `0.1.0-dev`, even though this combined download collection is labeled `v0.2.0-preview`.

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

**Android:** Download the APK and install using the system package installer. This is a development/debug-signed preview, not an official app-store release.

**Windows:** Extract the ZIP, then open `MitraWave-Desktop-Preview.exe`. It launches a UI preview in your default browser.

**Linux:** Extract the `.tar.gz`, then run `chmod +x MitraWave-Desktop-Preview && ./MitraWave-Desktop-Preview`. The ISO is a **nonbootable data container** for the Linux x86-64 preview, not an OS distribution.

**macOS:** Extract the ARM64 archive and run the preview launcher. This binary is unsigned and may be blocked by macOS Gatekeeper.

**Web:** Extract and serve the static `index.html` and `mitrawave.js` files. **iOS:** The Simulator archive is for developer testing on a Mac with Xcode; a signed iPhone IPA is not yet available.

## Repository policy

This public repository contains **only `README.md`**. Downloadable builds are distributed as **GitHub Release assets**, and the implementation source remains in a **separate private repository**. Backend server binaries and credentials are not included in these public downloads.

## Feedback

Submit issues via the [GitHub Issues tab](https://github.com/rajniwebdeveloper/MitraWave-Public/issues). Do not post passwords, personal conversations or encryption secrets.

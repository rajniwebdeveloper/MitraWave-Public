# MitraWave

<img src="https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png" width="112" alt="MitraWave app icon" />

### Stay Connected, Even Offline.

**MitraWave** is a privacy-first messaging product being developed for Android, iOS, Web, Windows, Linux and macOS, with online chat and proximity-based encrypted mesh delivery as its intended capabilities.

[**Download latest Android APK (v0.5.0-dev)**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.5.0-dev/MitraWave-Android-v0.5.0-dev.apk) · [**Other platform UI previews**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.2.0-preview) · [**All releases**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases)

> **Important:** Most available downloads are **UI previews**. Android v0.5 includes experimental encrypted-message code but has not passed a real two-device E2EE test. The Android v0.5.0-dev preview includes the branded icon, password-encrypted local signing-key backup/import, **live username/password registration/login**, and **experimental internet-based encrypted send/receive** using public HTTPS/WSS. These functions have not been validated in a real two-device chat test. This is NOT an audited Signal/Double-Ratchet implementation; there is no persistent chat-history backup, nearby mesh, or calls. Other platforms remain UI previews. **Do not use these experimental builds for sensitive conversations.**

## Downloads — Android v0.5.0-dev, other platforms v0.2.0-preview

| Platform | Public download | What it contains |
| --- | --- | --- |
| **Android (7.0+)** | [Download latest APK](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.5.0-dev/MitraWave-Android-v0.5.0-dev.apk) | Android experimental HTTPS/WSS encrypted 1:1 messaging, identity backup/import, min API 24, target API 36 |
| **Windows x64** | [Download Windows ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Windows-Desktop-Preview-amd64.zip) | `.exe` desktop UI preview launcher |
| **Linux x86-64** | [Download Linux tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-amd64.tar.gz) | Linux desktop UI preview executable |
| **Linux ARM64** | [Download ARM64 tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-arm64.tar.gz) | ARM64 desktop UI preview executable |
| **Linux ISO** | [Download ISO](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-DATA-ONLY.iso) | **Data ISO only; NOT bootable, NOT a Linux OS or installer** |
| **macOS Apple Silicon** | [Download macOS tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-macOS-Desktop-Preview-arm64.tar.gz) | Unsigned local desktop UI preview launcher |
| **Web** | [Download Web ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Web-UI-Preview.zip) | Static HTML + compiled Kotlin/JS browser preview |
| **iOS Simulator** | [Download Simulator ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-iOS-Simulator-UI-Preview.zip) | Unsigned **simulator-only** application, not an iPhone IPA |

[**SHA-256 checksums for all downloads**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/SHA256SUMS.txt)

The Windows, Linux and macOS desktop downloads run a local-only user interface in the default browser. They are *not* connected to the private Go backend. The current Android APK's internal version is `0.5.0-dev` (versionCode 5). The other downloadable previews are unchanged older builds. **Android v0.5 is not ready for general public-secure messaging.**

## Android private-key import and local recovery (v0.5.0-dev)

The Android app now offers **Settings → Private key import / export**, with a password-encrypted `.mwbackup` that includes a local P-256 signing private key, its public key and a saved recovery note. The private key is encrypted locally using Android Keystore; the exported backup uses AES-256-GCM with a password-derived key. To import, select the saved `.mwbackup`, enter its password and confirm replacing the local identity.

**This does not restore chat history.** The prototype has no working encrypted chat database; restoring a key alone cannot retrieve messages that were never backed up. Real-device restore testing and a security audit remain outstanding. The backup and password should be kept private.

[View Android v0.3.0 release](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.3.0-dev) · [Download app icon](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png)

## Go backend/TCP connection status

MyServer82 runs a **Go HTTP + WebSocket gateway** on internal-only TCP `127.0.0.1:18482`, with Redis and PostgreSQL privately isolated. The gateway is now reachable through **[public HTTPS](https://trade.apihubs.in/mitrawave/healthz)** at `https://trade.apihubs.in/mitrawave/` and **WSS** at `wss://trade.apihubs.in/mitrawave/v1/live`, using Apache TLS reverse proxy. Public integration tests have passed registration/login, immutable P-256 key lookup, temporary ciphertext delivery, acknowledgement/deletion and authenticated WebSocket upgrade. The Android app includes an experimental client for this endpoint. **Real-device E2EE interoperability, an audited ratchet and long-term message storage remain incomplete.**

[View verified public transport integration test](https://github.com/rajniwebdeveloper/MitraWave/actions/runs/40186672895) (requires private repo access).

## Android experimental encrypted chat (v0.5.0-dev)

Android now has a prototype **HTTPS + WSS** client, username/password sign-in, P-256 public-key registration, encrypted 1:1 message sending, decryption and inbox acknowledgement. Message encryption uses ephemeral P-256 ECDH, HKDF-SHA256, AES-256-GCM and ECDSA signatures. Contact identity keys are pinned on first use (**TOFU, not independently verified**).

**Security limits:** This is not a reviewed Signal/Double Ratchet. It lacks post-compromise security, persistent chat history, strong first-contact verification and completed real-device testing. Messages displayed in the app are held in memory only and disappear when the app is closed. The `.mwbackup` restores a signing identity and note, **not chat history**. This APK is for developer testing only.

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

**Android:** Download the latest **v0.5.0-dev** APK and install using the system package installer. Sign in or create a disposable test account in Chats. This is a debug-signed **developer preview, not a production secure messenger**; do not send sensitive messages. **Update warning:** preview APK signatures can differ between GitHub Actions builds; if Android refuses an in-place upgrade, export your password-protected `.mwbackup` first, then uninstall the old preview and install the new APK. Uninstalling erases the app's local data; `.mwbackup` restores only the signing identity and saved note, **not chat history**.

**Windows:** Extract the ZIP, then open `MitraWave-Desktop-Preview.exe`. It launches a UI preview in your default browser.

**Linux:** Extract the `.tar.gz`, then run `chmod +x MitraWave-Desktop-Preview && ./MitraWave-Desktop-Preview`. The ISO is a **nonbootable data container** for the Linux x86-64 preview, not an OS distribution.

**macOS:** Extract the ARM64 archive and run the preview launcher. This binary is unsigned and may be blocked by macOS Gatekeeper.

**Web:** Extract and serve the static `index.html` and `mitrawave.js` files. **iOS:** The Simulator archive is for developer testing on a Mac with Xcode; a signed iPhone IPA is not yet available.

## Repository policy

This public repository contains **only `README.md`**. Downloadable builds are distributed as **GitHub Release assets**, and the implementation source remains in a **separate private repository**. Backend server binaries and credentials are not included in these public downloads.

## Feedback

Submit issues via the [GitHub Issues tab](https://github.com/rajniwebdeveloper/MitraWave-Public/issues). Do not post passwords, personal conversations or encryption secrets.
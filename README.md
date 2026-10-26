# MitraWave

<img src="https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png" width="112" alt="MitraWave app icon">

### Stay Connected, Even Offline — planned product vision

MitraWave is an experimental device-owned messaging project. Android includes a prototype encrypted relay client; the current Windows, Linux, macOS, Web and iOS Simulator packages are **UI-only previews**.

**Latest multi-platform download collection:** [MitraWave 0.8.0 developer previews](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.8.0-multiplatform-preview)

> **Not a production-ready, audited encrypted messenger.** The public API is live, and build/integration checks passed. But no real two-Android-device encrypted-message roundtrip has been certified, and the experimental cryptography is not Signal/Double Ratchet. Do not use these builds for sensitive communication.

## Public downloads (0.8.0 preview collection)

| Platform | Public download | Functional scope |
| --- | --- | --- |
| **Android 7.0+** | [APK v0.7.0-dev](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Android-v0.7.0-dev.apk) | Prototype username registration, key backup, PostgreSQL user search, experimental HTTPS/WSS encrypted chat, self-deletion |
| **Windows x64** | [Windows ZIP/EXE](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Windows-UI-Preview-amd64.zip) | Local-browser UI-only preview |
| **Linux x86-64** | [Linux tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Linux-UI-Preview-amd64.tar.gz) | Local-browser UI-only preview |
| **Linux ARM64** | [Linux ARM64 tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Linux-UI-Preview-arm64.tar.gz) | Local-browser UI-only preview |
| **Linux ISO** | [Data-only ISO](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Linux-UI-Preview-DATA-ONLY.iso) | **Non-bootable data image** containing a Linux x64 preview executable; not an OS or installer |
| **macOS Apple Silicon** | [macOS ARM64 tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-macOS-UI-Preview-arm64.tar.gz) | Unsigned/non-notarized local-browser UI-only preview |
| **Web** | [Web ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-Web-UI-Preview.zip) | Static HTML + Kotlin/JS UI-only preview |
| **iOS Simulator** | [Simulator ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/MitraWave-iOS-Simulator-UI-Preview.zip) | Unsigned **Simulator-only** preview, not a signed iPhone IPA |

[Verify SHA-256 checksums](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.8.0-multiplatform-preview/SHA256SUMS.txt)

The Android APK's **internal app version remains `0.7.0-dev` (versionCode 7)**; `0.8.0` names the combined download collection, not an Android source version. Windows and Linux x64 launches were verified; other platforms passed archive/build checks but not device-level functional tests.

## Rajni Web Developer owner identity — create on your device

The registered username is intended to be `@rajniwebdeveloper`, while the display name can be **Rajni Web Developer**. The server must **never** generate or distribute a shared private key for this account; each owner identity needs a device-generated private key.

On a trusted Android device:

1. Install the Android APK, open **Chats**, enter `rajniwebdeveloper`, and select **Register**. If the name is already registered, do not overwrite its key—only a matching key can log in.
2. Open **Settings → Private key import / export**, choose a strong backup password, and export your encrypted `.mwbackup`.
3. Keep that password and backup separate and secure. Import that file **before** trying to reconnect from another Android phone.
4. Check the displayed public fingerprint before treating the identity as verified. No owner account private key or backup is included in this public GitHub release.

**Important:** This is single-primary-device identity only. Multi-device linked keys, account recovery from the server, and portable chat history are **not implemented**.

## Live backend and database

- Public API health: [`https://trade.apihubs.in/mitrawave/healthz`](https://trade.apihubs.in/mitrawave/healthz)
- HTTPS API base: `https://trade.apihubs.in/mitrawave/`
- WebSocket notifications: `wss://trade.apihubs.in/mitrawave/v2/live`
- Go internal listener: `127.0.0.1:18482`, TLS terminated by Apache.
- **PostgreSQL 17:** durable username and public primary-device identity key directory (no private keys or chat history). Username-prefix lookup from Android, rate-limited and authenticated.
- **Redis:** non-persistent short-lived signed challenges, sessions, ciphertext inboxes (24-hour maximum expiry), and WSS tickets. Cache may be lost on service restart.
- **Self-deletion:** signed online deletion removes PostgreSQL identity entry and cached session/inbox state, then erases phone identity. Local-only erase leaves the PostgreSQL identity registered until online deletion. Separately exported backups and messages delivered to other people are unaffected.

## What was tested

**Passed:** Go race unit tests and vet; public TLS/health/readiness; signed registration/login; permanent PostgreSQL username prefix lookup; ciphertext relay/ACK; single-use WebSocket handshake; signed online deletion; CI Android build, Kotlin/JS web build, iOS Simulator build, desktop cross-compilation; Windows and Linux x64 local-launch health tests; archive integrity and SHA-256 checks.

**Not completed:** two physical Android devices exchanging and decrypting messages end-to-end; independent security audit and threat model; actual live messaging on Web, Windows, Linux, macOS, or iPhone; durable encrypted chat history; linked multi-device provisioning; Bluetooth/Wi-Fi offline mesh; calls; store-ready Android App Bundle and signing, iPhone IPA/signing/notarization, Play Store privacy-policy/Data-Safety/external account-deletion requirements.

MitraWave Android encryption is experimental P-256 ECDH/HKDF-SHA256/AES-256-GCM/ECDSA with first-use contact key pinning. It is **not** an independently validated Signal/Double-Ratchet implementation and does **not** provide all production E2EE security properties.

## Install safely

Android preview builds are debug-signed and may use different keys from earlier GitHub Actions builds. An in-place update can fail with a signature mismatch. **Before uninstalling an older APK**, export your encrypted identity backup and safeguard its password; uninstalling deletes local identity data. **The identity backup cannot recover chat messages.**

This public repository contains only `README.md`; compiled downloads are GitHub Release assets. Source is in a separate private repository.

Issues: [MitraWave-Public Issues](https://github.com/rajniwebdeveloper/MitraWave-Public/issues). Do not upload private keys, backups, secrets or personal messages.

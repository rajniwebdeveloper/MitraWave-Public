# MitraWave

<img src="https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.3.0-dev/MitraWave-App-Icon-512.png" width="112" alt="MitraWave app icon" />

### Stay Connected, Even Offline.

**MitraWave** is an experimental device-owned identity messenger. Android has a preliminary HTTPS/WSS encrypted message client; Windows, Linux, macOS, Web and iOS Simulator releases currently provide UI previews.

[**Download latest Android APK — v0.7.0-dev**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.7.0-dev/MitraWave-Android-v0.7.0-dev.apk) · [**View latest release**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.7.0-dev) · [**All releases**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases)

> **Developer preview — NOT a production-audited E2EE messenger.** No verified two-device interoperability test or Signal/Double-Ratchet protocol, no persistent encrypted chat history, no Bluetooth/Wi-Fi offline mesh, and no working calls. Do not send sensitive conversations.

## Downloads

| Platform | Download | Scope |
| --- | --- | --- |
| **Android 7.0+** | [APK v0.7.0-dev](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.7.0-dev/MitraWave-Android-v0.7.0-dev.apk) | Device-owned signed login, **PostgreSQL username search**, temporary WSS encrypted-message relay, in-app self-delete |
| **Windows x64** | [ZIP with EXE](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Windows-Desktop-Preview-amd64.zip) | Local browser UI preview |
| **Linux x86-64** | [tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-amd64.tar.gz) | Local browser UI preview |
| **Linux ARM64** | [tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-arm64.tar.gz) | Local browser UI preview |
| **Linux ISO** | [ISO](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Linux-Desktop-Preview-DATA-ONLY.iso) | **Data-only image, not bootable or an installer** |
| **macOS Apple Silicon** | [tar.gz](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-macOS-Desktop-Preview-arm64.tar.gz) | Unsigned UI preview |
| **Web** | [ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-Web-UI-Preview.zip) | Static browser UI preview |
| **iOS Simulator** | [ZIP](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.2.0-preview/MitraWave-iOS-Simulator-UI-Preview.zip) | Unsigned simulator app, **not an iPhone IPA** |

Latest Android: package `com.mitrawave.app`, versionCode `7`, versionName `0.7.0-dev`, minSdk 24, targetSdk 36. SHA-256 APK: `c1bfeabd9d9786deac5f6e1d372e4c90d3e2582e296e975eae16c0d5f242dbb3`.

## Device-owned account + PostgreSQL user search

- **Private identity stays on your phone.** Android creates the signing key locally and protects it with Android Keystore. Username registration and reconnect authenticate via short-lived cryptographic challenges, without a server-side password or OTP.
- **PostgreSQL 17 directory:** stable `@username` and public primary-device key records, searchable by username prefix in the Android Chats screen. Usernames survive Redis restarts and stay registered until signed account deletion. PostgreSQL stores **no private keys, passwords, chat messages or media**.
- **Device metadata:** the directory records the enrolled primary device ID and public key. Actual multi-device linking and secure approval of second devices are **not yet implemented**.
- **Redis:** temporary ciphertext messages (maximum 24-hour TTL), sessions, rate limiting and WSS notifications. Its disk persistence is disabled; queued messages can be lost during restart.
- **Account self-deletion:** Confirm **Delete my account** in Android Chats or Settings to delete PostgreSQL username and public device key, revoke Redis session/inbox entries, and erase the local private identity. **Offline local erase** cannot delete the PostgreSQL identity remotely.
- **Recovery:** Export a password-encrypted `.mwbackup` in Settings. It includes your local identity, username and optional recovery note, **not chat history**. Exported backups stored elsewhere and messages already received by other users are not deleted automatically.

## Live Go backend

- HTTPS status: [`https://trade.apihubs.in/mitrawave/healthz`](https://trade.apihubs.in/mitrawave/healthz)
- WebSocket: `wss://trade.apihubs.in/mitrawave/v2/live`
- Internal TCP: `127.0.0.1:18482`, with HTTPS termination by aaPanel Apache.
- Private Docker network: persistent PostgreSQL identity storage and memory-only Redis queue. Neither MitraWave database container publishes a host port.
- Verified live integration: signed account registration/reconnect, PostgreSQL username prefix search, key lookup, temporary relay/acknowledgement, authenticated WSS upgrade, signed account deletion and key removal. PostgreSQL identity persistence was separately tested across a Redis restart.

## Features

MitraWave's intended product includes device-owned identities, encrypted 1:1 chat, username search, trusted key verification, optional encrypted nearby Bluetooth/Wi-Fi messaging, group chats, private calls and opt-in multi-hop relay. **Many of these are not implemented yet.** The Android encryption is experimental (P-256 ECDH, HKDF-SHA256, AES-GCM, ECDSA and first-use key pinning); it lacks an audited ratchet, durable encrypted conversations, robust identity verification and multi-device support.

## Installation and privacy

Android APKs are developer/debug-signed. **Before uninstalling an older APK**, export an encrypted identity backup and save the password; different CI signing keys may prevent in-place upgrades. Uninstalling deletes local app data, and the identity backup cannot recover messages.

This repository contains **only `README.md`**. The APK and other compiled files are GitHub Release assets; the implementation source remains in a separate **private repository**. Real-device testing, external account-deletion web flow, privacy policy, Data Safety declarations, security review and a properly signed production build remain to be completed before a Play Store production launch.

Please report issues via [GitHub Issues](https://github.com/rajniwebdeveloper/MitraWave-Public/issues) without sharing passwords, message contents or private keys.

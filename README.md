# MitraWave

### Stay Connected, Even Offline.

**MitraWave** is a privacy-first messenger designed to bring together online chat, trusted nearby connections, and encrypted mesh delivery in one experience.

[**Download Android APK**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/tag/v0.1.0-dev) · [**All Releases**](https://github.com/rajniwebdeveloper/MitraWave-Public/releases)

> **Available download:** v0.1.0-dev is an **Android UI preview**, not a functioning messenger. It lets you explore the Chats, Nearby, Calls, Groups and Settings screens. Authentication, actual message delivery, encryption, and nearby transfers **do not yet work** in this APK. Please do not use it for sensitive communication.

## Features

MitraWave's feature set is designed around privacy and connectivity. **This section describes the product's feature design, not functionality available in the current preview APK.**

| Experience | Features |
| --- | --- |
| **Secure accounts** | Unique @username or email + password; no phone number or OTP required; device management |
| **Friends & identity** | Username search, friend requests, QR invitations, security-key QR verification, blocking |
| **Private conversations** | End-to-end encrypted individual chats, encrypted local chat history, replies, reactions and read receipts |
| **Online messaging** | Real-time chat, delivery acknowledgements, typing indicators, encrypted offline delivery queue |
| **Nearby offline chat** | Bluetooth discovery and direct Wi-Fi-capable nearby transfer without internet, subject to phone permissions and platform limits |
| **Smart mesh relay** | Optional encrypted store-and-forward via consenting nearby devices, with expiry and bounded hop counts |
| **Media sharing** | Photos, videos, documents, voice messages, stickers and emoji |
| **Calls** | Private voice and video conversations |
| **Communities** | Groups, channels, admin controls, topics and polls |
| **Privacy & personalization** | App lock, disappearing messages, device verification, light/dark themes and chat settings |
| **Cross-platform** | Android, iOS and Web product architecture; some offline features are mobile-only |

### How encrypted mesh delivery is designed

**Alex → Alexa → Sam:** Alex sends a message addressed to Sam. If Sam is offline, an eligible, consenting relay such as Alexa can temporarily carry an encrypted envelope. When Alexa and Sam come within supported Bluetooth/Wi-Fi range, Sam may receive and decrypt it on his own device. Relay users are not supposed to see message contents. Delivery depends on device connectivity, permissions and operating-system limitations.

## Current Android Preview

The downloadable **v0.1.0-dev** APK includes:

- Chats list, sample conversations and search/filter UI
- Nearby screen with relay setting preview
- Calls, Groups and Settings navigation screens
- System light/dark theme support
- Kotlin-based Android app prototype

**Preview screens and toggles are demonstrations only. There is no functioning backend, secure messaging, or mesh transport in this release.**

## Download & Compatibility

| Item | Value |
| --- | --- |
| App | MitraWave |
| Release | v0.1.0-dev — Android debug UI preview |
| Package | `com.mitrawave.app` |
| Minimum Android | 7.0 (API 24) |
| Target Android | 16 (API 36) |
| APK file size | Approximately 17.7 MiB |
| SHA-256 | `71116ca84d407db740ba766adafdfe3ab8a4582d90972865a37d4f4dc7dcc755` |

**[Download MitraWave Android APK](https://github.com/rajniwebdeveloper/MitraWave-Public/releases/download/v0.1.0-dev/MitraWave-Android-v0.1.0-dev.apk)**

Download from GitHub Releases, verify the checksum if desired, and install through Android's standard package installer. This build is for UI testing.

## Repository & Releases

This **public repository contains only `README.md`**. Android binaries are provided **exclusively as GitHub Release assets**; implementation source remains in a separate private repository and is not published here.

## Feedback

You can share suggestions and bug reports through the repository's **Issues** tab. Never include passwords, private encryption keys, or personal chat content in public reports.

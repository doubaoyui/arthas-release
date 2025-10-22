# Privacy Policy

_Last updated: October 22, 2025_

## 1. Overview

Arthas is a desktop application that bundles a Svelte frontend with a Tauri-based Rust backend and optional Node sidecars. This Privacy Policy explains what information the application processes, how that information is used, and what control you retain. Arthas is designed to run primarily on your device; we do not operate any cloud back-end for this product.

## 2. Information We Do Not Collect

Arthas does **not** create user accounts, profile you, embed tracking pixels, or send analytical telemetry to the project maintainers. We do not sell or rent personal data, and we do not embed third-party advertising or analytics SDKs.

## 3. Information Stored Locally

All persisted data remains on the device where you install Arthas. Typical storage locations are the operating system’s application data folders (for example, `%APPDATA%\arthas` on Windows, `~/Library/Application Support/arthas` on macOS, or `~/.local/share/arthas` on Linux/WSL). The application keeps the following records:

- **Application settings (`settings.json`)** – UI preferences, terminal profiles, and integration switches are stored via `tauri-plugin-store`. If you enable the WeChat integration, your AppID, AppSecret, and optional default cover media ID are written into this file in plain text so the desktop app can reconnect.
- **Operational logs** – Runtime diagnostic logs are written to the OS-specific log directory (for example, `%LOCALAPPDATA%\arthas\logs`). Logs contain timestamps, component names, and error messages that help troubleshoot crashes. They do not include your WeChat credentials or workspace content.
- **WeChat media cache** – When you upload cover images for WeChat drafts, resized copies and metadata (`image-cache.json`) are stored under a `wechat/` subdirectory next to the settings file so the app can avoid re-uploading identical files.
- **Cline sidecar assets** – To power AI-assisted workflows, Arthas decomposes a packaged `cline-core` runtime into a local cache directory. This contains executables and extension bundles only; it does not hold your prompts unless the underlying provider stores them.
- **Window and workspace state** – The filesystem indexer and window manager keep ephemeral information about the folders you open (paths, file names, change counters) strictly in memory or in temporary files under the same app data directory. This information is never uploaded by Arthas itself.

Deleting the application data directory and the log directory removes all of the data described above.

## 4. How Arthas Uses Network Access

Arthas only touches the network for the scenarios below. Each one is optional and triggered by user configuration or explicit actions:

- **Automatic updates** – The built-in updater fetches version metadata from `https://raw.githubusercontent.com/doubaoyui/arthas-release/main/updater.json`. The request contains standard HTTP headers (for example, your IP address and user agent supplied by the OS). No additional personal data is transmitted.
- **WeChat Official Account publishing (optional)** – If you supply AppID and AppSecret credentials, Arthas requests an access token from `api.weixin.qq.com` and uploads draft content and cover images you choose. The data sent is limited to the article HTML you generate, the media files you select, and the credentials required by WeChat.
- **AI provider integrations (optional)** – Arthas launches a local `cline-core` sidecar that relays prompts, source code, and other context you provide to whichever model endpoints you configure inside Cline (for example, OpenAI or other LLM vendors). The project does not operate those endpoints; any data you send is governed by the third-party provider’s policies.
- **Local services** – The Rust backend exposes HTTP and gRPC bridges on `127.0.0.1` (default ports 26040–26050) so the UI and sidecars can communicate. These endpoints never listen on external interfaces.

Arthas performs no background synchronization with cloud storage and does not send your file contents anywhere unless you enable one of the integrations above.

## 5. Your Choices and Data Control

- **Disable integrations** – Leave integration switches (for example, WeChat or AI providers) blank to keep the application fully offline.
- **Clear stored data** – Delete the Arthas application data directory and log directory to remove configuration, caches, and logs. You can do this manually or via the operating system’s storage manager.
- **Revoke credentials** – Change or delete your WeChat credentials in `settings.json` (or through the Arthas settings UI) if you believe they have been exposed. You may also revoke them inside the WeChat Official Account console.
- **Firewall rules** – You can block outbound connections to GitHub, WeChat, or third-party AI endpoints; Arthas will continue to function for offline-only features.

## 6. Data Security

Because Arthas stores configuration files in plain text for compatibility across platforms, protect your device with operating system user accounts, disk encryption, and antivirus software. We recommend keeping your system up to date and restricting physical access to machines that store WeChat or AI provider credentials.

## 7. Children’s Privacy

Arthas is intended for use by adults and is not marketed to children under 13. We do not knowingly collect personal data from children.

## 8. Changes to This Policy

We may update this Privacy Policy when Arthas gains new capabilities or when regulations change. Material updates will be reflected in the project release notes and the “Last updated” date above. Continued use of the application after a revision signifies acceptance of the updated terms.

## 9. Contact

If you have questions about this Privacy Policy or need assistance deleting stored data, please open an issue in the project’s GitHub repository (`https://github.com/doubaoyui/arthas`) or contact the maintainers through the release channel where you obtained the installer.



# Tauri Foundation

> The goal of this repository is to serve as a starting point and reference for all
  Tauri apps built with Vite, React, and TypeScript — tested, signed, and
  distributed automatically with GitHub Actions for macOS (Apple Silicon),
  Windows, Linux x64, and Linux ARM64 (Raspberry Pi).

## Contents

- Root UI in [`index.html`](index.html) and [`src/main.ts`](src/main.ts).
- Desktop shell in [`src-tauri/tauri.conf.json`](src-tauri/tauri.conf.json),
  [`src-tauri/Cargo.toml`](src-tauri/Cargo.toml),
  [`src-tauri/src/main.rs`](src-tauri/src/main.rs), and
  [`src-tauri/src/lib.rs`](src-tauri/src/lib.rs).
- App icons in [`src-tauri/icons/`](src-tauri/icons/).
- CI in [`.github/workflows/tauri.yml`](.github/workflows/tauri.yml).

## Develop

```sh
npm install
npm run tauri dev
```

## Build

```sh
npm run build
npm run tauri build
```

## Links

- [Tauri v2 docs](https://v2.tauri.app/)
- [Tauri GitHub Action](https://github.com/tauri-apps/tauri-action)
- [Icons reference](https://v2.tauri.app/develop/icons/)

## CI

| Job                         | Runner            | Formats       | Artifact           |
| ---------------------------- | ------------------ | ------------- | ------------------ |
| Windows                      | `windows-latest`   | `nsis`, `msi` | `tauri-windows`    |
| macOS (Apple Silicon)        | `macos-26`         | `dmg`, `app`  | `tauri-macos-arm64`|
| Linux x64                    | `ubuntu-latest`    | `deb`, `appimage` | `tauri-linux-x64` |
| Linux ARM64 (Raspberry Pi)   | `ubuntu-24.04-arm` | `deb`, `appimage` | `tauri-linux-arm64` |

The `nsis`, `msi`, `dmg`, `deb`, and `appimage` formats are bundled, and all
bundles are uploaded as artifacts.

## App updates

This repository configures Tauri with `"updater": { "active": false }`,
so no update endpoint is polled.

The Rust plugin updater is enabled inside its `Cargo.toml` to keep the
update path functional. To enable updates in your app, you need to:

  1. Generate an update signing key pair: `npx tauri signer generate`.
  2. Add the private key and its password as repo secrets
     (`TAURI_SIGNING_PRIVATE_KEY`, `TAURI_SIGNING_PRIVATE_KEY_PASSWORD`).

## Notes

- This repository is public by design: it is what makes the GitHub Actions minutes (including macOS and ARM64 Linux runners) free and unlimited. Do not commit secrets to it; signing material belongs in GitHub Actions secrets only.
- Raspberry Pi targets assume a 64-bit Raspberry Pi OS (Pi 3/4/5). The app uses the system WebKitGTK webview, which Raspberry Pi OS provides.

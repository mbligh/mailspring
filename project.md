# Mailspring Monterey fork

## Purpose
Maintain the Mailspring desktop client for Intel Macs running macOS Monterey 12.7.x, starting from upstream 1.23.0. Keep changes directly on `main`.

## Implementation
- On macOS, left-clicking the menu-bar tray icon activates the main window; right-click displays the existing menu. Other platforms retain their existing tray behavior.
- The application bundle remains named `Mailspring.app`; Finder may rename an existing duplicate if both copies are retained.
- Electron is pinned to 41.7.2 in `package.json`. Avoid upgrades that drop macOS 12.
- UI and packaging live in this repository; the C++ `mailsync` engine is an upstream submodule, with a prebuilt binary downloaded during `npm install`.
- `.github/workflows/build-monterey.yml` builds the Intel `Mailspring.app` on an Intel macOS GitHub runner and uses the upstream build script without its ZIP installer, then creates a DMG containing `Mailspring.app` and a drag-to-Applications shortcut.
- Successful builds replace `Mailspring-Monterey.dmg` on the fixed `monterey-latest` GitHub release.

## Build and download
- Workflow: https://github.com/mbligh/mailspring/actions/workflows/build-monterey.yml
- Stable download (after first successful build): https://github.com/mbligh/mailspring/releases/download/monterey-latest/Mailspring-Monterey.dmg
- Builds run on pushes to `main` and via `workflow_dispatch`.
- The app is **unsigned and unnotarized**; Gatekeeper may require explicit authorization. Packaging on macOS 15 does not itself establish compatibility with Monterey; test on macOS 12.7.

## Follow-up
- Verify the new DMG and tray interactions on Monterey 12.7 (left-click when hidden/minimized/background, right-click menu).
- Selectively backport upstream security fixes, privacy fixes, and sync correctness changes while retaining Monterey support.

# Mailspring Monterey fork

## Purpose
Maintain the Mailspring desktop client for Intel Macs running macOS Monterey 12.7.x, starting from upstream 1.23.0. Keep changes directly on `main`.

## Implementation
- Electron is pinned to 41.7.2 in `package.json`. Avoid upgrades that drop macOS 12.
- UI and packaging live in this repository; the C++ `mailsync` engine is an upstream submodule, with a prebuilt binary downloaded during `npm install`.
- `.github/workflows/build-monterey.yml` builds the Intel `Mailspring.app` on an Intel macOS GitHub runner and creates `Mailspring.zip` with the existing build script.
- Successful builds replace `Mailspring-Monterey.zip` on the fixed `monterey-latest` GitHub release.

## Build and download
- Workflow: https://github.com/mbligh/mailspring/actions/workflows/build-monterey.yml
- Stable download (after first successful build): https://github.com/mbligh/mailspring/releases/download/monterey-latest/Mailspring-Monterey.zip
- Builds run on pushes to `main` and via `workflow_dispatch`.
- The app is **unsigned and unnotarized**; Gatekeeper may require explicit authorization. Packaging on macOS 15 does not itself establish compatibility with Monterey; test on macOS 12.7.

## Follow-up
- Confirm that the first CI build installs dependencies, includes the sync engine, and runs on Monterey.
- Selectively backport upstream security fixes, privacy fixes, and sync correctness changes while retaining Monterey support.

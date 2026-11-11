# Mailspring (Monterey fork)

## Requirements

- Maintain an installable Intel macOS 12 (Monterey) version of Mailspring under the app name **Mailspring**.
- Deliver the app as a DMG, not a ZIP; keep the existing sync engine bundled.
- Left-clicking the macOS status-bar icon brings the window to the front; right-clicking retains its menu.
- Show media attachments without distorting or severely cropping their aspect ratio. Video attachments use a full-frame preview while ordinary document thumbnails remain compact.

## Implementation

- Electron/React/TypeScript app with the existing Mailspring-Sync native backend.
- Received-message attachments render via `app/internal_packages/attachments/lib/message-attachments.tsx` and `app/src/components/attachment-items.tsx`. Styling is in `app/static/style/components/attachment-items.less`.
- macOS Quick Look generates the video-preview PNG; the attachment component displays it as a responsive image with a height cap and `object-fit: contain`. Other file types retain the existing cropped strip layout.
- Commits to `main` trigger `.github/workflows/build-monterey.yml`, producing a DMG and updating the `monterey-latest` GitHub release asset.

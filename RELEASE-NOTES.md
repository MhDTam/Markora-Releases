# Markora V1 · 1.0.0

The first public binary release of Markora for Windows x64. Arabic and English interfaces, glass light/dark themes, compact capture and a full annotation editor.

## Included

- Portable ZIP and Windows installer, with SHA-256 checksums and upstream license notices.
- Region/window/full-screen capture, independent timer modes, original-resolution PNGs, clipboard copy and configurable export quality.
- Grouped drawing tools, curved connectors, text, callouts, steps, selection, annotation eraser and editable projects.
- Mini startup, configurable save folder, opt-in automatic saving and three recent captures.
- Optional Gemini OCR with keys stored in Windows Credential Manager.
- In-app update notifications on startup and in Settings, linking directly to the latest GitHub release page.

## Stability and performance work

- Restored missing Home navigation at intermediate editor widths and corrected narrow-window toolbar spacing.
- Preserved Mini's position after moving an expanded timer or gallery.
- Kept timer and direct captures independent, including cancellation of a pending countdown.
- Protected unsaved edits when exiting from the system tray.
- Fixed Escape cancellation during an eraser gesture and case-insensitive `.markora` file extensions.
- Guarded image loading against stale asynchronous results and blocked copy/export until the raster is ready.
- Validated project IDs, geometry, colors and resource limits before importing.
- Loaded the editor only when needed, resized window-preview pixels before encoding, paused hidden-window polling and released the region overlay raster after capture/cancel.
- Bounded retained undo rasters to a 96 MiB estimate, while preserving the immediate undo state.

## Validation

Production Windows build and installer packaging; 19 JavaScript unit tests; 13 Rust unit tests (plus 3 opt-in desktop tests); warning-free release Clippy; native WebView2 regression, Mini, editor, callout, OCR, region/full-screen capture, and update-notification smoke suites. See [QA validation](QA.md) for exact scope and observations.

On the development PC, one idle-Mini sample showed JavaScript heap changing from 10.42 MiB to 6.49 MiB after lazy loading. Aggregate process memory changed only slightly; measurements depend on Windows, WebView2 and hardware. This is not a minimum-memory specification.

## Notes

Requires Windows 10/11 x64 and WebView2. Binaries are unsigned. Gemini OCR requires internet, a valid user-supplied key and provider availability. Protected or restricted windows may refuse capture. Updates are checked via GitHub Releases and downloaded/installed manually by opening the release link; automatic silent binary replacement is not performed. Installer packaging was verified; an installation over an existing user installation was not performed during the audit.

This release publishes binaries and documentation; Markora's application source remains private.

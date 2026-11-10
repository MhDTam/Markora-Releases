# Markora 1.0.0 validation

Tested on an interactive Windows desktop on 2026-11-10. These results describe the exercised workflows, not a guarantee that every possible device/window combination is bug-free.

| Check | Result |
| --- | --- |
| TypeScript, Vite and Windows release build | Passed |
| NSIS x64 installer packaging | Passed; existing user installation was not overwritten for testing |
| JavaScript unit tests | 17 passed |
| Rust tests | 8 passed; 3 opt-in interactive tests excluded from this unit run |
| Release Clippy with warnings as errors | Passed |
| Production npm dependency audit | No known advisories reported at audit time |
| Five native editor window sizes | Header controls do not overlap; Home remains available |
| Maximize / restore / Mini transitions | Native viewport fills correctly; original session retained |
| Open and minimized window capture from Mini | Passed using an owned Chrome test window |
| Region / window / full-screen / timed capture | Passed using real Windows capture commands |
| Timed region / timed window / timed full screen | Passed; window selected before countdown |
| Cancel timer then direct capture | No delayed ghost capture after original timer elapsed |
| Mini timer: Arabic/English × light/dark | Bounded fields; seven-second custom input; presets, repeat and Escape cancellation passed |
| Move expanded Mini, then close popup | New position retained |
| Copy image without saving | Native clipboard command passed |
| Three recent captures, reload, opt-in auto-save | Passed; autosave test used an isolated output folder |
| Eraser gesture / undo / Escape | Original raster preserved; annotation erase is undoable; cancelled gesture restored |
| Selection / text / steps / Shift constraints | Native editor workflow tests passed, including Arabic labels in English UI and vice versa |
| Professional callout styles | Minimal/elbow/plate creation, anchored movement, bends, endpoint swap, roundtrip and zoom/pan export invariance passed |
| Callout screen/export geometry | Sparse edge-antialiasing tolerance, at most 512 channel values with delta at most 32 at 100%; viewport includes the whole raster |
| Import validation | Rejects malformed geometry, duplicate/unsafe IDs and unsupported raster metadata; bounds object/point counts |
| Region overlay memory | Captured image element cleared after selection |
| Tray exit with unsaved annotation | Confirmation shown; document not silently discarded |
| Gemini OCR | Real owned Arabic/English fixture recognized in about 2.4 s; existing Windows Credential Manager key used, never logged |
| Release screenshots | Actual native app, owned generated demonstration documents only |

Annotation export/project tests intercept the native save-dialog transport and inspect its payload; they do not claim an automated test of clicking the Windows file dialog. Native capture, clipboard, window state and opt-in autosave use real commands.

## Resource observations

One five-second idle-Mini sample per build on the same development PC:

| Metric | 0.28.1 | V1 candidate |
| --- | --- | --- |
| JavaScript heap | 10.42 MiB | 6.49 MiB |
| Aggregate private process memory | 289.8 MiB | 285.8 MiB |
| Aggregate working set | 458.6 MiB | 450.2 MiB |
| CPU, percentage of one core over sample | 0.57% | 0.00% |

The process tree includes WebView2 browser, renderer, GPU and utility processes. Working sets can include shared pages; CPU, memory and timings vary with Windows/runtime/hardware and these short observations are not performance guarantees. The editor's roughly 390 kB JavaScript chunk is absent during a fresh Mini startup. Preview resizing now happens before PNG/base64 encoding; hidden picker polling stops; finished region rasters are released; retained unique undo rasters have a 96 MiB estimate budget (the newest undo state is always kept).

## Remaining platform limits

Protected windows may reject Windows Graphics Capture. OCR depends on a valid key, network, Google quotas and model availability. V1 has no automatic updater and its binaries are unsigned. Further hardware/DPI testing and user bug reports remain useful; do not publish API keys or private captures with reports.

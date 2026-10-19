# Claude Desktop + IconVectors MCP walkthrough

[Watch or download the 40-second walkthrough](media/claude-desktop-iconvectors-walkthrough.mp4) (H.264 MP4, 1920x1080, 813,774 bytes).

This Windows example uses one Lucide folder SVG, a stroke change to `#E11D48`, and transparent PNG exports at **16, 24 and 32 pixels**. The video uses real historical Claude tool panels, an actual IconVectors result screenshot, direct renders of the saved SVGs and the verified PNG files. It is an edited walkthrough of a completed run, **not uninterrupted live execution or a speed benchmark**. Internal directory text in the video is blurred; filenames and size results remain visible.

## Prerequisites

- Windows with IconVectors **2.10** installed and running. The validated application version was **2.10.0.0**. IconVectors is commercial software; install it separately from the [official download page](https://iconvectors.io/download.html).
- [Claude Desktop for Windows](https://claude.com/download), signed in with permission to use local extensions. The tested client version was **2.42304.0.0**; this is a test record, not a minimum-version claim.
- The official `Axialis-IconVectors-Claude.mcpb` bundle **2.10.0**, installed and enabled with its requirements met. The verified bundle's companion matched the previously inspected installation. Use the matching bundle supplied with IconVectors, not a similarly named package.

Follow the [official Claude setup guide](https://iconvectors.io/help/using-iconvectors-with-claude-anthropic.html). For the tested client, the local installation route was Settings > Extensions > Advanced settings > Install Extension; Add custom connector is not this local MCPB workflow. Approve the extension and individual tool requests as appropriate. Preserve other extensions/settings. Claude launches the stdio companion; the local application bridge used `127.0.0.1:61337`, not a remote HTTP MCP URL.

## Workflow and observed outcome

1. Copy [source/folder.svg](../examples/claude-desktop-walkthrough/source/folder.svg) into a disposable working directory. Keep the source unchanged and choose new output filenames.
2. Check application identity with `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Inspect the current document before opening the working copy with `document_open`; do not replace unrelated unsaved work. `render_previewPng` provides a real preview.
3. Inspect the SVG and current path target with `document_getSvg`, `dom_query` and `dom_getElement`. The successful resumed run used `dom_setAttributes` to set that path's stroke to `#E11D48`. Reacquire the target from the current document; an ordinal from another session is not reusable. Reinspect and save only the working copy.
4. Export three new PNGs with `export_toBitmap`, using the size syntax below. Check each returned size and the actual file before continuing.

The initial `dom_setStyle` attempt timed out; it is not presented as successful. The workflow resumed after inspection. The first export used `size: {width:16,height:16}` and produced a real 24x24 file instead. The corrected calls below produced the verified sizes. A timeout is not evidence that a write was cancelled: inspect state and outputs before any retry.

## Correct pixel export arguments

For `export_toBitmap`, replace the placeholder with a new absolute Windows output path visible to IconVectors. This is an argument example, not a shell command:

```json
{
  "path": "<NEW_ABSOLUTE_WINDOWS_PATH_TO_folder-16px.png>",
  "formatName": "png",
  "size": {
    "mode": "pixels",
    "widthPx": 16,
    "heightPx": 16,
    "keepAspectRatio": false
  }
}
```

For the other outputs, set **both** `widthPx` and `heightPx` to **24**, then **32**, and use distinct new filenames. Do not use `width`/`height` or resize the document canvas. The installed schema exposes `size` as an object without detailing its fields; this explicit shape was verified through Claude Desktop. No overwrite guard is assumed: confirm each destination is absent before export.

## Verified files and limitations

| Genuine output | Decoded dimensions | Bytes |
| --- | --- | --- |
| [folder-16px.png](../examples/claude-desktop-walkthrough/png/folder-16px.png) | 16x16 | 323 |
| [folder-24px.png](../examples/claude-desktop-walkthrough/png/folder-24px.png) | 24x24 | 372 |
| [folder-32px.png](../examples/claude-desktop-walkthrough/png/folder-32px.png) | 32x32 | 569 |

Independent decoding checked transparency, nonempty content and the expected recoloring. Visual inspection found no obvious clipped stroke. The 16px result has softer antialiasing, including low-alpha pixels at the left/right border; this is not a pixel-perfect claim. The preserved source and protected reference files remained unchanged. The [saved recolored SVG](../examples/claude-desktop-walkthrough/result/folder.svg), [asset provenance, hashes and original license notices](../examples/claude-desktop-walkthrough/NOTICE.md) accompany the outputs.

The test also reported a runtime-directory discovery warning and an `unknown` build identifier; those were not repaired or evidence of a broader compatibility PASS. Do not generalize this one Windows/client/application combination to every MCP client or release.

For connection issues, see [troubleshooting](troubleshooting.md). The separate [SVG-to-PNG batch workflow](https://github.com/axialis-software/iconvectors-svg-png-workflow) documents a different, 12-icon example; this walkthrough is a single-icon MCP demonstration.

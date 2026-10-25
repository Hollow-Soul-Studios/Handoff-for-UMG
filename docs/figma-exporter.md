# Figma exporter

The companion exporter is a free Figma plugin that works with Figma design. It exports the frames you select to a
tool-neutral `.handoff.zip` (`layout.json` plus PNG and optional SVG assets) that the Unreal importer turns into Widget
Blueprints. It ships prebuilt with the plugin download in `HandoffForUMG/Extras/FigmaExporter/` (see the README there).

* Works offline: its manifest declares no network access. Nothing is uploaded.
* No REST API, no access token, no Enterprise plan: it reads the file through the Figma Plugin API.
* Exports are deterministic; exporting the same design twice gives the same package (apart from the export timestamp).

*Figma is a trademark of Figma, Inc. The exporter is an independent tool and is not affiliated with or endorsed by
Figma.*

## Install

No build step and no Node.js: the plugin download already contains the built exporter.

1. Find the installed plugin folder: for a Fab install to the engine,
   `<UE install>/Engine/Plugins/Marketplace/HandoffForUMG/`; for a project install, `<Project>/Plugins/HandoffForUMG/`.
2. In the Figma desktop app choose **Plugins > Development > Import plugin from manifest...** and pick
   `Extras/FigmaExporter/manifest.json` in that folder.
3. Keep the folder in place: Figma loads `dist/code.js` and `dist/ui.html` next to the manifest.

## Export

1. Select the top-level frames, components or component sets to export, or select nothing to export every top-level
   frame on the current page.
2. Run **Plugins > Development > Handoff exporter for Figma design > Export for Unreal Engine...**
3. Choose the options and press **Export .handoff.zip**.

| Option | Meaning |
|---|---|
| Image scale | `1x and 2x` (default), `1x only` or `2x only` PNGs for rasterised layers |
| Include SVG | Also write an informational `.svg` for vector layers |
| Only selection | On: the selection (or all frames if nothing is selected). Off: all frames on the page |

The **Warnings** list after an export names layers the importer will approximate or cannot reproduce (mixed text
styles, missing fonts, unsupported effects and so on).

## Tag layers

Tags go in the **Layer tags** tab or in the layer name:

```
Play Button [button] [focus] [action=IA_Confirm]
Panel [9slice=16]            Panel [9slice=12,12,16,16]
HUD [safezone]               Logo [rasterize]              Debug [ignore]
Icon [widget=Image]          Header [inline]
```

What each tag does in Unreal: [Feature mapping](FeatureMapping.md).

## Import receipt (status write-back)

After an import, Unreal writes `<package>.receipt.json`. In the exporter run **Load import receipt...** and choose it.
Each layer then shows its import status and the Unreal asset it maps to. This stores a few plugin-data keys on your
nodes (`handoff.status`, `handoff.ueAsset`, `handoff.ueWidget`, plus `handoff.exportedAt` on exported frames); these
are the only changes the exporter makes to your Figma file.

## Next steps

Import the zip in Unreal: [Quick start](QuickStart.md). Re-importing after design changes:
[Re-import rules](ReimportRules.md).

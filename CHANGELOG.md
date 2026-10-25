# Changelog

All notable changes to Handoff for UMG. Format loosely follows [Keep a Changelog](https://keepachangelog.com/).
Plugin versions use `MAJOR.MINOR.PATCH`.

## 1.0.0

First public release. Supports Unreal Engine 5.8 (tested) and 5.7 (one plugin package per engine version).

### Import
* Imports a `.handoff.zip` design package (also a package folder or a `layout.json`) into Widget Blueprints, one
  `WBP_<Frame>` per top-level frame.
* Constraints become Canvas Panel anchors; auto layout becomes Horizontal, Vertical or Wrap boxes; rectangles become
  Border, Image or Size Box; text becomes Text Block; spacers and components (child Widget Blueprints, or inline with
  `[inline]`) are supported.
* Texture import with UI settings, 1x or 2x; 9-slice margins (`[9slice=...]`); safe-zone wrapper (`[safezone]` or
  project option).
* Layer tags: `[button]`, `[focus]`, `[9slice=...]`, `[action=...]`, `[safezone]`, `[inline]`, `[ignore]`,
  `[rasterize]`, `[widget=...]`.
* Plan step: **Plan** shows every change in a Changes / Re-link / Fonts / Messages window before **Apply** writes
  anything.
* Preview window at 1920x1080, 2560x1440, 1280x800 and 2532x1170 (configurable), rendered with the project DPI curve.

### Re-import
* Three-way merge per property (last import, current asset, new package); Unreal-side edits are kept by default.
* Identity by node id, with automatic re-link by hierarchy path, layer name, type and geometry above a strict
  threshold, and a **Re-link** tab for suggestions and manual links.
* Widgets referenced by graphs, bindings, animations or `BindWidget` members are locked and never removed; widgets you
  added by hand are never touched.
* Container swaps keep slot edits made in Unreal where both slot types share the field.
* Deterministic manifest in `<Project>/Handoff/Manifests/` (commit it with your assets).
* Safety net: backup of affected `.uasset` files and the manifest to `Saved/HandoffBackups/<timestamp>/` before apply,
  **Restore last import**, optional source control check-out.

### Fonts and styles
* Font mapping table (composite font assets or TTF/OTF files), search folders, reuse of earlier imports; missing
  fonts are flagged, never silently replaced. No fonts are bundled.
* Optional, user-triggered download of Google Fonts that are published under the SIL OFL, saved with the OFL text.
* CommonUI mode: `UCommonTextBlock` with generated `UCommonTextStyle` subclasses, button sets as `UCommonButtonBase`
  subclasses with `UCommonButtonStyle`, `UCommonActivatableWidget` screens, default focus, `[action=...]` input actions
  (Enhanced Input path on 5.8; legacy data table path on 5.7).

### Automation
* Python API `unreal.HandoffLibrary` (import, plan, restore, Google Font download, REST fetch).
* Commandlet `-run=HandoffImport` with `-Plan`, `-Explain`, `-Render`, `-Relink`, `-Report`, `-FailOnConflicts`,
  `-Restore` and CI exit codes (0, 1, 2).
* Console commands `Handoff.Import`, `Handoff.Preview`, `Handoff.SaveImportWindowShot`, `Handoff.SaveWindowShot`.
* Optional REST fetch from Figma for Dev and Full seats (token stored per user, never in the project).
* Import receipts (`<package>.receipt.json`) that the exporter can write back to Figma plugin data.

### Support tools
* **Tools > Handoff for UMG > Check Setup...** (16 health checks, HC01 to HC16) and **Create Support Bundle...**.
* Console `Handoff.Health` and `Handoff.SupportBundle`, Python `run_health_check()`, `health_check_report()` and
  `create_support_bundle()`, `Content/Python/handoff_support.py`, commandlet `-Health` and `-SupportBundle`.

### Companion exporter
* Free Figma exporter plugin, shipped prebuilt in `Extras/FigmaExporter` (no build step): exports selected frames to
  `.handoff.zip` with PNG/SVG assets, deterministic output, layer tag editor, import receipt write-back. Works offline
  and uses no REST API.

### Samples and documentation
* `MainMenu_v1.zip` and `MainMenu_v2.zip` sample packages and the v1 to v2 re-import scenario.
* Quick start, feature mapping, re-import rules, fonts and styles, automation, troubleshooting, layout schema, design
  log.

### Known limits
See the [plugin README](docs/plugin-readme.md#known-limits).

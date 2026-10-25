# Roadmap

Planned work after 1.0. This is a statement of intent, not a promise of dates; the order may change with user
feedback. Vote with a thumbs-up on the matching [feature request](../../issues?q=label%3Aenhancement).

## Next (v1.x)

* **Spatial navigation-rule suggestions** for CommonUI screens.
* **MVVM ViewModel stubs** generated for imported screens.
* **String Table localization** for imported text.
* **Photoshop and Penpot exporters** that write the same tool-neutral package format.
* **MCP / agent-callable wrapper** around the existing Python API (the Python API and the `HandoffImport` commandlet
  already ship in 1.0).

## Always

* A build within 14 days of each Unreal Engine minor release; the latest 2 to 3 engine versions supported.
* Updates for changes in the Figma developer platform.
* Patches every 2 to 4 weeks for the first three months, then monthly.

## Non-goals

* No runtime module; the plugin stays editor-only.
* No full UMG-to-Figma round trip beyond the import status write-back.
* No gameplay logic generation.
* No exact fidelity for vector boolean operations or blur (they are rasterised).
* No UEFN or Verse target.
* No prototype-flow graphs.

# Handoff for UMG

Documentation, support and issue tracker for **Handoff for UMG**, an Unreal Engine editor plugin that imports a design
package into Widget Blueprints and lets you re-import after the design changes without losing your graphs, bindings or
hand edits.

This repository contains **documentation and issues only**. The plugin itself is distributed through Fab and its source
is not hosted here.

## What it is

* Works with Figma design through the free companion exporter plugin, shipped prebuilt in the plugin download
  (`Extras/FigmaExporter`). The package format is tool-neutral ([layout schema](docs/LayoutSchema.md)), so other
  exporters can target it.
* Output is ordinary UMG: Canvas Panel anchors, Horizontal/Vertical/Wrap boxes, Borders, Images, Text Blocks, Size
  Boxes, Spacers and child Widget Blueprints for components. Optional CommonUI mode generates text styles, button
  styles, `CommonButtonBase` buttons and `CommonActivatableWidget` screens.
* Re-import is a 3-way merge. A property you changed in Unreal is never overwritten unless you choose "Take Figma",
  and every change is shown in a diff window before anything is written. A backup is taken before every apply and
  **Restore last import** puts the files back.
* Editor only. There is no runtime module, and nothing from the plugin ships in your packaged game.
* Automation: Python (`unreal.HandoffLibrary`), a `HandoffImport` commandlet for CI, and console commands.
* Built-in **Check Setup** health checks and a **support bundle** for issue reports (nothing is uploaded).

Requirements: Unreal Engine 5.7 or 5.8 (built and tested on 5.8). Windows is the tested platform; Mac and Linux are
allow-listed in the plugin modules but untested. Details: [plugin README](docs/plugin-readme.md).

*Figma is a trademark of Figma, Inc. Handoff for UMG is an independent product and is not affiliated with or endorsed by
Figma. Unreal Engine is a trademark of Epic Games, Inc.*

## Documentation

Start at the [documentation index](docs/index.md):

* [Quick start](docs/QuickStart.md)
* [Feature mapping](docs/FeatureMapping.md)
* [Re-import rules](docs/ReimportRules.md)
* [Fonts and styles](docs/FontsAndStyles.md)
* [Automation](docs/Automation.md)
* [Troubleshooting](docs/Troubleshooting.md)
* [Health checks](docs/support/health-checks.md) and [support bundle](docs/support/support-bundle.md)
* [FAQ](docs/support/faq.md)
* [Figma exporter](docs/figma-exporter.md)

## Getting help

1. Check [Troubleshooting](docs/Troubleshooting.md) and the [FAQ](docs/support/faq.md).
2. In Unreal run **Tools > Handoff for UMG > Check Setup...** and fix anything marked Warning or Fail
   ([what each check means](docs/support/health-checks.md)).
3. Still stuck? Run **Create Support Bundle...** and [open an issue](../../issues/new/choose) with the zip attached.
   Full steps in [SUPPORT.md](SUPPORT.md).

For license and purchase questions use the publisher contact on the Fab product page; never post purchase details in an
issue.

## Support policy

* **Replies within 2 business days** on issues.
* **Engine support:** a build within 14 days of each Unreal Engine minor release. The latest 2 to 3 engine versions are
  supported.
* **UE 5.x is supported through the end of 2028.**
* Patches every 2 to 4 weeks for the first three months after release, then monthly. See the
  [changelog](CHANGELOG.md) and [roadmap](ROADMAP.md).

## Contributing

Issues only, plus documentation fixes by pull request. See [CONTRIBUTING.md](CONTRIBUTING.md) and the
[Code of Conduct](CODE_OF_CONDUCT.md). Documentation license: [LICENSE-docs.md](LICENSE-docs.md).

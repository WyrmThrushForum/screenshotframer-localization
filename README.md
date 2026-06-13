# ScreenshotFramer

ScreenshotFramer is a desktop tool for creating localized App Store screenshots from reusable image layers, device frames, backgrounds, and localized text resources.

[Download]()

## Overview

ScreenshotFramer helps automate the production of App Store screenshot images for multiple languages and screenshot numbers. It works by combining image layers, similar to a simple layered graphics workflow, and exporting the rendered result to disk.

A project can include:

- Background images
- Device frame images
- Localized screenshot folders
- `.strings` files for localized text
- Configuration files that define layer positions, sizes, and image paths

The tool is intended for teams that need to generate consistent App Store artwork across several locales without manually editing every exported screenshot.

## Platform note

The documented application targets macOS / Mac 10.13+ and is written in Swift. A Windows build or Windows-specific workflow is not described in the available project information.

## Main capabilities

- Compose screenshots from multiple image layers
- Use device frame images around screenshots
- Add localized text through `.strings` files
- Use variables in image paths
- Export combinations of supported images and languages
- Run exports from the desktop app or command line

## Localization workflow

Localized folders can be named by language or locale, such as:

- `en-US`
- `de-DE`

Each localized folder is expected to contain a `screenshots.strings` file. The string keys correspond to screenshot numbers used during rendering.

Example:

```strings
"1" = "It Starts With a Thought";
"2" = "Add Your Thoughts";
"3" = "Discover Connections";
"4" = "Visualize Your Idea";
"5" = "Productive on the Go";
```

The screenshot number can later be referenced through the `$image` variable.

## Project structure

A ScreenshotFramer project may include folders such as:

- `backgrounds` — optional background images
- `device_frames` — optional device frame artwork
- localized folders — screenshot images and text for each locale
- `Export` — generated output
- `.frame` configuration files — layout and export settings

This structure can be useful when combined with screenshot folders produced by tools such as fastlane snapshot.

## Variables

ScreenshotFramer supports variable-based paths so the same configuration can be reused across multiple images and languages.

Supported variables include:

| Variable | Purpose |
| --- | --- |
| `$image` | Screenshot number, typically numeric values such as `1` through `5` |
| `$language` | Locale folder name, excluding reserved folders such as `backgrounds`, `device_frames`, and `Export` |

For example, a layer path such as:

```text
$language/iPhone SE-$image.png
```

can resolve to:

```text
en-US/iPhone SE-1.png
```

or:

```text
de-DE/iPhone SE-1.png
```

depending on the selected language and screenshot number.

## Command-line usage

ScreenshotFramer includes command-line export support.

Export a single project file:

```bash
cd ~/Developer/MyProject/Screenshots
Screenshot-Framer-CLI -project "./iPhone SE.frame"
```

Export all configured devices in a directory:

```bash
cd ~/Developer/MyProject/Screenshots
Screenshot-Framer-CLI -project .
```

Run the CLI from inside a repository:

```bash
cd ~/Developer/MyProject/Screenshots
./Screenshot-Framer-CLI -project .
```

If using a downloaded binary, make sure the CLI file is executable before running it.

## Practical use cases

ScreenshotFramer is useful for:

- Preparing localized App Store screenshots
- Reusing a consistent layout across many languages
- Applying device frames to generated screenshots
- Exporting multiple screenshot variants from one configuration
- Maintaining screenshot assets in a repeatable folder structure

## Known limitations

The project documentation notes several limitations:

- Layers cannot be rearranged by drag and drop in the table view
- Exporting may use a large amount of memory
- There is no aspect ratio lock when scaling images
- Output is organized under `Export/$language/...` for clarity

## License

ScreenshotFramer is distributed under the MIT license.

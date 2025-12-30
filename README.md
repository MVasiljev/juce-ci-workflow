# JUCE CI Workflow

Reusable GitHub Actions workflow for building JUCE audio plugins on all platforms.

## Supported Platforms

| Platform | Formats | Runner |
|----------|---------|--------|
| macOS | AU + VST3 | `macos-latest` |
| Windows | VST3 | `windows-latest` |
| Linux | VST3 | `ubuntu-latest` |

## Usage

In your plugin repository, create `.github/workflows/build.yml`:

```yaml
name: Build Plugin

on:
  push:
    branches: [main]
    tags: ['v*']
  pull_request:
    branches: [main]

jobs:
  build:
    uses: MVasiljev/juce-ci-workflow/.github/workflows/build-juce-plugin.yml@main
    with:
      plugin_name: "My Plugin Name"
      version: "1.0.0"
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `plugin_name` | Yes | - | Name of the plugin |
| `version` | Yes | - | Version string |
| `juce_version` | No | `8.0.4` | JUCE version to use |
| `build_au` | No | `true` | Build Audio Unit (macOS) |
| `build_vst3` | No | `true` | Build VST3 |

## Artifacts

After build completes, you'll get:
- `{plugin_name}-v{version}-macOS` - AU + VST3 for macOS
- `{plugin_name}-v{version}-Windows` - VST3 for Windows
- `{plugin_name}-v{version}-Linux` - VST3 for Linux
- `{plugin_name}-v{version}-ALL-PLATFORMS` - Combined ZIP with everything

## Requirements

Your plugin repository must have:
1. `CMakeLists.txt` in root
2. JUCE as submodule at `../JUCE` (relative) or workflow will clone it

## License

MIT License - Use freely for your JUCE projects.

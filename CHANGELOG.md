# Changelog

## 0.2.0

- Adds relay patch support for Unity AI Assistant `2.17.0-pre.1`.
- Handles the 2.17.0 relay's use of actual newline bytes (0x0A) inside the Codex provider template literal, which differs from the escaped `\n` (0x5C 0x6E) used in 2.7.x relays.
- Retains backward-compatible support for `2.7.0-pre.1` and `2.7.0-pre.3`.

## 0.1.1

- Adds relay patch support for Unity AI Assistant `2.7.0-pre.3`.
- Keeps binary patching signature-gated for unsupported relay builds.

## 0.1.0

- Initial Windows-only release.
- Adds one-click setup for using Codex ChatGPT OAuth in Unity AI Assistant.
- Safely patches the local Unity AI Assistant relay binary after creating a backup.
- Adds diagnostics and restore commands.
- Documents Unity MCP server conflicts and reports possible global Codex `unityMCP` conflicts in diagnostics.

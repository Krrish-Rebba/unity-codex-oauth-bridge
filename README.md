# Unity AI Codex OAuth Bridge

Use Codex / ChatGPT OAuth inside Unity AI Assistant without manually entering an `OPENAI_API_KEY`.

This package patches the local Unity AI Assistant relay metadata so Unity's Codex provider can start the bundled Codex ACP bridge while Codex itself uses the existing Codex CLI ChatGPT login state.

## Status

- Version: `0.2.0`
- Platform: Windows only
- Tested targets: Unity AI Assistant `2.7.0-pre.1`, `2.7.0-pre.3`, and `2.17.0-pre.1` on Unity 6.4
- Repository: [https://github.com/Krrish-Rebba/unity-codex-oauth-bridge](https://github.com/Krrish-Rebba/unity-codex-oauth-bridge)
- License: MIT

This is an unofficial bridge. It is not affiliated with Unity or OpenAI.

## Prerequisites

Before setting up the bridge, ensure you have:
1. **Unity Editor**: Unity 6+ (tested on Unity 6.4) on Windows.
2. **Unity AI Assistant**: Package `com.unity.ai.assistant` installed (`2.7.0-pre.1`, `2.7.0-pre.3`, or `2.17.0-pre.1`).
3. **OpenAI Codex CLI**: Installed on your system and logged in with your ChatGPT account (`codex login`).

## Installation

### Method 1: Unity Package Manager via Git URL (Recommended)
1. In the Unity Editor, open **Window > Package Manager**.
2. Click the **+** button in the top-left and select **Add package from git URL...**.
3. Enter:
   ```text
   https://github.com/Krrish-Rebba/unity-codex-oauth-bridge.git
   ```
4. Click **Add**.

### Method 2: From Local Disk
If you have cloned or downloaded the repository locally:
1. Open **Window > Package Manager**.
2. Click **+** > **Add package from disk...**.
3. Select the `package.json` file inside the repository directory.

## Setup & Usage

1. **Run Setup**:
   In Unity's top menu bar, click:
   ```text
   Tools > Unity AI Codex OAuth > Setup Codex OAuth
   ```
   * What this does:
     * Validates your installed Unity AI Assistant version.
     * Backs up `RelayApp~/relay_win.exe` to `relay_win.exe.codex-oauth-backup`.
     * Patches the local relay binary to remove the `OPENAI_API_KEY` requirement for Codex.
     * Verifies your Codex CLI login status (opens `codex login` if not already signed in).
     * Configures Unity AI Gateway preferences and activates the Codex provider.

2. **Select Provider in Unity**:
   * Open the Unity AI Assistant window (**Window > AI > Assistant**).
   * Choose **Codex** as the active provider.

3. **Approve MCP Connection**:
   * When Unity displays the `New MCP Connection` prompt for `codex-mcp-client` from the package cache, click **Approve** if you trust the project and want Codex to access scene and asset tools.

## Management & Diagnostics

Useful menu commands under `Tools > Unity AI Codex OAuth`:
- **Diagnostics**: Checks relay patch state, backup existence, Codex CLI path, login status, and MCP configuration.
- **Restore Original Unity Relay**: Reverts `relay_win.exe` from the backup and cleans up bridge cache keys.
- **Advanced > Restart Unity AI Relay**: Restarts the background relay process without re-patching.

## Restoring Original Relay

To revert the patch at any time:
```text
Tools > Unity AI Codex OAuth > Restore Original Unity Relay
```
This restores the backed-up relay executable without deleting your Codex CLI login state.

## Important Notes & Troubleshooting

- **Assistant Updates**: When Unity AI Assistant is updated or reinstalled via Package Manager, Unity replaces the relay binary. If the `OPENAI_API_KEY` prompt reappears, simply run `Setup Codex OAuth` again.
- **Safe Signatures**: The bridge strictly validates the binary against known signatures (`2.7.0-pre.1`, `2.7.0-pre.3`, `2.17.0-pre.1`). Unsupported versions will be safely refused without making modifications.
- **MCP Conflict Handling**: If Codex answers questions but reports `No Unity Editor instances found` or `instance_count: 0`, prompt Codex:
  ```text
  Do not use the global unityMCP server. Use the Unity AI Assistant provided MCP server named unity-mcp-gateway. List the current Unity scene hierarchy.
  ```
- For more troubleshooting steps, see [Troubleshooting Guide](Documentation~/troubleshooting.md).
- See release history in [CHANGELOG.md](CHANGELOG.md).

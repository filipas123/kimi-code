# Changelog

## 0.6.0

### Changed

- Replaced the legacy Python/stdio runtime with the in-process Kimi Code Node
  SDK. The extension no longer downloads or starts a separate Kimi executable.
- Raised the minimum supported editor version to VS Code 1.100.0.
- Added an opt-in legacy migration prompt on the first launch that detects data
  from version 0.5.x. The migration copies or merges supported data into the
  current Kimi Code home and does not delete the legacy source. If migration is
  skipped or needs to be retried, run **Kimi Code: Migrate Legacy Data** from the
  Command Palette.
- Legacy Kimi Code OAuth credentials and MCP OAuth credentials are deliberately
  not copied. Sign in to Kimi Code again and re-authorize affected MCP servers
  after migration.
- Removed the `kimi.executablePath` and `kimi.environmentVariables` settings.
  The old `kimi.environmentVariables.KIMI_SHARE_DIR` value is consulted only to
  discover legacy data during migration; it is not applied to the new runtime.
  The system-level `KIMI_CODE_HOME` environment variable remains supported.
- When VS Code and the Kimi Code terminal app resolve to the same
  `KIMI_CODE_HOME`, they use the same configuration and session storage. Running
  the same session concurrently from multiple processes is not supported or
  protected by cross-process locking.
- The model picker groups models by provider when multiple providers are
  configured, keeps provider identity when display names match, and recognizes
  adaptive-thinking metadata. A configured custom default provider no longer
  requires dismissing the Kimi account login screen on every launch.
- The file changes panel and Undo actions use extension-maintained baselines.
  Files changed through Kimi's Write and Edit operations are tracked on a
  best-effort basis. File deletions performed inside Bash are not tracked by
  this baseline and therefore cannot be restored by the panel's Undo action.

### Distribution boundary

Release packaging produces target-specific VSIX files for `darwin-x64`,
`darwin-arm64`, `linux-x64`, `linux-arm64`, `win32-x64`, and `win32-arm64`.
Archive and static verification for a target does not by itself prove that the
extension has run successfully in that target's Extension Host; runtime test
results must be recorded separately for each operating system and architecture.

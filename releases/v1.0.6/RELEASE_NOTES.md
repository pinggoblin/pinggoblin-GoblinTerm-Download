# GoblinTerm Release Notes (Next)

Status: Draft (pre-release)
Target version: TBD
Release date: TBD

## Summary

This release focuses on native terminal stability and correctness improvements versus the first release, with emphasis on multiline paste behavior in Linux full-screen editors.

## Highlights

- Multiline paste in Linux editor sessions (for example nano) is now routed through a safe typed-input mode to prevent line collapse/overwrite.
- Paste routing logic was hardened so editor/alt-screen multiline content does not incorrectly fall back to bracketed/shell paths.
- Paste diagnostics were made opt-in for cleaner normal operation.
- Native SSH authentication status indicator was restored to checkmark formatting.

## Added

- New Settings toggle:
  - Safe editor multiline paste mode (Linux CLI alt-screen)
- Additional paste-route state reporting (debug-only) for targeted troubleshooting.

## Changed

- Editor multiline paste behavior now favors input-path simulation in editor/alt-screen contexts.
- Paste routing precedence was updated to prioritize editor-safe handling before generic bracketed routing.
- Debug tracing for paste payloads now prints only when `GOBLINTERM_DEBUG_PASTE=1` is set.

## Fixed

- Fixed nano multiline paste cases where lines were collapsed/overwritten instead of inserted as separate lines.
- Fixed inconsistent editor paste outcomes caused by mode/routing edge cases across bracketed and alt-screen states.
- Restored native SSH authentication success prefix from `?` back to checkmark output.

## Known Issues

- Terminal behavior can still vary by remote host shell/editor stack and TERM negotiation.
- Keep `Safe editor multiline paste mode` enabled for Linux CLI editor-heavy workflows.

## Upgrade Notes

- No migration is expected for existing session data.
- Existing profile data paths remain unchanged:
  - Packaged: %APPDATA%\GoblinTerm-User\db.json
  - Source/dev: %APPDATA%\GoblinTerm-Dev\db.json

## Verification Checklist (Release Candidate)

- SSH/Telnet/Serial connection launch and reconnect behavior
- Multi-tab macro execution from toolbar/context menu
- Copy/paste behavior at shell prompt and inside Linux editor sessions (nano multiline regression check)
- Right-click immediate paste toggle behavior
- Help -> Keyboard Shortcuts dialog content and accessibility
- Import/export and backup/restore operations
- Packaging script output and SHA256 generation

## Build Artifacts

Use the release script:

powershell
./build-release.ps1 -Version <version>

Expected output:

- release/GoblinTerm-v<version>-win64/
- release/GoblinTerm-v<version>-win64.zip
- release/GoblinTerm-v<version>-win64-SHA256.txt

## Notes for Final Cut

Before publishing, update this file:

- Replace target version and date.
- Move confirmed fixes from "Known Issues" to "Fixed".
- Remove any troubleshooting-only notes that should not appear in public release notes.

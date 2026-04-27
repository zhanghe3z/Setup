# Setup

Misc machine bootstrap notes.

## Claude Code — skip permission prompts via `settings.json`

Add `dangerouslySkipPermissions: true` to your Claude Code settings file so
every session launches without per-tool permission prompts.

**Only do this inside a sandbox / VM / disposable container** — Claude can run
arbitrary shell commands without asking.

### User-level (applies to every project)

`~/.claude/settings.json`:

```json
{
  "dangerouslySkipPermissions": true
}
```

### Project-level (just this repo)

`.claude/settings.json` at the repo root:

```json
{
  "dangerouslySkipPermissions": true
}
```

### Notes

- If the file already exists, merge the key in — do **not** overwrite the
  whole file.
- Project settings override user settings, so a per-project `false` will
  re-enable prompts in that one repo.
- When running as root, also set `IS_SANDBOX=1` in the environment, otherwise
  Claude Code refuses to honor the flag.

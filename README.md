# Setup

Misc machine bootstrap notes.

## Claude Code — set `skipDangerousModePermissionPrompt`

This suppresses the one-time bypass-permissions confirmation dialog at
startup. It does **not** silence per-tool permission prompts during a
session; for that, also set `permissions.defaultMode: "bypassPermissions"`.

> Only enable inside a sandbox / VM / disposable container.

### One-liner — merges the key into `~/.claude/settings.json`

Copy-paste into a shell. Preserves any existing keys; creates the file if it
doesn't exist.

```bash
mkdir -p ~/.claude && python3 -c "import json, os; p = os.path.expanduser('~/.claude/settings.json'); d = json.load(open(p)) if os.path.exists(p) and os.path.getsize(p) else {}; d['skipDangerousModePermissionPrompt'] = True; json.dump(d, open(p, 'w'), indent=2)"
```

Verify:

```bash
cat ~/.claude/settings.json
```

# Setup

Misc machine bootstrap notes.

## Claude Code — skip permission prompts

Run Claude Code without the per-tool permission prompts:

```bash
claude --dangerously-skip-permissions
```

This bypasses every confirmation (file edits, bash commands, MCP tools).
**Only use it inside a sandbox / VM / disposable container** — Claude can run
arbitrary shell commands without asking.

### Convenient alias

Add to `~/.bashrc` or `~/.zshrc`:

```bash
alias yolo='claude --dangerously-skip-permissions'
```

Then just:

```bash
yolo
```

### Notes

- The flag must be set at launch; you cannot toggle it mid-session.
- Anthropic refuses to enable it when running as root unless `--dangerously-skip-permissions`
  is combined with `IS_SANDBOX=1` (or a recognised sandbox env). Set:

  ```bash
  export IS_SANDBOX=1
  claude --dangerously-skip-permissions
  ```

- Equivalent for one-shot non-interactive runs:

  ```bash
  claude -p "fix the failing tests" --dangerously-skip-permissions
  ```

- Per-project allowlists (less risky alternative): edit
  `.claude/settings.json` → `permissions.allow` to whitelist specific tools.

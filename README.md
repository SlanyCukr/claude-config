# claude-config

Backup of my custom Claude Code configuration. These are **copies** — the live files are in `~/.claude/`. After editing the live files, re-copy and push.

## Files

| File here | Live path | Wired via |
|---|---|---|
| `system-prompt-append.txt` | `~/.claude/system-prompt-append.txt` | `claude` alias in `~/.zshrc` adds `--append-system-prompt-file ~/.claude/system-prompt-append.txt` |
| `output-styles/i-have-adhd.md` | `~/.claude/output-styles/i-have-adhd.md` | `"outputStyle": "ADHD"` in `~/.claude/settings.json` (style name comes from the file's `name:` frontmatter, not the filename) |

## Notes

- The append file is a *delta* on top of Claude Code's default system prompt — do not duplicate what upstream already ships.
- Global `~/.claude/CLAUDE.md` is deliberately a zero-byte file; all global guidance lives in the append file.
- Tools that read `~/.claude/settings.json` (e.g. t3code's embedded Claude Agent SDK) pick up the output style automatically, but NOT the append file — that only rides on the shell alias unless passed explicitly.

## Sync

```bash
cp ~/.claude/system-prompt-append.txt ~/Documents/personal/projects/claude-config/
cp ~/.claude/output-styles/i-have-adhd.md ~/Documents/personal/projects/claude-config/output-styles/
cd ~/Documents/personal/projects/claude-config && git add -A && git commit -m "sync" && git push
```

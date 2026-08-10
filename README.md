# claude-config

My Claude Code config, packaged as a **Claude Code plugin**. The plugin ships the ADHD output style; the system prompt append file rides along as a versioned copy.

## Install

Symlink the repo into the skills dir — it auto-loads every session as `claude-config@skills-dir`:

```bash
ln -s ~/Documents/personal/projects/claude-config ~/.claude/skills/claude-config
```

Then select the style (note the plugin namespace):

```json
// ~/.claude/settings.json
{ "outputStyle": "claude-config:ADHD" }
```

Renaming the plugin (`.claude-plugin/plugin.json` → `name`) changes the style id and breaks that setting.

## Contents

| File | Role |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `output-styles/i-have-adhd.md` | ADHD output style (`name: ADHD` → loads as `claude-config:ADHD`). **Live-loaded via the symlink** — edits here apply next session, no copying. |
| `system-prompt-append.txt` | **Copy** of `~/.claude/system-prompt-append.txt`. Plugins have no mechanism that reaches the system prompt, so this stays wired via the `claude` alias in `~/.zshrc`: `--append-system-prompt-file ~/.claude/system-prompt-append.txt`. Re-copy and push after editing the live file. |

## Notes

- The append file is a *delta* on top of Claude Code's default system prompt — do not duplicate what upstream already ships.
- Global `~/.claude/CLAUDE.md` is deliberately a zero-byte file; all global guidance lives in the append file.
- Tools embedding the Claude Agent SDK with user setting sources (e.g. t3code) load the plugin and the style automatically, but NOT the append file — that must be passed explicitly (t3code: Providers → Claude → Launch arguments).

## Sync (append file only)

```bash
cp ~/.claude/system-prompt-append.txt ~/Documents/personal/projects/claude-config/
cd ~/Documents/personal/projects/claude-config && git add -A && git commit -m "sync append" && git push
```

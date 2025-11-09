# Global AGENTS.md Configuration Proposal

**Standardize `~/.config/agents/AGENTS.md` as a cross-tool, user-level configuration.**

## Problem

Each AI coding tool uses a different global config path:
- **Claude Code:** `~/.claude/CLAUDE.md`
- **Codex:** `~/.codex/AGENTS.md`
- **droid:** `~/.factory/AGENTS.md`
- **Amp:** `~/.config/AGENTS.md`

**Result:** Users must either duplicate personal preferences across tool-specific paths OR copy the same config into every project's `./AGENTS.md`.

## Solution

**One standard location:** `~/.config/agents/AGENTS.md`

**Platforms:**
- Linux/macOS: `~/.config/agents/AGENTS.md` (`$XDG_CONFIG_HOME/agents/AGENTS.md`)
- Windows: `%APPDATA%\agents\AGENTS.md`

**Why a directory (`agents/`) not a lone file:**
- Follows XDG standard: `~/.config/<name>/` (not `~/.config/file`)
- Extensible: add `rules/`, `commands/`, templates later
- Prevents `~/.config/` clutter from tool-specific files

## How It Works

Tools check `~/.config/agents/AGENTS.md` for global user configuration. Project-level config takes precedence over global.

Implementation details—precedence order, parent directory walking, merging behavior—are up to individual tools.

## Adoption

**Tool developers:** Check `$XDG_CONFIG_HOME/agents/AGENTS.md` (fallback: `~/.config/agents/AGENTS.md`) on Unix and `%APPDATA%\agents\AGENTS.md` on Windows. Merge with project configs (project takes precedence).

**Users:** Create `~/.config/agents/AGENTS.md` with personal preferences. Applies across all compatible tools.

## Precedent

**Amp** already uses `~/.config/AGENTS.md` (lone file). This proposal uses the directory pattern (`~/.config/agents/`) for better extensibility.

**Similar patterns:** Git uses `~/.gitconfig` (global) + `.git/config` (project), npm uses `~/.npmrc` + `.npmrc`.

## Related

[openai/agents.md Issue #91](https://github.com/openai/agents.md/issues/91)

## License

CC0 1.0 Universal

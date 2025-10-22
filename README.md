# Global AGENTS.md Configuration Proposal

**Standardize `~/.config/agents/AGENTS.md` as a cross-tool, user-level configuration.**

## Problem

Users must duplicate personal preferences across every project or fragment config across tool-specific paths (`~/.claude/`, `~/.codex/`, `~/.gemini/`).

## Proposal

**`~/.config/agents/AGENTS.md`** as the global configuration location.

**Paths:**
- Linux/macOS: `~/.config/agents/AGENTS.md` (or `$XDG_CONFIG_HOME/agents/AGENTS.md`)
- Windows: `%APPDATA%\agents\AGENTS.md`

**Why `~/.config/agents/`:**
- Follows XDG Base Directory standard
- Matches pattern: `~/.config/<name>/` (not lone files)
- Allows expansion: `rules/`, `commands/`
- Prevents fragmentation

**Configuration precedence:**
1. `./.agents.local.md` (per-developer, not committed)
2. `./AGENTS.md` or `./.agents/AGENTS.md` (project-level)
3. Parent directories: `../AGENTS.md` (up to `$HOME`)
4. **`~/.config/agents/AGENTS.md`** ← global
5. Tool defaults

## Precedent

**Amp already implements this:**
- Checks `$HOME/.config/AGENTS.md`
- Auto-includes parent directory AGENTS.md files

**Similar patterns:**
- Git: `~/.gitconfig` + `.git/config`
- Claude Code: `~/.claude/CLAUDE.md` + `./CLAUDE.md`
- Codex: `~/.codex/instructions.md` + `./AGENTS.md`

## Project-Level Organization

This proposal focuses on **global** config. For project-level organization:

**Current standard:** `./AGENTS.md` (root file)

**Alternative:** `./.agents/AGENTS.md` (directory structure)
- Allows expansion: `.agents/rules/`, `.agents/commands/`
- Reduces root directory clutter
- Already proposed in [openai/agents.md#9](https://github.com/openai/agents.md/issues/9)

Both patterns work with this global config proposal.

## Implementation

**For tool developers:**
1. Check `$XDG_CONFIG_HOME/agents/AGENTS.md` (fallback: `~/.config/agents/AGENTS.md`)
2. Check `%APPDATA%\agents\AGENTS.md` on Windows
3. Merge with project configs (project takes precedence)

**For users:**
Create `~/.config/agents/AGENTS.md` with personal preferences. Applies across all projects unless overridden.

## Related Discussion

This proposal is discussed in:
- [openai/agents.md Issue #TBD](https://github.com/openai/agents.md/issues) (pending submission)

## License

CC0 1.0 Universal - Public Domain

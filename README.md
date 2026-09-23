# Claude Code Custom Skills

Personal collection of custom Claude Code skills.

Works alongside Matt Pocock's skill collection - this repo contains only custom-built skills.

## How Claude Code finds skills

This matters, because getting it wrong means the skill silently never appears.

Claude Code looks in `~/.claude/skills/` for **folders**, not loose files. Each skill
must be its own folder containing a file called exactly `SKILL.md`:

```
~/.claude/skills/
  auto-implement/
    SKILL.md
```

A bare `auto-implement.md` sitting in `~/.claude/skills/` is ignored.

The `SKILL.md` frontmatter must include a `name:` field, and the name must match the
folder. Without `name:`, the skill does not load.

This repo is laid out to mirror `~/.claude/skills/` exactly, so installing is a
straight copy of the folders.

## Skills

### `/auto-implement`
Multi-agent orchestrator for systematic GitHub issue implementation.

**Features**:
- One clean context per ticket (sub-agents)
- One branch and one pull request per ticket - nothing is committed to `main`
- Sub-agents run shell commands and edit files autonomously; they do not merge
- Token budget: <150k per ticket
- Auto-detects GitHub repository
- Uses `/implement` skill for TDD workflow
- Comments the PR link on the issue; the issue closes when you merge
- Handles blockers gracefully

**Usage**:
```
/auto-implement
```

**Prerequisites**:
- GitHub CLI (`gh`) installed and authenticated
- Git repository with GitHub remote
- Open issues in GitHub repository

**What it will not do**: merge a PR, force-push, rewrite published history, add
dependencies, or change CI config without asking you first.

## Installation

Same on every machine. Clone this repo once, then copy the skill folders across.

### PowerShell (Windows)

```powershell
cd ~\.claude
git clone https://github.com/lysanderbryant-del/claude-skills-custom.git skills-custom
Get-ChildItem .\skills-custom -Directory -Force | Where-Object { $_.Name -ne '.git' } | ForEach-Object { Copy-Item $_.FullName .\skills\ -Recurse -Force }
```

### Bash (macOS / Linux)

```bash
cd ~/.claude
git clone https://github.com/lysanderbryant-del/claude-skills-custom.git skills-custom
for d in skills-custom/*/; do cp -r "$d" skills/; done
```

### Check it worked

Start Claude Code and type `/auto` at the prompt. `auto-implement` should appear in
the autocomplete list. If it does not:

1. Confirm the file is at `~/.claude/skills/auto-implement/SKILL.md` - not
   `~/.claude/skills/auto-implement.md`
2. Confirm the first lines of that file include `name: auto-implement`
3. Restart Claude Code

## Updating skills

After editing a skill in `~/.claude/skills/`, sync it back here:

### PowerShell

```powershell
Copy-Item ~\.claude\skills\auto-implement\SKILL.md ~\.claude\skills-custom\auto-implement\SKILL.md -Force
cd ~\.claude\skills-custom
git add .
git commit -m "Update auto-implement skill"
git push
```

### Bash

```bash
cp ~/.claude/skills/auto-implement/SKILL.md ~/.claude/skills-custom/auto-implement/SKILL.md
cd ~/.claude/skills-custom
git add .
git commit -m "Update auto-implement skill"
git push
```

## Adding a new skill

1. Create `~/.claude/skills/<skill-name>/SKILL.md`
2. Give it frontmatter with at least `name:` and `description:`
3. Copy the folder into this repo, commit, push

## Contributing

These are personal skills, but feel free to fork and adapt for your own use!

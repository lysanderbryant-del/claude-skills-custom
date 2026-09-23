# Claude Code Custom Skills

Personal collection of custom Claude Code skills.

Works alongside Matt Pocock's skill collection - this repo contains only custom-built skills.

## Skills

### `/auto-implement`
Multi-agent orchestrator for systematic GitHub issue implementation.

**Features**:
- One clean context per ticket (sub-agents)
- Token budget: <150k per ticket
- Auto-detects GitHub repository
- Uses `/implement` skill for TDD workflow
- Automatic ticket management (update/close)
- Commits to main branch
- Handles blockers gracefully

**Usage**: 
```
/auto-implement
```

**Prerequisites**:
- GitHub CLI (`gh`) installed and authenticated
- Git repository with GitHub remote
- Open issues in GitHub repository

## Installation

### Initial Setup (First Machine)

1. Clone this repository:
```bash
cd ~/.claude
git clone https://github.com/lysanderbryant-del/claude-skills-custom.git skills-custom
```

2. Copy skills to main skills directory:
```bash
cp ~/.claude/skills-custom/*.md ~/.claude/skills/
```

### Syncing to Other Machines

1. Clone the repository:
```bash
cd ~/.claude
git clone https://github.com/lysanderbryant-del/claude-skills-custom.git skills-custom
```

2. Copy skills to main skills directory:
```bash
cp ~/.claude/skills-custom/*.md ~/.claude/skills/
```

### Updating Skills

After editing skills in `~/.claude/skills/`, sync back to repository:

```bash
# Copy updated skills back to custom repo
cp ~/.claude/skills/auto-implement.md ~/.claude/skills-custom/

# Commit and push
cd ~/.claude/skills-custom
git add .
git commit -m "Update skills"
git push
```

## Contributing

These are personal skills, but feel free to fork and adapt for your own use!

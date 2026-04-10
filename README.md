# claude-skills

Personal Claude Code skills collection.

## Skills

| Skill | Description |
|---|---|
| [`github-docs`](github-docs/) | Generate a GitHub dark-themed single-page HTML doc site for any project |

---

## Installation

Skills in this repo are loaded by pointing Claude Code's skills path at this directory.

### Option A — Symlink into `~/.claude/skills/` (recommended)

```bash
# Create the skills dir if it doesn't exist
mkdir -p ~/.claude/skills

# Symlink each skill you want active
ln -s ~/stash/github/claude-skills/github-docs ~/.claude/skills/github-docs
```

After linking, Claude Code will discover the skill automatically in every session.

### Option B — Add a skills path in `settings.json`

Open `~/.claude/settings.json` and add (or extend) the `skillsDirectories` key:

```json
{
  "skillsDirectories": [
    "~/stash/github/claude-skills"
  ]
}
```

Restart Claude Code for the change to take effect.

### Option C — Reference from a project's `CLAUDE.md`

If you only want a skill active in one project, add to `.claude/CLAUDE.md` (or the project's `CLAUDE.md`):

```markdown
@~/stash/github/claude-skills/github-docs/SKILL.md
```

---

## Usage

Once installed, invoke the `github-docs` skill in any Claude Code session:

```
/github-docs
```

Or just describe what you want — Claude will pick up the skill automatically when you ask to "generate docs" or "create documentation" for the project.

### What it generates

- `docs/index.html` — a single self-contained file, no build tools required
- GitHub dark theme (matches `github.com` dark mode aesthetics)
- Sidebar navigation with active-link highlighting
- Hero section with language/tech badges
- Feature cards, pipeline flow diagrams, collapsible API endpoint blocks
- Project structure tree view, configuration table, callout boxes
- Fully responsive with mobile sidebar toggle

---

## Adding New Skills

1. Create a directory: `~/stash/github/claude-skills/<skill-name>/`
2. Add `SKILL.md` with YAML frontmatter (`name`, `description`) — see [agentskills.io/specification](https://agentskills.io/specification)
3. Add any supporting files (templates, scripts, reference docs)
4. Symlink or reference as shown above

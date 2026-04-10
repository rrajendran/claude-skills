# claude-skills

Personal Claude Code skills collection.

## Skills

| Skill | Description |
|---|---|
| [`github-docs`](github-docs/) | Generate a GitHub dark-themed single-page HTML doc site for any project |

---

## Installation

```bash
npx ai-agent-skills rrajendran/claude-skills
```

This installs all skills globally to `~/.claude/skills/`, making them available in every session.

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

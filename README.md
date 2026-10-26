# Skills

Jack's agent skills.

## Installation

### Claude Code

```bash
claude plugin marketplace add sentienthouseplant/skills
claude plugin install jack-skills@sentienthouseplant
```

### Codex

```bash
codex plugin marketplace add sentienthouseplant/skills
codex plugin add jack-skills@sentienthouseplant
```

### Any other agent, or editable files

```bash
npx skills@latest add sentienthouseplant/skills
```

The plugin is a managed bundle and skills.sh copies files you own, so pick one route per agent. Installing both gives you every skill twice.

## Reference

These split on one axis: who can invoke them. **User-invoked** skills are reachable only when you type them (e.g. `/some-skill`); their job is to orchestrate. **Model-invoked** skills can be invoked by you _or_ reached for automatically by the agent when the task fits; they hold the reusable discipline. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one. See [.agents/invocation.md](./.agents/invocation.md).

### Engineering

Skills I use daily for code work.

**User-invoked**

_None yet._

**Model-invoked**

_None yet._

### Productivity

General workflow tools, not code-specific.

**User-invoked**

_None yet._

**Model-invoked**

- **[nice-diagram](./skills/productivity/nice-diagram/SKILL.md)**: Always used when creating a diagram. Draws it in D2 with a monochrome house style, rendered to whatever format the destination needs (PNG, SVG, PDF, PPTX, GIF, ASCII text).

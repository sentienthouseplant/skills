# Model-invoked vs user-invoked

Every `SKILL.md` in this repo is a skill. The one axis that splits them is **invocation**, who can reach it:

- **User-invoked**: reachable **only by the human typing its name**. Set `disable-model-invocation: true` in the frontmatter (Claude Code) and `policy.allow_implicit_invocation: false` in `agents/openai.yaml` (Codex). The `description` is **human-facing**: a one-line summary read by a person browsing slash-commands. Strip trigger lists ("Use when the user says…").
- **Model-invoked**: reachable by **model or user**. The default: omit `disable-model-invocation` and the `policy` block from `agents/openai.yaml`. The `description` is **model-facing** and keeps rich trigger phrasing ("Use when the user wants…, mentions…, asks for…") so auto-invocation fires. The test for whether a skill should stay model-invoked: _could the model usefully reach for this autonomously?_ (Reuse is the reason to extract a skill, not the test.)

A user-invoked skill may invoke model-invoked skills, but it can never reach another user-invoked skill.

Every skill carries an `agents/openai.yaml` beside its `SKILL.md`. It holds Codex UI metadata: `interface.display_name` and `interface.short_description` for the skill picker, and, for user-invoked skills, the `policy.allow_implicit_invocation: false` that pairs with `disable-model-invocation`. Keep the two in sync: a skill is user-invoked in both harnesses or neither.

## Templates

User-invoked `SKILL.md`:

```markdown
---
name: <skill-name>
description: <One line for a human browsing slash-commands.>
disable-model-invocation: true
---
```

User-invoked `agents/openai.yaml`:

```yaml
interface:
  display_name: "<Skill Name>"
  short_description: "<A few words>"
policy:
  allow_implicit_invocation: false
```

Model-invoked `SKILL.md`:

```markdown
---
name: <skill-name>
description: <What it does>. Use when the user wants…, mentions…, asks for….
---
```

Model-invoked `agents/openai.yaml`:

```yaml
interface:
  display_name: "<Skill Name>"
  short_description: "<A few words>"
```

## Dependencies between them

Dependencies are expressed as an explicit instruction to **call the Skill tool** with the named skill (`Call the Skill tool with "<skill-name>"`), not deep `../other-skill/FILE.md` cross-references, and not a bare `/skill`-style mention left for the model to interpret. Naming the tool is what gets it fired. Shared reference docs live inside the skill that owns them; other skills reach that material by calling the Skill tool with it, not by linking across folders.

This is about **operative** instructions: a skill's own steps telling the agent to go run another skill right now. Prose that just names skills for a human to pick from (bucket `README.md`s) isn't invoking anything, so it keeps `/skill`-style names as plain labels.

The Skill tool takes one skill per call. A step that needs two skills is two calls: say so (`Call the Skill tool twice, for "a" and "b"`).

This convention only holds when the named skill is **model-invoked**. When a step's precondition is a user-invoked skill, phrase it as an instruction for the human to act on: "tell the user to run `/<skill-name>`", never as a Skill tool call.

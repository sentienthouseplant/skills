Skills are organized into bucket folders under `skills/`:

- `engineering/`: daily code work
- `productivity/`: daily non-code workflow tools
- `in-progress/`: beta: being tried out, not shipped in the plugin

Every skill lives at `skills/<bucket>/<skill-name>/SKILL.md`, with an `agents/openai.yaml` beside it.

Every skill in `engineering/` or `productivity/` (the **promoted** buckets) must have a reference in the top-level `README.md` and an entry in `.claude-plugin/plugin.json`'s `skills` array (the plugin ships exactly the promoted set). Skills in `in-progress/` must not appear in either.

`.claude-plugin/marketplace.json` makes this repo its own single-plugin marketplace. Run `claude plugin validate .` after touching either manifest. It must pass; the only expected warnings are the root `CLAUDE.md` (it's for working on this repo, not shipped context) and the missing icon. Installed copies only update when `version` in `.claude-plugin/plugin.json` changes, so bump it whenever a change to a promoted skill should reach them.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`.

Each bucket folder has a `README.md` that lists every skill in the bucket with a one-line description, with the skill name linked to its `SKILL.md`. The promoted buckets' `README.md`s and the top-level `README.md` group entries into **User-invoked** and **Model-invoked**; the `in-progress/` `README.md` uses a flat list.

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true` plus `policy.allow_implicit_invocation: false` in `agents/openai.yaml`, reachable only by the human) or model-invoked (model- or user-reachable). See [.agents/invocation.md](./.agents/invocation.md).

To (re)link every skill into the local harness skill directories (`~/.claude/skills`, `~/.agents/skills`), run `scripts/link-skills.sh`. Each entry is a symlink into this repo, so a `git pull` keeps installed skills current; re-run the script after adding, removing, or renaming a skill.

No em-dashes anywhere in this repo's prose (`SKILL.md` files, `README.md`s, docs, code comments). Where a sentence reaches for one, rewrite it instead with a comma, colon, period, parentheses, or a conjunction, whichever the sentence actually wants; never do a blind character substitution.

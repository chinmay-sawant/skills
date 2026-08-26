# developer-skills

Personal collection of agent skills I use every day to get consistent results from any coding agent (opencode, codex, gemini, claude, cursor, etc.). Each skill lives under `skills/<name>/` and is picked up automatically when the agent reads `AGENTS.md`.

This is not a product repo - it is my daily toolkit for backend and general development. Install with `npx skills add chinmay-sawant/developer-skills` or a single skill with `npx skills add chinmay-sawant/developer-skills --skill <name>`.

[![skills.sh](https://skills.sh/b/chinmay-sawant/developer-skills)](https://skills.sh/chinmay-sawant/developer-skills)

## Skills

| Skill | What it does | Where |
|-------|--------------|-------|
| **PR** | Templates and checklists for PRs, issues, and progress comments so every PR has the same shape | [`skills/PR/`](skills/PR/) |
| **Feynman** | Plain-words explainer loop - forces the agent to explain anything simply until I can retell it | [`skills/feynman/`](skills/feynman/) |
| **Unslop** | Cut AI tells from writing and add human voice - puffery, em dashes, chatbot filler (original by [cursor/plugins](https://github.com/cursor/plugins/blob/main/pstack/skills/unslop/SKILL.md), copied to `skills/unslop/` for local use) | [`skills/unslop/`](skills/unslop/) |

## Install

**Website:** [skills.sh/chinmay-sawant/developer-skills](https://skills.sh/chinmay-sawant/developer-skills)

**Badge** (add to any README):
```md
[![skills.sh](https://skills.sh/b/chinmay-sawant/developer-skills)](https://skills.sh/chinmay-sawant/developer-skills)
```

**CLI** - pick one skill or all:

```sh
# list available skills in this repo
npx skills add chinmay-sawant/developer-skills --list

# install one skill
npx skills add chinmay-sawant/developer-skills --skill PR
npx skills add chinmay-sawant/developer-skills --skill feynman
npx skills add chinmay-sawant/developer-skills --skill unslop

# install all 3 skills
npx skills add chinmay-sawant/developer-skills --skill '*'

# interactive picker (no --skill flag)
npx skills add chinmay-sawant/developer-skills
```

Direct skill pages:

- [PR](https://skills.sh/chinmay-sawant/developer-skills/PR) - `npx skills add chinmay-sawant/developer-skills --skill PR`
- [feynman](https://skills.sh/chinmay-sawant/developer-skills/feynman) - `npx skills add chinmay-sawant/developer-skills --skill feynman`
- [unslop](https://skills.sh/chinmay-sawant/developer-skills/unslop) - `npx skills add chinmay-sawant/developer-skills --skill unslop`

Verify locally after install: `npx skills add ./ --list` should show 3 skills.

## The two I reach for most

### 1. Feynman - the explainer (my "make it comprehensible" skill)

Agents often return a correct but hard-to-follow answer with jargon or skipped steps. I use the Feynman skill to fix that.

It runs `/feynman <topic>` as a loop:

1. explain it to a smart 12-year-old in short sentences
2. self-audit for jargon, hand-waves, circular reasoning, or name-dropping
3. fill each gap from real source (`file:line` or authoritative docs) and re-explain

It repeats until zero gaps remain and I could retell the explanation without the agent in the room. I use `/feynman this` to re-explain the current conversation and `/feynman me <topic>` to flip roles and get graded.

Skill file: [`skills/feynman/SKILL.md`](skills/feynman/SKILL.md)

### 2. PR - the shipping skill

Whenever I open a PR, raise an issue, or leave a progress update, the agent already knows the expected shape. I use these templates so I do not reinvent it each time.

- **PRs:** [`skills/PR/PR_TEMPLATE.md`](skills/PR/PR_TEMPLATE.md) - title convention, summary, changes, impact table, test plan, related issues, and the `gh pr create` command with required `--assignee "@me"` and labels
- **Issues:** [`skills/PR/ISSUE_TEMPLATE.md`](skills/PR/ISSUE_TEMPLATE.md) - context, scope, out of scope, success criteria, and `gh issue create` command
- **Comments:** [`skills/PR/COMMENT_TEMPLATE.md`](skills/PR/COMMENT_TEMPLATE.md) - factual progress updates without chatty trailing prompts

My agents are aware of these by default - I just say "make a PR" or "open an issue" and they follow the template.

## How agents use this repo

1. Agent reads [`AGENTS.md`](AGENTS.md) at session start for the conventions ledger.
2. When a task matches a skill (e.g. "explain this" or "open a PR"), the agent loads the skill's `SKILL.md` / template from `skills/<name>/` and follows it verbatim.
3. No install step is needed if your agent is pointed at this repo. For local reuse, copy or symlink `skills/<name>/` into your global skills folder (e.g. `~/.agents/skills/` or `.opencode/skills/` depending on the tool).

## Layout

```
skills/
  PR/
    SKILL.md
    PR_TEMPLATE.md
    ISSUE_TEMPLATE.md
    COMMENT_TEMPLATE.md
  feynman/
    SKILL.md
  unslop/
    SKILL.md
AGENTS.md   - placeholder conventions ledger (keep per-project details here)
README.md   - this file
```

## Adding a new skill

1. Create `skills/<name>/SKILL.md` (or template files) following the existing shape.
2. Add a one-line entry to the table above and to `AGENTS.md` under `## Skills (this repo)`.
3. Keep the skill self-contained - an agent should be able to run it with only the files in its folder.

## Credits

- **Unslop** - original skill by [cursor/plugins](https://github.com/cursor/plugins/blob/main/pstack/skills/unslop/SKILL.md) (pstack/skills/unslop). Copied verbatim to [`skills/unslop/SKILL.md`](skills/unslop/SKILL.md) for local use.

---

See [`AGENTS.md`](AGENTS.md) for the full conventions ledger and placeholder sections to fill per project.

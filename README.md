![codex-dotfiles](./assets/codex-dotfiles.png)

# codex-dotfiles

> Install everything by copying [INSTALL.md](./INSTALL.md) into Codex and following the prompt.

Personal Codex defaults for orchestrated software development. The primary agent investigates, plans, reviews, and approves. Two cheaper custom agents handle implementation and pull-request publication.

## Workflow

1. The primary agent investigates the repository and approves a concrete plan.
2. `Luna Max Implementer` implements and validates the plan.
3. The primary agent reviews the actual diff and sends substantive fixes back to the same implementer.
4. The primary agent performs final acceptance.
5. `Luna PR Writer` creates the branch, commit, push, and pull request.

Small mechanical changes can stay in the primary agent when delegation would cost more than the work.

## Contents

```text
AGENTS.md
agents/
  luna-max-implementer.toml
  luna-pr-writer.toml
skills/
  orchestrated-development/
    SKILL.md
INSTALL.md
```

- [`AGENTS.md`](./AGENTS.md) contains concise global defaults and routes non-trivial development to the workflow skill.
- [`orchestrated-development`](./skills/orchestrated-development/SKILL.md) defines investigation, implementation, review, validation, and publication.
- [`Luna Max Implementer`](./agents/luna-max-implementer.toml) is the only write-heavy implementation worker.
- [`Luna PR Writer`](./agents/luna-pr-writer.toml) handles approved Git and pull-request operations.

The primary model is selected in Codex or its local configuration. The custom agents explicitly use `gpt-5.6-luna` with different reasoning efforts.

## Workflow dependencies

- [Ponytail](https://github.com/DietrichGebert/ponytail) keeps implementations minimal.
- [Caveman](https://github.com/JuliusBrussee/caveman) provides concise communication and commit-message skills.

The installation prompt detects these dependencies and installs only what is missing.

## Installation model

The installer creates links only for files owned by this repository:

```text
~/.codex/AGENTS.md
~/.codex/agents/luna-max-implementer.toml
~/.codex/agents/luna-pr-writer.toml
~/.agents/skills/orchestrated-development
```

It does not link or replace the whole `~/.codex` directory, so authentication, history, logs, local configuration, other agents, and other skills remain local.

See the official OpenAI documentation for [AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [skills](https://learn.chatgpt.com/docs/build-skills), and [subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents).

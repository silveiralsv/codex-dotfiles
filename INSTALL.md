# Installation prompt

Install this repository as the user's cross-platform Codex dotfiles. Complete
the installation on Windows, macOS, or Linux without replacing unrelated Codex
state.

Repository:

```text
https://github.com/silveiralsv/codex-dotfiles.git
```

## Safety requirements

- Detect the operating system, shell, home directory, and `CODEX_HOME` before
  changing anything. Use `~/.codex` only when `CODEX_HOME` is unset.
- Never link, replace, delete, or move the entire Codex home directory.
- Do not modify authentication, history, logs, `config.toml`, MCP settings, or
  unrelated agents and skills.
- Inspect every destination before creating a link.
- Leave a destination unchanged when it already resolves to the correct source.
- If a destination exists and is not the correct link, explain the conflict and
  ask before moving it to a timestamped backup.
- Never discard local repository changes. If an existing checkout is dirty,
  use it without pulling and report that it was not updated.
- Use non-destructive Git operations only. Update a clean existing checkout
  with a fast-forward-only pull.

The user invoked this prompt to install these dotfiles and the declared
Ponytail and Caveman dependencies. Do not request confirmation for ordinary
clone, link creation, or installation of a missing declared dependency. Ask
only when resolving an existing conflicting destination or when elevated
permissions are required.

## Locate the checkout

1. If the current working directory is this repository, use it.
2. Otherwise, look in common user development locations for an existing
   checkout whose `origin` identifies `silveiralsv/codex-dotfiles`, whether the
   remote uses HTTPS or SSH. Do not scan the entire home directory.
3. If none exists, clone it to `~/codex-dotfiles` on macOS/Linux or
   `$HOME\codex-dotfiles` on Windows.
4. Resolve and retain the checkout's absolute path for all link targets.

## Create only these links

Create parent directories when missing. Link individual files and the single
skill so existing user content remains available.

```text
<CODEX_HOME>/AGENTS.md
  -> <checkout>/AGENTS.md

<CODEX_HOME>/agents/luna-max-implementer.toml
  -> <checkout>/agents/luna-max-implementer.toml

<CODEX_HOME>/agents/luna-pr-writer.toml
  -> <checkout>/agents/luna-pr-writer.toml

<HOME>/.agents/skills/orchestrated-development
  -> <checkout>/skills/orchestrated-development
```

On macOS and Linux, use symbolic links.

On Windows, use PowerShell symbolic links. If Windows refuses link creation,
explain that Developer Mode or an elevated shell is required and request the
smallest necessary action. Do not silently copy files as a fallback because
copies would not stay synchronized with the repository.

## Install workflow dependencies

First inspect whether each dependency is already installed. Do not reinstall
or downgrade an existing installation.

### Ponytail

Project: <https://github.com/DietrichGebert/ponytail>

If Ponytail is absent, verify that `codex` and `node` are available, then use
the current Codex installation commands documented by the project:

```text
codex plugin marketplace add DietrichGebert/ponytail
codex plugin add ponytail@ponytail
```

Inspect `codex plugin --help` first and adapt only if the installed Codex CLI
uses an equivalent newer command. Do not guess unsupported flags.

### Caveman

Project: <https://github.com/JuliusBrussee/caveman>

The workflow needs the Caveman skills, especially `caveman-commit`; it does not
require the Caveman proxy. If the skills are absent, verify that `npx` is
available, then use the project's Codex skill installation command:

```text
npx skills add JuliusBrussee/caveman --skill '*' -a codex --yes
```

If Node.js, `npx`, Git, or Codex is missing, do not install a system package
manager or change shell profiles automatically. Report the missing prerequisite
and the smallest platform-appropriate installation step.

## Validate

After installation:

1. Verify every link exists and resolves to the intended checkout source.
2. Parse both custom-agent TOML files or otherwise confirm they are readable.
3. Confirm the `orchestrated-development` skill contains a readable `SKILL.md`.
4. Confirm Ponytail and the Caveman skills are discoverable when installed.
5. Report created links, unchanged correct links, dependency actions, backups,
   and blockers.
6. Tell the user to restart the Codex desktop app or start a new Codex session
   so global instructions, custom agents, skills, and plugins are reloaded.

Do not create a commit, push, or pull request in the dotfiles repository unless
the user separately asks for publication.

## Instruction files

Before working in a repository, read and follow every applicable `AGENTS.md`
and `CLAUDE.md` file. Merge their instructions by scope, with files closest to
the affected code taking precedence when instructions conflict.

## Git and pull requests

- Never include references to Codex, AI assistants, agents, automation, or
  generated assistance in branch names, commit messages, pull request titles
  or descriptions, authorship, co-authorship, acknowledgements, credits, or
  participation metadata.
- Always discover and follow the repository's own branch, commit, and pull
  request conventions before publishing changes.
- When a repository has no explicit branch convention, use a neutral
  issue-based descriptive branch name, such as `apo-1234-short-description`.
- Preserve the user's configured Git author identity and do not add co-author
  trailers unless the user explicitly requests them.

## Communication

Be concise without sacrificing technical accuracy.

- No greetings, filler, or conversational padding.
- Do not restate the user's request.
- Do not narrate routine tool calls.
- Do not explain obvious code changes.
- Prefer short paragraphs and bullets.
- Report only relevant findings, decisions, errors, and tradeoffs.
- Do not summarize work again after already describing it.
- Do not offer additional help unless useful.
- For errors and logs, quote only decisive lines.
- Keep code, commands, identifiers, and technical terminology exact.
- If a decision has meaningful tradeoffs, explain them normally.

## Development workflow

For feature tickets, substantial bug fixes, maintenance, refactors, tests, and
other non-trivial development requests, automatically use the
`$orchestrated-development` skill.

Do not require the user to invoke the skill, request subagents, or switch
models manually.

Handle read-only questions, investigations without requested fixes, and very
small mechanical changes directly when orchestration would cost substantially
more than the work.

Never merge a pull request automatically.

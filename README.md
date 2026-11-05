# opencode-ask-agent

A read-only OpenCode agent for asking questions. It drills into primary sources,
verifies claims against ground truth, and reports what is verified, inferred, or
still unknown.

## What it is

`ask.md` is the agent definition: model-agnostic, `mode: all` (usable as a
primary agent or delegated to as a subagent), with read-only permissions and a
narrow allowlist for shell commands that only discover, read, or inspect.

Shell commands are allowed without prompting only when they are read-only
inspection commands. Everything else asks first. Output flags such as
`--output`, secret-bearing paths such as `.env` and `~/.ssh`, and all shell
redirection are forced back to an approval prompt.

## Install

The active copy lives at `~/.config/opencode/agents/ask.md` and is a symlink to
this file:

```sh
mkdir -p ~/.config/opencode/agents
ln -sfn ~/programmingProjects/opencode-ask-agent/ask.md \
  ~/.config/opencode/agents/ask.md
```

OpenCode reloads agents automatically after saving. Use `/reload` in the TUI if
the agent does not appear immediately.

## Use

Select `ask` as the session agent, or ask the current agent to delegate a
research question to it. It is also visible as a subagent because
`mode: all`.

Example:

> Ask the `ask` agent why `foo` behaves differently in production.

## Notes

- Keep this file as the source of truth. Editing the symlink target updates the
  active agent.
- Permissions are intentionally conservative. If a legitimate inspection
  command asks for approval, approve it once or add a narrow rule here rather
  than broadening the default `shell` rule.
- `git log`, `git show`, and `git diff` can invoke configured pagers, textconv
  filters, or external diff drivers. Use trusted repositories.

## License

[MIT](LICENSE)

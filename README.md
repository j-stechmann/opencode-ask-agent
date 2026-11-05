# opencode-ask-agent

A research-focused OpenCode agent for asking questions. It drills into primary
sources, verifies claims against ground truth, and reports what is verified,
inferred, or still unknown.

## What it is

`ask.md` is the agent definition: model-agnostic, `mode: all` (usable as a
primary agent or delegated to as a subagent). The edit tools are denied, so it
cannot write files through them. Shell is allowed without prompting; read-only
behavior is a prompt-level instruction, not an enforced sandbox.

Because shell runs with the host user's authority, the agent can still modify
files through commands such as `rm`, `mv`, or output redirection. The edit deny
only blocks OpenCode's dedicated edit tools.

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
- Shell is intentionally unrestricted. If you want a hard read-only boundary,
  set the `shell` rule back to `ask` or `deny` and add an allowlist.
- `git log`, `git show`, and `git diff` can invoke configured pagers, textconv
  filters, or external diff drivers. Use trusted repositories.

## License

[MIT](LICENSE)

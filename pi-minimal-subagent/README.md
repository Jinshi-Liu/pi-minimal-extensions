# Pi Minimal Subagent

A minimal implementation based on Pi's official Subagent example.
Delegate a self-contained task to an independent Pi subprocess with per-call options and a compact status panel.

基于 Pi 官方示例的最小子 agent 实现：一个工具、五个参数，沿用官方子进程执行方式、事件解析和结果展示。

## Install

Requires Pi 1.4.0 or a compatible later release using the `@earendil-works` packages.

```sh
pi install npm:pi-minimal-subagent
```

Run `/reload` in an existing Pi session. Use one subagent implementation at a time so the tool and command names remain unique.

## Tool

Ask the main agent to delegate a task using `subagent`.

| Parameter | Meaning | Default |
| --- | --- | --- |
| `prompt` | Complete task brief, authorization boundaries, and expected result | Required |
| `model` | Pi model ID or provider/model | Parent's current model |
| `tools` | Exact tool-name allowlist; `[]` selects no tools | Parent's active tools, excluding subagent |
| `cwd` | Child working directory | Parent's working directory |
| `session` | Independent child session ID to create or resume | Fresh in-memory session |

Example tool arguments:

```json
{
  "prompt": "Read the project's README and tests. Summarize how to run the tests. Do not modify files.",
  "tools": ["read", "grep", "find", "ls"],
  "session": "test-review"
}
```

Supply the complete task context in `prompt`. Each child starts with its own conversation and loads normal Pi configuration, extensions, MCP, and skills. When needed, include exact MCP tool names in `tools`. Tool selection uses Pi's normal runtime permissions.

Repeated calls with the same `session` continue that child conversation. Persistent child sessions live under Pi's agent directory in `subagent-sessions/`. For parallel tasks, use different session IDs and separate file or browser ownership.

The extension uses per-call parameters instead of role files. The parent agent coordinates multiple calls. The child runtime excludes this subagent tool, and delegated prompts carry the task's authorization boundaries.

## Status panel

- `/subagents`: show the compact status panel below the editor.
- `/subagents hide`: hide the panel while tasks continue.
- The panel shows running/completed/failed/cancelled states, elapsed time, and recent reported activity.
- Up to five tasks are shown, with running tasks first.
- Ctrl+O expands the tool's full result and usage details.

## 中文快速上手

告诉主 agent：

> 使用 subagent，只读检查项目中的测试入口，返回运行命令与依据，不修改文件。

主 agent 为这次任务传入独立任务书及所需工具。输入 `/subagents` 查看状态，输入 `/subagents hide` 隐藏。需要续接同一个子任务时复用 `session`。

## Source and license

Community package adapted from the [official Pi 1.4.0 Subagent example](https://github.com/earendil-works/pi/tree/v1.4.0/packages/coding-agent/examples/extensions/subagent).

Retains the example's subprocess execution approach, JSON event parsing, usage display, and single-result rendering. Adds direct per-task options, independent named sessions, and a lightweight status view.

MIT. Upstream copyright and license are included in `LICENSE` and `NOTICE`.

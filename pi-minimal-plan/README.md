# Pi Minimal Plan

A minimal implementation based on Pi's official Plan Mode example.
Plan, refine, and execute numbered tasks with progress tracking and a toggleable todo panel.

基于 Pi 官方示例的最小计划模式实现：制定计划、修改计划、按步骤执行，并通过 `/todos` 切换任务面板。

## Install

Requires Pi 1.4.0 or a compatible later release using the `@earendil-works` packages.

```sh
pi install npm:pi-minimal-plan
```

Run `/reload` in an existing Pi session. If you already installed a local Plan Mode example, use one copy at a time so the command names remain unique.

## Use

1. Enter `/plan` and describe your task.
2. Review the numbered plan.
3. Choose **Execute the plan**, **Stay in plan mode**, or **Refine the plan**.
4. During execution, completed steps are tracked with `[DONE:n]` markers.

| Command | Action |
| --- | --- |
| `/plan` | Toggle planning mode; reset the current checklist |
| `Ctrl+Alt+P` | Same as `/plan` |
| `/todos` | Show the todo panel; enter again to hide it |
| `pi --plan` | Start Pi in planning mode |

The todo panel starts hidden after startup or reload. Showing or hiding it only affects display; execution and the footer progress counter continue normally.

Planning mode disables the built-in edit/write tools and checks Bash commands against the example's allowlist. Other active tools remain available. Execution restores the previous tool selection.

The official lifecycle is preserved: toggling `/plan` clears the checklist, and a fully completed plan returns to normal mode. During execution, `/plan` switches back to planning with an empty checklist. Press Esc first when you want to interrupt an active run.

## 中文快速上手

- `/plan`：进入规划，告诉 AI 你想做什么。
- 生成计划后，在菜单选择执行、继续规划或修改。
- `/todos`：输入一次显示任务面板，再输入一次隐藏；隐藏不影响执行。
- 保留官方模式切换与进度记录逻辑，仅把 `/todos` 改为面板开关。

## Source and license

Community package adapted from the [official Pi 1.4.0 Plan Mode example](https://github.com/earendil-works/pi/tree/v1.4.0/packages/coding-agent/examples/extensions/plan-mode).

MIT. Upstream copyright and license are included in `LICENSE` and `NOTICE`.

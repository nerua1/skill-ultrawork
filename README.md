# parallel-agent-executor (Ultrawork) ⚡

**Parallel execution engine — run multiple AI-agent tasks simultaneously instead of sequentially.**

Stop waiting in line when you can use all lanes. Ultrawork fires independent tasks in parallel, routes each to the right model tier, and collects results — all at once.

## Features

- **True parallelism** — spawns subagents simultaneously for independent tasks
- **Tier routing** — auto-selects the right model per task (LOW/STANDARD/THOROUGH)
- **PID tracking** — real process management via `wait -n` and PID arrays
- **Zero dependencies** — pure bash, no npm/pip/containers needed
- **OpenClaw / Hermes compatible** — plugs in as a skill

## Quick Start

```bash
# Clone to your OpenClaw skills directory
git clone https://github.com/nerudek/parallel-agent-executor.git ~/.openclaw/skills/ultrawork

# Or symlink if you keep skills elsewhere
ln -s /path/to/parallel-agent-executor ~/.openclaw/skills/ultrawork
```

## Usage

```bash
# Multiple independent tasks — all fire at once
/ultrawork "add types to auth.ts" "fix bug in utils.ts" "update README"

# With explicit count
/ultrawork 3 "task1" "task2" "task3"

# Parallel file processing
/ultrawork "analyze src/*.ts" "generate docs" "run tests"
```

Or just say: `ulw`, `ultrawork`, `run in parallel`, `do these at once`

## How It Works

```
Sequential (slow):               Parallel (fast):
┌─────────┐                      ┌─────────┐
│ Task A  │ ──10s──>             │ Task A  │ ──┐
├─────────┤                      ├─────────┤   │
│ Task B  │ ──10s──>             │ Task B  │ ──┼──10s──> Done
├─────────┤                      ├─────────┤   │
│ Task C  │ ──10s──>             │ Task C  │ ──┘
└─────────┘                      └─────────┘
Total: 30s                       Total: 10s
```

## Tier Routing

| Tier | Model | Use For | Speed |
|------|-------|---------|-------|
| LOW | qwen3-coder | Simple lookups, type exports | ⚡ Fast |
| STANDARD | qwen3.5-35b | Normal implementation | 🚀 Normal |
| THOROUGH | kimi-k2.5 | Complex analysis, security | 🐢 Thorough |

## When to Use

**Use it when:** tasks are independent and you want to cut total execution time.
**Skip it when:** tasks have dependencies (B needs A) or you need guaranteed sequential verification.

## Documentation

Full docs: [SKILL.md](SKILL.md) | [SKILL.hermes.md](SKILL.hermes.md)

---

Current version: `1.0.0` | License: MIT | Author: nerudek

If this saved you time: [☕ PayPal.me/nerudek](https://www.paypal.me/nerudek)

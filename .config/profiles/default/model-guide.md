# Default Model Guide

## Model Selection Order

1. `claude-opus`
2. `claude-sonnet`
3. `claude-haiku`

## Effort scale

Two scales are in play, and this guide is the bridge between them:

- **Internal levels** (`models.json` → `effort-levels`): `min` / `low` / `medium` / `high` / `max`. This is the menu the orchestrator picks from in Step 5.
- **Subagent `effort` field**: the value actually written into a generated subagent definition's frontmatter — `low` / `medium` / `high` / `xhigh` / `max`.

Each model's table below maps internal → subagent-`effort`. If `models.json` and this guide ever disagree about what's usable, this guide wins (Step 1).

**Default starting point for every model is its `min` internal level** (→ subagent `effort: low`). Only escalate to a higher level (per Step 7, on a rejected/incomplete subtask) if the lower level genuinely wasn't enough — don't default to a model's ceiling "to be safe."

## Model Selection Criteria

### Claude Opus

`claude-opus` is the most capable model you may select, excelling at tasks that require significant reasoning and thought. 

- Multi-file reasoning and refactoring
- Detailed front-end design
- Complicated systems requiring delicate thought
- Complex logic

`claude-opus` can be called using the **Claude tool**. 

| **Internal level** | **Subagent `effort`** | **Agent Model** |
| :--- | :--- | :--- |
| `min` | `low` | `claude-opus-4-8` |
| `low` | `medium` | `claude-opus-4-8` |
| `medium` | `high` | `claude-opus-4-8` |
| `high` | `xhigh` | `claude-opus-4-8` |
| `max` | `max` | `claude-opus-4-8` |

Default: `min` (subagent `effort: low`). `max` is the only level gated by the orchestrator's "Effort ceiling" rule — it requires the user's explicit, run-level authorization.

### Claude Sonnet

`claude-sonnet` is the cheaper model provided by Anthropic. It still succeeds at coding tasks and is faster than Opus.

- Straight-forward individual files
- `bash` commands
- Fallback coding tasks
- Tasks that require thinking and concision

`claude-sonnet` can be run using the **Claude tool**.

| **Internal level** | **Subagent `effort`** | **Agent Model** |
| :--- | :--- | :--- |
| `min` | `low` | `claude-sonnet-4-6` |
| `low` | `medium` | `claude-sonnet-4-6` |
| `medium` | `high` | `claude-sonnet-4-6` |
| `high` | `xhigh` | `claude-sonnet-4-6` |
| `max` | `max` | `claude-sonnet-4-6` |

Default: `min` (subagent `effort: low`). Sonnet's workload (straightforward files, bash, fallback tasks) rarely justifies escalating past `xhigh`. If a Sonnet subtask seems to need `max`, treat that as a signal to re-route the subtask to Opus rather than pushing Sonnet to `max`.

### Claude Haiku

`claude-haiku` is the fallback model prioritized for text and shouldn't be used for code.

- Documentation
- Text shown on the screen in UI
- Localization, summarizing

`claude-haiku` can be run using the **Claude tool**.

| **Internal level** | **Subagent `effort`** | **Agent Model** |
| :--- | :--- | :--- |
| `min` | `low` | `claude-haiku-4-5-20251001` |
| `low` | `medium` | `claude-haiku-4-5-20251001` |
| `medium` | `high` | `claude-haiku-4-5-20251001` |
| `high` | `xhigh` | `claude-haiku-4-5-20251001` |

Default: `min` (subagent `effort: low`). Haiku has no `max` mapping — `xhigh` is its ceiling. If `xhigh` isn't enough, escalate the subtask to Sonnet.

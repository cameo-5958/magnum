---
description: Add a new model to the currently active profile, with its own selection scope, effort mapping, and invocation method.
disable-model-invocation: true
---

# Add model

Adds a new model entry to the currently active profile's `models.json`, plus a matching section in `model-guide.md`.

1. Read `${CLAUDE_PLUGIN_ROOT}/.config/index.json` for `currently-selected-profile`, call it `{profile}`. Read that profile's `models.json` and `model-guide.md`.

2. Gather the new model's details. Use anything already given in $ARGUMENTS; for whatever's missing, ask the user (via `AskUserQuestion` where the choice is closed-ended, plain questions otherwise) — don't invent values for an unspecified scope or invocation:
   - **`id`** — kebab-case identifier, must not already exist in `models.json` (e.g. `claude-fable`).
   - **`name`** — short display name (e.g. `Fable`). This is what fills `[<name>] <task>` in the orchestrator's subagent-naming convention.
   - **`color`** — a hex color, distinct from existing entries' colors.
   - **`effort-levels`** — the internal scale this model exposes. Offer the two patterns already in use as defaults: 5-level `["min","low","medium","high","max"]` (full range, like Opus/Sonnet) or 4-level `["min","low","medium","high"]` (capped below `max`, like Haiku).
   - **Scope** — for `model-guide.md`: one sentence describing the model, plus a bullet list of the kinds of subtasks it should be selected for. This is what the orchestrator reads in Step 5 to decide when to route work to this model.
   - **Invocation** — exactly one of:
     - *Claude tool*: the concrete model id(s) to use per effort level (e.g. `claude-fable-5`).
     - *External provider* (Case B in `orchestrate/SKILL.md`): the exact bash invocation template, with `<prompt>` marking where the subtask instruction is substituted (e.g. `opencode run "<prompt>" --model deepseek/deepseek-v4-pro`).
   - **Position** — where this model goes in the selection order. Default: append at the end (lowest priority) unless the user specifies otherwise.

3. Update `models.json`: append `{ "id", "name", "color", "effort-levels" }` to `models`, and increment `model-count`.

4. Update `model-guide.md`:
   - Insert a new `###` subsection under `## Model Selection Criteria` at the chosen position, matching the existing format: description sentence, scope bullets, an invocation line, and an effort-mapping table.
   - Build the effort-mapping table from `## Effort scale`'s convention: a 5-level model maps `min/low/medium/high/max` → subagent `effort` `low/medium/high/xhigh/max`; a 4-level model maps `min/low/medium/high` → `low/medium/high/xhigh` (no `max` row). Default is always `min` (subagent `effort: low`).
   - For an external-provider model, write the invocation block the way `orchestrate/SKILL.md`'s Case B expects: state the exact command with the `<prompt>` placeholder, in the same form as its worked example.
   - Insert the model's `id` into `## Model Selection Order` at the chosen position, renumbering as needed.

5. Report the new model's full config (the `models.json` entry and the `model-guide.md` section) back to the user for confirmation.

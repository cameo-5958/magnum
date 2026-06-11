---
description: Change the model selection order for the currently active profile.
disable-model-invocation: true
---

# Reorder models

$ARGUMENTS is a space- or comma-separated list of model `id`s in the desired selection order (e.g. `claude-sonnet claude-opus claude-haiku`).

1. Read `${CLAUDE_PLUGIN_ROOT}/.config/index.json` for `currently-selected-profile`, call it `{profile}`.
2. Read `${CLAUDE_PLUGIN_ROOT}/.config/profiles/{profile}/models.json`. Confirm $ARGUMENTS contains every `id` in `models`, exactly once each, with no unrecognized ids. If not, stop and tell the user which ids are missing, duplicated, or unknown — do not guess.
3. Reorder `models.json`'s `models` array to match $ARGUMENTS.
4. Read `${CLAUDE_PLUGIN_ROOT}/.config/profiles/{profile}/model-guide.md`. Rewrite the `## Model Selection Order` numbered list to match $ARGUMENTS, and reorder the `###` subsections under `## Model Selection Criteria` to the same order (renumber nothing else — only the order changes).
5. Report the new order back to the user.

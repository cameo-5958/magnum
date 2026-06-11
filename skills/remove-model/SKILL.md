---
description: Remove a model from the currently active profile.
disable-model-invocation: true
---

# Remove model

$ARGUMENTS is the `id` or display `name` of the model to remove from the currently active profile.

1. Read `${CLAUDE_PLUGIN_ROOT}/.config/index.json` for `currently-selected-profile`, call it `{profile}`.
2. Read `${CLAUDE_PLUGIN_ROOT}/.config/profiles/{profile}/models.json`. Find the entry whose `id` or `name` matches $ARGUMENTS. If none matches, stop and tell the user.
3. If `models` has only one entry, stop — a profile must keep at least one model. Tell the user to use `create-profile`/edit a different profile instead.
4. If the matched model's `id` is `claude-sonnet`: `orchestrate/SKILL.md`'s Case B hardcodes a Sonnet-pinned wrapper for non-Claude models. Warn the user that removing it may break that fallback path, and confirm before continuing.
5. Remove the matching entry from `models.json`'s `models` array and decrement `model-count`.
6. Read `${CLAUDE_PLUGIN_ROOT}/.config/profiles/{profile}/model-guide.md`. Remove the model's `###` subsection under `## Model Selection Criteria`, and remove its entry from the `## Model Selection Order` numbered list (renumber the remaining entries).
7. Report what was removed and the resulting model order.

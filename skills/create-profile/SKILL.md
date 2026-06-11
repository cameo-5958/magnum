---
description: Create a new profile by copying an existing one.
disable-model-invocation: true
---

# Create profile

The first word of $ARGUMENTS is the new profile's name. An optional second word names an existing profile to copy from; if omitted, copy from the `currently-selected-profile` (read from `${CLAUDE_PLUGIN_ROOT}/.config/index.json`).

1. Confirm `${CLAUDE_PLUGIN_ROOT}/.config/profiles/<new-name>/` does not already exist. If it does, stop and tell the user.
2. Confirm the source profile's directory `${CLAUDE_PLUGIN_ROOT}/.config/profiles/<source>/` exists. If not, stop and tell the user.
3. Copy `models.json` and `model-guide.md` from the source profile into a new `${CLAUDE_PLUGIN_ROOT}/.config/profiles/<new-name>/` directory, unchanged.
4. Tell the user the new profile was created from `<source>`, and that they can use `add-model`, `remove-model`, and `reorder-models` (which act on `currently-selected-profile`) to customize it, then `swap-profile` to make it active.

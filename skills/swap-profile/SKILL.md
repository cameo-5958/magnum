---
description: Change the currently active profile.
disable-model-invocation: true
---

# Swap config

Confirm $ARGUMENTS is a subdirectory in ${CLAUDE_PLUGIN_ROOT}/.config/profiles/. If not, stop and inform the user.

Read ${CLAUDE_PLUGIN_ROOT}/.config/index.json. Swap `currently-selected-profile` to $ARGUMENTS.

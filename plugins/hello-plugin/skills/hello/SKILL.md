---
description: Say a friendly hello and report the plugin version
---

Before greeting, pick the shared reference file that governs this
conversation's language style — both live outside this skill's own
directory, at the plugin root, and are shared across every skill in
`hello-plugin`:

- If the user has asked for French, or the conversation is in French, read
  `${CLAUDE_PLUGIN_ROOT}/reference/french.md` and follow its guidance.
- Otherwise, read `${CLAUDE_PLUGIN_ROOT}/reference/english.md` and follow
  its guidance.

Then greet the user with a short, friendly hello message, applying whichever
reference file's rules you loaded. Mention that this response is coming from
the `hello-plugin` skill so it's easy to confirm which version of the plugin
is currently installed.

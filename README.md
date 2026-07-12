# claude-plugin-marketplace-test

A minimal Claude Code plugin marketplace, used for testing versioning
workflows (e.g. how version bumps show up in VS Code Copilot).

## Structure

```
.claude-plugin/marketplace.json      marketplace catalog
plugins/hello-plugin/
  .claude-plugin/plugin.json         plugin manifest (name, version, author)
  reference/english.md               shared reference file (British spelling rules)
  reference/french.md                shared reference file (respond in French)
  skills/hello/SKILL.md              the "hello" skill (loads a reference/ file conditionally)
  skills/goodbye/SKILL.md            the "goodbye" skill
  skills/version/SKILL.md            the "version" skill
```

`reference/` sits at the plugin root, outside any single skill's own directory,
and is shared across all skills in `hello-plugin`. `skills/hello/SKILL.md`
reaches it via `${CLAUDE_PLUGIN_ROOT}/reference/<file>.md` — this variable is
substituted inline in skill content, so it resolves correctly regardless of
how deeply the skill is nested. This is testing whether reference files can
be shared across skills within one plugin (they can, as long as they stay
inside the plugin root — files outside the plugin directory entirely are not
copied into the install cache and won't resolve).

## Testing locally with Claude Code

```
/plugin marketplace add ./claude-plugin-marketplace-test
/plugin install hello-plugin@claude-plugin-marketplace-test
/hello-plugin:hello
/hello-plugin:goodbye
/hello-plugin:version
```

## Testing from GitHub

```
/plugin marketplace add lim-Qizhen/claude-plugin-marketplace-test
/plugin install hello-plugin@claude-plugin-marketplace-test
```

## Third-party plugin: figma

The `figma` entry points straight at Figma's own repo
(`figma/mcp-server-guide`), which already ships a `.claude-plugin/plugin.json`
and its own `skills/` directory (including `figma-use`). No files are copied
into this marketplace — Claude Code clones/updates directly from Figma's repo,
and version resolution follows *their* `plugin.json` version field.

```
/plugin install figma@claude-plugin-marketplace-test
```

To pick up a new Figma release, run `/plugin marketplace update` (refreshes
the catalog) then `/plugin update figma@claude-plugin-marketplace-test`
(re-resolves and re-fetches if Figma bumped their version).

## Bumping the version

The plugin version lives only in `plugins/hello-plugin/.claude-plugin/plugin.json`
(the `version` field). Bump it, commit, and push — that's the change to
watch propagate through version-tracking tooling.

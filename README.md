# claude-plugin-marketplace-test

A minimal Claude Code plugin marketplace, used for testing versioning
workflows (e.g. how version bumps show up in VS Code Copilot).

## Structure

```
.claude-plugin/marketplace.json      marketplace catalog
plugins/hello-plugin/
  .claude-plugin/plugin.json         plugin manifest (name, version, author)
  skills/hello/SKILL.md              the "hello" skill
  skills/goodbye/SKILL.md            the "goodbye" skill
  skills/version/SKILL.md            the "version" skill
```

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

## Bumping the version

The plugin version lives only in `plugins/hello-plugin/.claude-plugin/plugin.json`
(the `version` field). Bump it, commit, and push — that's the change to
watch propagate through version-tracking tooling.

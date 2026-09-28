# codex

OpenAI Codex CLI layer for OpenCharly images.

The `codex` candy installs the OpenAI Codex CLI globally via npm so `codex` is on
`PATH`. It depends on `nodejs` and ships a `package.json` pinning
`@openai/codex`, which the build installs globally into `~/.npm-global/bin`. A
CUE-validated tmux terminal profile exposes it through the generic Charly agent
channel.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `codex` |
| Requires | `layer-nodejs` |
| Binary | `${HOME}/.npm-global/bin/codex` |
| Pinned package | `@openai/codex` `0.144.6` (in `package.json`) |
| Install files | `charly.yml`, `package.json` |
| Agent channel | `agent_provide: tmux`, profile `codex` (terminal) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-codex:v2026.243.0408'
```

After the image is built:

```bash
~/.npm-global/bin/codex --version
node -e 'console.log(require(process.env.HOME+"/.npm-global/lib/node_modules/@openai/codex/package.json").version)'
```

The `plan:` asserts the installed package exactly matches the declared
deterministic pin.

## Layout

- `charly.yml` — the `codex:` candy entity: the `nodejs` require, the tmux
  terminal profile, and the `check:` assertions, plus the embedded `skill:`
  entity.
- `package.json` — pins `@openai/codex`.
- `CHANGELOG/` — per-CalVer release notes.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-coder:codex` — the npm-global install reference
- Runtime parent: `/charly-coder:nodejs`
- Sibling AI CLIs: `/charly-coder:claude-code`, `/charly-coder:gemini`
- Bundled by: `/charly-openclaw:openclaw-full` (metalayer)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella

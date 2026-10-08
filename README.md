# layer-mcporter

The `mcporter` MCP server CLI, installed globally via npm, as a standalone
OpenCharly layer repo.

The candy depends on `nodejs` and ships a `package.json` pinning `mcporter`,
which the build installs globally under `NPM_CONFIG_PREFIX` (`~/.npm-global`).
The result is verifiable: the `mcporter` binary lands at
`~/.npm-global/bin/mcporter`, the package is unpacked under
`~/.npm-global/lib/node_modules/mcporter`, `mcporter --version` exits cleanly
with a semantic version, and `mcporter --help` lists the core MCP commands
(`list`, `call`) that define the CLI surface.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `mcporter` |
| Binary | `~/.npm-global/bin/mcporter` |
| Dependencies | `layer-nodejs` |
| Service / port | none |

## How to use it

Compose the layer as a nested `candy:` list inside a named box body:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-mcporter:v2026.243.0409'
```

```bash
mcporter list        # list configured MCP servers
mcporter call <tool> # call an MCP tool
```

## Layout

- `charly.yml` — the `mcporter:` candy entity (the `require:`, the `check:`
  assertions, and the embedded `mcporter-skill:` skill entity).
- `package.json` — pins the `mcporter` npm package.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:mcporter` — the MCP server CLI, its install path,
  and its `list` / `call` surface.
- `/charly-coder:nodejs` — required runtime dependency.
- `/charly-image:layer` — candy authoring reference.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella

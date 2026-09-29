# AGENTS.md — layer-mcporter

Standalone candy repo for the `mcporter` layer — the MCP server CLI installed
globally via npm. The candy lives in `charly.yml` at the repo root: the
`require:` on `layer-nodejs`, the `check:` assertions, and the embedded `skill:`
entity projected into the marketplace corpus as `/charly-tools:mcporter`. The npm
package the build installs globally is pinned in `package.json`.

Canonical files:

- `charly.yml` — the `mcporter:` candy entity and the `mcporter-skill:` skill
  entity.
- `package.json` — pins the `mcporter` npm package.
- `CHANGELOG/` — per-CalVer release history; read it before changing baked checks.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-tools:mcporter` — the owning skill. The MCP server CLI, its install
  path, and its `list` / `call` surface. Load before editing or troubleshooting
  the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, and service declarations). Load before editing any entity field or
  plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.
- The `check:` assertions run the binary from `${HOME}/.npm-global/bin/`; keep
  the npm global prefix contract in sync with the `nodejs` candy.

## Modify this repo

- Edit the `mcporter:` candy entity AND the `mcporter-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- The npm package pin lives in `package.json`; keep it and the `check:`
  assertions in sync.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.

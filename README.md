# DesignSkills

DesignSkills is the design pack of
[Grove](https://github.com/Linkuistics/grove). It ships Grove's design session
kinds and four design craft skills as agent skills. Grove's core supplies the
spine that each kind loads.

## Kinds

| Kind | Skill | Purpose |
| --- | --- | --- |
| `design` | `grove-design` | Establishes how to build what the requirements state, and delivers a spec, a set of decision records, or both |
| `review-design` | `grove-review-design` | Reads one design artifact adversarially and writes findings, not fixes |
| `integrate-review-design` | `grove-integrate-review-design` | Triages the findings of one `review-design` leaf and applies the real ones |

`grove-design` has two resources inside its own skill directory.
`references/visual-design-discussion.md` holds the procedure for a visual
design discussion, and `assets/diagram-viewer.html` is its diagram viewer.

The review and integration kinds belong to families whose members ship in
several packs. Their family procedures therefore stay in Grove's spine, as
`references/review.md` and `references/integrate-review.md`. Each of the two
kinds loads the `grove` skill and then reads its family file there.

## Craft skills

| Skill | Purpose |
| --- | --- |
| `decision-records` | Keeps decision records as the minimum coherent set that describes the design's current state |
| `codebase-design` | Designs and reviews module interfaces, coupling and test seams |
| `cli-tool-design` | Designs and audits command-line tools that agents can drive |
| `model-led-development` | Routes a specification question to the instrument that answers it, and lets a checked model lead the implementation |

A craft skill is guidance that a session of any kind can use. No Grove mandate
names it.

The ADR and spec formats stay in Grove's core, in the spine's `ADR-FORMAT.md`
and `SPEC-FORMAT.md`. The craft skills `decision-records` and
`codebase-design` deepen those two formats. Without the craft skills, the
formats in core still bind.

## Layout

The source directory is `plugins/design`. It is the Claude Code plugin root and
the Ravel source directory. It has two roots:

- `skills` holds the three kind skills.
- `craft` holds the four craft skills.

The plugin manifest lists `"skills": ["./craft/"]`. Claude Code scans `skills/`
by default and adds `craft/`. `plugins/design/PROVENANCE.md` holds the sources
of the craft skills. The repository root holds the files that the pack does not
deliver: this README, the licence and the Taskfile.

Grove's external pack contract, `docs/specs/external-pack-contract.md` in the
Grove repository, states the layout, the references between skills and the
conformance rules.

## Install

Each route also needs Grove's core, which supplies the `grove` skill.

### Ravel

Add this record to the `skills.sources` list of the Ravel settings, beside the
record of Grove's core. Replace `<checkout>` with the absolute path of a
checkout of this repository:

```json
{ "id": "design", "type": "local", "path": "<checkout>/plugins/design", "roots": ["skills", "craft"] }
```

Ravel reads the checkout as a local directory. It does not fetch or update the
checkout. A tool outside Ravel holds the checkout at a published commit.

### Claude Code plugin

Install the plugin from Grove's marketplace:

```text
/plugin marketplace add Linkuistics/grove
/plugin install design@linkuistics
```

The manifest declares the dependency `grove`, so the installation also adds
Grove's core. The skills then have the namespace `design:`, for example
`design:grove-design` and `design:codebase-design`.

### Manual installation

Grove's manual installer links the skills of both roots of a pack:

```sh
<grove checkout>/plugins/install.sh --pack <design checkout>/plugins/design
```

Grove's marketplace entry for this pack arrives with the Grove release that
removes the design kinds and the four craft skills from Grove. Until that
release, Grove ships its own copies of these skills. The installer refuses a
skill name that two scanned plugins ship, so it does not install this pack
beside Grove's `linkuistics` plugin before that release.

## Checks

Run every check of the pack:

```sh
task check
```

The checks use Grove's conformance runner from a plain Git checkout of Grove,
under `.cache/grove/`. The `Taskfile.yml` variable `GROVE_COMMIT` names that
Grove commit. The variable `GROVE_REPOSITORY` names the public Grove
repository.

- `task check:conformance` checks the pack alone, then the aggregate of
  Grove's core and this pack. Conformance covers only the kind skills in
  `skills/`. It does not read `craft/`.
- `task check:plugin` checks the Claude Code plugin with
  `claude plugin validate`, which covers the manifest and the craft skills of
  `craft/`. It skips when Claude Code is not installed.

`GROVE_COMMIT` names Grove commit `84fba18c1f98b694bcf440181c3853a6ec343772`,
which removed Grove's own copies of these skills. The pack passes alone, and
the aggregate reads each design kind and each moved rule once.

## Provenance

The skills come from Grove commit `c800d311a541b02237f06b5a9b5ddba4c2993765`,
at these paths:

- `plugins/grove/skills/grove-design/`, with `SKILL.md`,
  `assets/diagram-viewer.html` and `references/visual-design-discussion.md`
- `plugins/grove/skills/grove-review-design/`
- `plugins/grove/skills/grove-integrate-review-design/`
- `plugins/linkuistics/skills/decision-records/`
- `plugins/linkuistics/skills/codebase-design/`, with `SKILL.md` and
  `references/design-examples.md`
- `plugins/linkuistics/skills/cli-tool-design/`, with `SKILL.md` and
  `references/auditing-and-refactoring.md`
- `plugins/linkuistics/skills/model-led-development/`, with `SKILL.md` and
  three files in `references/`

Grove keeps the full history of these files. This repository imports none of
it. The move made these changes:

- Each kind skill has the bare-name opening of Grove's external pack contract.
  The kinds have no other change.
- `model-led-development` names `doubt-driven-development` by its bare name.
  It cites Grove's formal-methods records by their public URLs. Those records
  stay in Grove.
- `decision-records/LICENSES/mattpocock-skills.LICENSE` is new. It is a copy
  of the file in Grove's spine.
- `plugins/design/PROVENANCE.md` holds the sections of Grove's
  `plugins/linkuistics/PROVENANCE.md` for the craft skills. The section of
  `model-led-development` names Grove's repository and its public URLs where
  the source said "this repository".

Grove commit `84fba18c1f98b694bcf440181c3853a6ec343772` removed Grove's copies
of these files. `GROVE_COMMIT` names that commit, so the aggregate check reads
each design kind once.

`decision-records` adapts passages of
[mattpocock/skills](https://github.com/mattpocock/skills), which uses the MIT
licence. `decision-records/LICENSES/mattpocock-skills.LICENSE` holds that
licence text.

## Licence

DesignSkills uses the Apache License 2.0, as Grove does. The `LICENSE` file
holds the full text.

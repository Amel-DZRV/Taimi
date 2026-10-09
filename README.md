# Taimi

A general-purpose, project-agnostic agent-company workflow for **feature development**. Amel acts as CEO: he decides what gets built, the company builds it, he tests the result.

Taimi is the features half of the old Scruffy skillset. Scruffy keeps bugs. The two diverge fully: Taimi's backbone is forked from Scruffy's `feature-dev` and `verification` and does not stay in sync.

- `DESIGN.md`: what Taimi is and why.
- `taimi_roles.md`: how each role thinks, what it draws on, what it remembers, what it can call.
- `SKILL.md`: the driver. Start here to run a feature.

## Layout

```
taimi/
├── SKILL.md                     the driver: flow, CEO touchpoints, terminal states
├── DESIGN.md
├── taimi_roles.md
├── roles/<role>/                persona.md, skills.md, tools.md (19 roles)
├── memory/global/<role>.md      durable cross-project judgment, one file per role
├── mechanisms/
│   ├── council/RUNNER.md        shared council runner (Product/Business, Design/Architecture)
│   └── pipeline/
│       ├── RUNNER.md            shared per-platform pipeline runner + ship steps
│       ├── references/          spec-and-plan, orchestration, verification, worktrees, pr-format
│       └── scripts/             ui-touch.sh, pair-diff.py, tree-diff.py (forked from Scruffy)
├── rules/engineering-discipline.md
└── scripts/init-project.sh      creates a project's empty per-role memory files
```

`roles/` is pure definition and project-agnostic. Nothing project-specific ever accumulates there. Per-project facts live in each project's own repo at `memory/projects/<role>.md`, never in this repo.

## Install

Symlink the repo as one skill so Claude Code discovers `SKILL.md`:

```bash
mkdir -p ~/.claude/skills
ln -sfn "$PWD" ~/.claude/skills/taimi
chmod +x mechanisms/pipeline/scripts/* scripts/*
```

Runners and roles are plain files the driver reads, not separate skills, so there is nothing else to register.

For a new project:

```bash
scripts/init-project.sh /path/to/project
```

The visual proof scripts need Python with Pillow (`pip install pillow`).

## Dependencies

Notion (the documentation home and the project's source of truth), GitHub (PRs and auto-merge), and a harness that can run parallel subagents and worktrees. QA's mobile toolchain needs a simulator or emulator and the accessibility-tree tooling.

## Status

Written, not yet run. The first real feature will show what the runners get wrong; expect corrections to land in the role memory files, which is the design working.

Open items are listed in `DESIGN.md` section 9 and `taimi_roles.md` section 14.

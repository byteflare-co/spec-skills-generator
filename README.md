# spec-skills-generator

Auto-generate 3-layer specification documents and maintenance skills for any codebase.

## What It Does

This plugin analyzes your codebase and generates:

- **3-layer specification documents**: Overview (`01_overview.md`), Business Spec (`02_business_spec.md`), Technical Spec (`03_technical_spec.md`)
- **`/spec` skill**: Q&A skill for querying your specifications
- **`/spec-maintenance` skill**: Keeps specs in sync with code changes
- **`check_spec_drift.py`**: Automated drift detection script
- **CLAUDE.md integration**: Impact mapping section for your project

## Installation

```
/plugin marketplace add byteflare-co/spec-skills-generator
/plugin install spec-skills-generator@spec-skills-generator
```

## Usage

Run the generator skill:

```
/spec-skills-generator:generate
```

The skill will:

1. Auto-detect your project structure (languages, entry points, IaC, tests, etc.)
2. Ask configuration questions (output directory, existing docs)
3. Deep-analyze your codebase
4. Generate 3-layer spec documents
5. Create `/spec` and `/spec-maintenance` skills
6. Set up drift detection and CLAUDE.md integration

## Output Language

Spec documents are generated in the language detected from your project's CLAUDE.md `<language>` tag. If no language is configured, defaults to English.

## Generated Files

| File | Description |
|------|-------------|
| `docs/specification/01_overview.md` | Project overview, architecture, component catalog |
| `docs/specification/02_business_spec.md` | Business rules, domain model, use cases |
| `docs/specification/03_technical_spec.md` | API specs, data models, infrastructure |
| `.claude/skills/spec/SKILL.md` | `/spec` Q&A skill |
| `.claude/skills/spec-maintenance/SKILL.md` | `/spec-maintenance` skill |
| `scripts/check_spec_drift.py` | Spec-code drift checker |

## Requirements

- Claude Code CLI
- Python 3.10+ (for `discover_project.py` and `check_spec_drift.py`)

## How It Works

The plugin uses an 8-phase workflow:

1. **Project Discovery** — Runs `discover_project.py` to detect project structure
2. **Information Gathering** — Asks user for configuration preferences
3. **Spec Generation** — Deep-analyzes code and generates 3-layer specs
4. **Spec Skill Generation** — Creates `/spec` Q&A skill
5. **Maintenance Skill Generation** — Creates `/spec-maintenance` skill
6. **Drift Checker Generation** — Creates `check_spec_drift.py`
7. **Build System Integration** — Updates Makefile/package.json and CLAUDE.md
8. **Verification** — Runs drift checker to validate generated specs

## License

MIT

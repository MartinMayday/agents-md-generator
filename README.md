# agents-md-generator

SOP files for generating AGENTS.md files with progressive context loading.

## Purpose

This repository hosts the Standard Operating Procedure (SOP) files for the agents-md-generator tool, which automatically generates production-ready `AGENTS.md` files for any folder. The generated files include progressive context loading protocol (4 levels) and comprehensive validation.

## Repository Structure

```
__ref/SOPs/agents-md-generator/
├── directives/
│   ├── MISSION-OBJECTIVES.md
│   ├── TASKER-ORDERS.md
│   ├── AGENTS-MD-TEMPLATE.md
│   ├── VALIDATION-CHECKLIST.md
│   └── EXAMPLES-WRONG-vs-CORRECT.md
└── executions/
    ├── analyze-folder.py
    ├── extract-context.py
    ├── validate-agents-md.py
    └── check-existing-agents-md.py
```

## Usage

This repository is designed to be used with the `/generate-agents-md` slash command, which can fetch SOP files from GitHub using raw URLs.

### Configuration

Add to your project's `AGENTS.md` or `.claude/commands/generate-agents-md.md`:

```yaml
sop_source:
  github:
    user: "MartinMayday"
    repo: "agents-md-generator"
    branch: "main"  # or specific tag like "v1.1.0"
```

### Raw URLs

Directives can be accessed via:
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/directives/MISSION-OBJECTIVES.md`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/directives/TASKER-ORDERS.md`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/directives/AGENTS-MD-TEMPLATE.md`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/directives/VALIDATION-CHECKLIST.md`

Scripts can be accessed via:
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/executions/analyze-folder.py`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/executions/extract-context.py`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/executions/validate-agents-md.py`
- `https://raw.githubusercontent.com/MartinMayday/agents-md-generator/main/__ref/SOPs/agents-md-generator/executions/check-existing-agents-md.py`

## Versioning

- `main` branch: Latest development version (may be unstable)
- Tags (e.g., `v1.1.0`): Stable releases (recommended for production use)

## License

See the source repository for license information.

## Repository

**GitHub:** https://github.com/MartinMayday/agents-md-generator

## Support

For issues or questions, refer to the source repository documentation.

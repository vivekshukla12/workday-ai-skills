# Workday AI Skills

A collection of reusable AI skills for Workday-related tasks, workflows, integrations, reporting, analytics, and development.

These skills provide focused instructions and supporting references that help compatible AI assistants perform specific Workday-related tasks consistently.

## Available Skills

| Skill | Description |
| --- | --- |
| [WQL Formatter](skills/wql-formatter/) | Formats or minifies Workday Query Language queries while preserving their logic and identifying plausible syntax errors. |
| [Workforce Crisis Planner](skills/workforce-crisis-planner/) | Links workforce and financial data to crisis scenarios, gaps, approved mitigations, and implementation timelines. |
| [Workday Prism Assistant](skills/workday-prism-assistant/) | Supports Prism Analytics architecture, ingestion, transformations, calculated fields, security, publishing, scheduling, and troubleshooting. |

Additional skills may be added under the `skills/` directory.

## Repository Structure

```text
workday-ai-skills/
├── skills/
│   ├── wql-formatter/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   └── references/
│   ├── workforce-crisis-planner/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   ├── assets/
│   │   └── references/
│   └── workday-prism-assistant/
│       ├── SKILL.md
│       ├── agents/
│       └── references/
├── AGENTS.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

Each skill is self-contained. Supporting references required by a skill are stored inside its directory so the complete skill can be migrated between compatible environments.

## Using a Skill

Download or clone the repository and import or copy the complete skill directory into the skills location supported by your AI environment.

Do not copy only `SKILL.md` when the skill contains an `agents/`, `references/`, `scripts/`, or `assets/` directory. These files may be required for the skill to function correctly.

Example invocation:

```text
Use $wql-formatter to format this WQL query:
SELECT worker,location FROM allWorkers
```

Installation and invocation methods may vary between AI products and clients.

## Contributing

Contributions that add or improve reusable Workday-related AI skills are welcome.

Before contributing, read:

- [Repository safety rules](AGENTS.md)
- [Contribution guidelines](CONTRIBUTING.md)

Place each skill in its own directory under `skills/`.

## Public Repository Safety

This repository must never contain:

- Credentials, secrets, tokens, certificates, or authentication information.
- Tenant names, tenant URLs, internal aliases, configuration, or environment metadata.
- Customer, employer, partner, or confidential project information.
- Employee, candidate, payroll, banking, identity, or other production data.
- Real WIDs, reference IDs, employee IDs, event IDs, or other tenant identifiers.
- Real tenant queries, API payloads, responses, logs, screenshots, exports, or error traces.
- Proprietary manuals, downloaded documentation, course material, or substantial copied text.

All examples must use synthetic data and obvious placeholders. Every contribution must be reviewed and scanned before it is published, including any new Git history.

See [AGENTS.md](AGENTS.md) for the complete mandatory publication safeguards.

## Documentation and Source Policy

Skills may use publicly available Workday documentation as an authoritative technical source for product terminology, supported functionality, syntax, workflows, limitations, and other factual behavior.

Repository content derived from those sources must be independently authored. Public documentation may be summarized, normalized into decision guidance, or used to create original examples and AI-agent instructions. Third-party manuals, downloaded PDFs, screenshots, course files, and substantial copied passages are not included.

Where practical, reference files link directly to official public Workday documentation so users can verify current product behavior. See the [official Workday Documentation](https://doc.workday.com/) for authoritative and current information.

Customer-only documentation, tenant-specific configuration, NDA-covered material, and confidential Workday/customer information must not be published in this repository.

## Workday Intellectual Property Notice

Workday, Workday Prism Analytics, and other Workday product names and marks are trademarks or registered trademarks of Workday, Inc. Workday retains all rights to its trademarks, documentation, software, interfaces, training materials, and other proprietary materials.

This repository does not redistribute Workday documentation. Explanations, examples, workflows, prompts, decision logic, and AI-agent instructions in this repository are independently authored technical resources.

## Disclaimer

This is an independent community project. It is not affiliated with, endorsed by, sponsored by, or maintained by Workday, Inc.

The skills in this repository are provided as general technical resources and do not replace official Workday documentation, tenant validation, contractual guidance, or professional advice. Users should verify version-sensitive and tenant-specific behavior against official Workday sources and their own authorized environment.

## License

This project is available under the [Apache License 2.0](LICENSE). The repository license applies to independently authored repository content and does not grant rights to third-party trademarks, documentation, software, or other intellectual property referenced by the project.

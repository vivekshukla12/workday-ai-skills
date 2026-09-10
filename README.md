# Workday AI Skills

A collection of reusable AI skills for Workday-related tasks, workflows, integrations, reporting, and development.

These skills provide focused instructions and supporting references that help compatible AI assistants perform specific Workday-related tasks consistently.

## Available Skills

| Skill | Description |
| --- | --- |
| [WQL Formatter](skills/wql-formatter/) | Formats or minifies Workday Query Language queries while preserving their logic and identifying plausible syntax errors. |

Additional skills may be added under the `skills/` directory.

## Repository Structure

```text
workday-ai-skills/
├── skills/
│   └── wql-formatter/
│       ├── SKILL.md
│       ├── agents/
│       │   └── openai.yaml
│       └── references/
│           └── wql-syntax.md
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

## Documentation

Skills may include concise, independently written summaries of publicly available technical documentation when that information is necessary for reliable operation.

Third-party manuals, PDFs, screenshots, and substantial copied passages are not included. Refer to the [official Workday Documentation](https://doc.workday.com/) for authoritative and current product information.

## Disclaimer

This is an independent community project. It is not affiliated with, endorsed by, or sponsored by Workday, Inc.

Workday and related product names and marks belong to their respective owners. The skills in this repository are provided as general technical resources and do not replace official documentation, tenant validation, or professional guidance.

## License

This project is available under the [Apache License 2.0](LICENSE).

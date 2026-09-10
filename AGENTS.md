# Repository Safety Rules

This is a public repository. Before adding or updating any skill, inspect both the proposed files and the complete Git history that will be pushed.

## Never commit

- Credentials or secrets, including passwords, API keys, OAuth tokens, refresh tokens, client secrets, certificates, private keys, cookies, connection strings, or authentication headers.
- Tenant-specific metadata, including tenant names or URLs, customer-created aliases, report definitions, calculated-field definitions, integration configuration, security configuration, internal object identifiers, or environment details.
- Customer, employer, project, or partner information that is not already intentionally public.
- Personal, employee, candidate, payroll, financial, banking, health, contact, identity, or other production data.
- Real WIDs, reference IDs, employee IDs, candidate IDs, organization IDs, event IDs, or other identifiers copied from a Workday tenant.
- Real customer queries, API payloads, responses, logs, screenshots, exports, test evidence, or error traces. Use minimal synthetic examples and obvious placeholders.
- Proprietary manuals, downloaded PDFs, course materials, screenshots, or substantial copied passages from third-party documentation. Link to public documentation and write concise original summaries instead.
- Local artifacts and environment files such as `.env`, credential stores, editor state, caches, build output, archives, or exported `.skill` packages unless the repository intentionally releases them and they have been audited.

## Required pre-publication check

Before every push or pull request:

1. Review the complete diff and the list of files to be published.
2. Scan the working tree, staged content, and all commits that are not already on the remote branch for secrets and prohibited data.
3. Inspect commit authors, messages, filenames, and binary files as well as text content.
4. Confirm all examples are synthetic and contain no realistic tenant identifiers or personal data.
5. Confirm every included reference is original, appropriately licensed, or limited to a link and concise paraphrase.
6. Stop the publication if any result is ambiguous. Remove or sanitize the material, rescan the full affected history, and publish only after the scan is clean.

Do not rely on `.gitignore` or deletion in a later commit: content present in Git history remains publicly retrievable. If prohibited data enters history, do not push it. If it has already been pushed, treat it as exposed, rotate any affected secret, and rewrite or purge the public history.

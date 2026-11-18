---
name: wql-formatter
description: Format, minify, or compare Workday Query Language (WQL) queries while preserving their semantics. Produce a structured diff report for two queries and identify plausible syntax problems or spelling issues when relevant.
---

# WQL Formatter

Format, minify, or compare WQL while preserving the supplied query text and meaning.

## Modes

- **Format:** Apply readable indentation and line breaks. Put major clauses such as `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, and `OFFSET` at their logical levels. Put selected fields on separate lines when useful. Indent nested field selections inside `{...}`.
- **Minify:** Remove unnecessary whitespace and line breaks while retaining whitespace needed to separate tokens.
- **Compare:** Compare an original/baseline query with an updated/comparison query and prepare a copy-ready diff report. If either query or its role is unclear, ask for the missing query or clarify which one is original and which is updated.
- If the requested mode is genuinely unclear, ask whether the user wants formatting, minification, or comparison. When one dense query is supplied with an unqualified request to improve readability, infer **Format**.

## Comparison method

Compare the query structure and tokens, not raw character positions. Ignore whitespace-only formatting differences when identifying substantive changes; do not treat reordered fields as additions or removals.

Check and report applicable changes in these areas:

- **SELECT fields:** fields or expressions added or removed; aliases added, removed, or changed; nested related-object fields added or removed.
- **FROM:** data source or its arguments changed.
- **Filters:** `WHERE ON` relationships and conditions, and `WHERE` predicates, operators, or values changed.
- **Other clauses:** `PARAMETERS`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, or `OFFSET` changed.
- **Field order:** mention separately only when it changed and the user wants ordering included.

Match fields by their exact source identifiers and nested paths, keeping aliases as separate comparison details. If identity is ambiguous, call that out instead of guessing. Do not claim tenant-level field availability, validity, or equivalence without tenant metadata or query execution. A user may request a fields-only report; in that case omit changes to other clauses.

Return the report in a plain-text fenced code block so it can be copied easily. Include only substantive changes, organized by added, removed, renamed/re-aliased, or otherwise changed items. If nothing substantive changed, state that the queries differ only in formatting or that no substantive differences were detected, as appropriate.

## Spelling review during comparison

Check changed aliases and human-readable labels for likely spelling mistakes. Keep spelling findings separate from the diff report and never list a typo as a query change. Do not silently correct any query text.

Technical field identifiers may be tenant-defined and intentionally unusual. Preserve them. If an identifier looks misspelled, treat it as a verification note rather than a confirmed typo, unless the user says to ignore technical identifiers. If a likely typo is found, report it separately and hold the diff report until the user fixes or explicitly asks to proceed despite the typo.

## Preservation rules

- Preserve identifiers, aliases, operators, literals, clause order, selected fields, and query logic exactly when formatting or minifying.
- Never silently correct, rename, add, remove, reorder, or normalize query elements.
- Preserve all content inside quoted strings exactly, including whitespace and escapes.
- Treat comments conservatively. Do not remove them during minification if removal could change token boundaries or meaning.
- If the query arrived inside a Markdown table or code fence, remove only the surrounding Markdown representation. Unescape Markdown-only identifier escapes such as `\\_` when they are clearly presentation artifacts rather than WQL characters.

## Validation

Validate a query while formatting or minifying it. Check at minimum:

- balanced parentheses, braces, and quoted strings;
- missing or misplaced commas;
- recognizable WQL clause ordering;
- incomplete expressions or operators;
- malformed nested field selections;
- aliases in positions that appear invalid under the available Workday WQL documentation.

Before validating, read [references/wql-syntax.md](references/wql-syntax.md). Treat it as the bundled syntax baseline. If the user supplies newer Workday documentation, use it for version-specific rules while preserving this skill's output contract.

Do not claim tenant-level validation of data sources, fields, security, or business object relationships unless tenant metadata or execution results establish it.

## Output contract

- For **Format** or **Minify**, when no plausible syntax problem is found, return only the transformed query in a fenced `sql` code block. Do not add validation feedback, commentary, or a success statement.
- For **Format** or **Minify**, when a plausible syntax problem is found, still return the requested transformation without correcting it. After the code block, identify only the suspected location, the likely problem, and a concise example of the error message Workday may return. Label predicted wording as a **possible error message**, not an exact server response. Then ask whether the user wants a corrected query generated.
- For **Compare**, follow the comparison method and spelling-review rules above. Keep spelling findings outside the diff report.
- Do not discuss general query quality, optimization, field availability, tenant security, or stylistic recommendations unless the user explicitly asks.

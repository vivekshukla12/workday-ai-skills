---
name: wql-formatter
description: Format or minify Workday Query Language (WQL) queries while preserving their semantics, and report only plausible syntax problems with a likely error message. Use when a user supplies WQL and asks to format, pretty-print, compact, or minify it.
---

# WQL Formatter

Transform the supplied WQL query in the mode the user requests.

## Modes

- **Format:** Apply readable indentation and line breaks. Put major clauses such as `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, and `OFFSET` at their logical levels. Put selected fields on separate lines when useful. Indent nested field selections inside `{...}`.
- **Minify:** Remove unnecessary whitespace and line breaks while retaining whitespace needed to separate tokens.
- If the requested mode is genuinely unclear, ask whether the user wants formatting or minification. When a single-line or densely packed query is supplied with an unqualified request to improve readability, infer **Format**.

## Preservation rules

- Preserve identifiers, aliases, operators, literals, clause order, selected fields, and query logic exactly.
- Never silently correct, rename, add, remove, reorder, or normalize query elements.
- Preserve all content inside quoted strings exactly, including whitespace and escapes.
- Treat comments conservatively. Do not remove them during minification if removal could change token boundaries or meaning.
- If the query arrived inside a Markdown table or code fence, remove only the surrounding Markdown representation. Unescape Markdown-only identifier escapes such as `\_` when they are clearly presentation artifacts rather than WQL characters.

## Validation

Validate the query while transforming it. Check at minimum:

- balanced parentheses, braces, and quoted strings;
- missing or misplaced commas;
- recognizable WQL clause ordering;
- incomplete expressions or operators;
- malformed nested field selections;
- aliases in positions that appear invalid under the available Workday WQL documentation.

Before validating, read [references/wql-syntax.md](references/wql-syntax.md). Treat it as the bundled syntax baseline. If the user supplies newer Workday documentation, use it for version-specific rules while preserving this skill's output contract.

Do not claim tenant-level validation of data sources, fields, security, or business object relationships unless tenant metadata or execution results establish it.

## Output contract

- When no plausible syntax problem is found, return only the transformed query in a fenced `sql` code block. Do not add validation feedback, commentary, or a success statement.
- When a plausible syntax problem is found, still return the requested transformation without correcting it. After the code block, identify only the suspected location, the likely problem, and a concise example of the error message Workday may return. Label predicted wording as a **possible error message**, not an exact server response.
- Then ask whether the user wants a corrected query generated.
- Do not discuss general query quality, optimization, field availability, tenant security, or stylistic recommendations unless the user explicitly asks.

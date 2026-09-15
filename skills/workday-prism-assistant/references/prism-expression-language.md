# Workday Prism Expression Language Reference

This file is an independently authored working reference for AI assistance with Prism calculated fields and advanced filter expressions. Function names and syntax families are based on public Workday Prism Analytics documentation. Use official Workday documentation for authoritative version-specific behavior.

## Where Prism expressions are used

Prism expressions are used mainly in:

- Prism calculated fields, where an expression produces a value for each input row.
- Advanced Filter-stage conditions, where a Boolean expression determines whether a row remains in the dataset.
- Other supported dataset rules that accept Prism Boolean expressions.

Do not assume the same literal formatting rules apply in every context. In particular, date literals can differ between advanced filters and calculated fields.

## Core syntax rules

- Enclose field names containing spaces or special characters in square brackets, for example `[Worker Status]`.
- Text literals use double quotes.
- Numeric literals can be written directly as numbers.
- Keep comparison operands type-compatible.
- `CASE` uses `CASE WHEN ... THEN ... ELSE ... END` syntax.
- Every result branch of a `CASE` expression should resolve to the same field type; convert explicitly when needed.
- Use `COALESCE` when a business rule needs the first non-NULL value from a set of alternatives.
- Use `/* ... */` for comments in Prism expressions where supported.
- Treat NULL deliberately. Do not assume arithmetic, comparisons, or joins will treat NULL like zero or an empty string.

## Boolean-expression guidance

A Boolean expression evaluates to true, false, or, in some invalid/NULL cases, NULL.

Typical comparison capabilities documented for Prism include:

- Equal: `=` or `==`
- Greater/less than: `>`, `<`, `>=`, `<=`
- Alternative not-greater/not-less forms: `!>` and `!<`
- Not equal: `<>`, `!=`, or `^=`
- Range test: `BETWEEN ... AND ...`
- Membership: `IN(...)`
- Simple wildcard pattern matching: `LIKE(...)`
- NULL test: `IS NULL`
- Logical composition with `AND`, `OR`, and supported logical operators

Use operators only with compatible field types. If a user compares Text to Numeric, Date to Text, or Instance to Text, first determine whether conversion or an instance-specific function is required.

## Date handling

### Advanced Filter stage

Public Prism documentation supports ISO-style date literals directly in advanced filter expressions. Shorter ISO date forms can be interpreted with omitted time components defaulted appropriately.

Example pattern:

```text
[Effective Date] >= 2026-01-01
```

### Calculated field

For a literal date in a calculated field, prefer `TO_DATE` with an explicit input format rather than assuming a text literal is already a Date.

Example:

```text
CASE WHEN [Effective Date] >= TO_DATE("2026-01-01", "yyyy-MM-dd")
THEN "Current"
ELSE "Prior"
END
```

Use the actual source date format supplied by the user. Do not invent a format mask when the source format is unknown.

## Conversion functions

Use conversion functions when source and target field types differ or when an expression requires a specific type.

Documented Prism conversion functions include:

`BUILD_CURRENCY`, `CAST`, `EPOCH_MS_TO_DATE`, `EXTRACT_AMOUNT`, `EXTRACT_CODE`, `EXTRACT_CODE_TEXT`, `TO_BOOLEAN`, `TO_CURRENCY`, `TO_DATE`, `TO_DECIMAL`, `TO_DOUBLE`, `TO_INT`, `TO_LONG`, `TO_STRING`.

Selection guidance:

- Use `TO_DATE` to parse text into a Date using an explicit format.
- Use `TO_STRING` when text operations are needed on non-Text input.
- Use `TO_INT`, `TO_LONG`, `TO_DECIMAL`, or `TO_DOUBLE` based on required numeric semantics.
- Use `EXTRACT_AMOUNT` when only the numeric amount of a Currency field is needed.
- Use `EXTRACT_CODE` or `EXTRACT_CODE_TEXT` when the currency code is needed.
- Use `BUILD_CURRENCY` or `TO_CURRENCY` only when the requirement genuinely needs a Currency result rather than a plain numeric field.

## Date functions

Documented Prism date functions include:

`DAYS_BETWEEN`, `DATE_ADD`, `EXTRACT`, `HOURS_BETWEEN`, `MILLISECONDS_BETWEEN`, `MINUTES_BETWEEN`, `SECONDS_BETWEEN`, `TODAY`, `TRUNC`, `YEAR_DIFF`.

Use these for elapsed-time calculations, date component extraction, date arithmetic, current-date logic, and date truncation. Confirm whether the calculation expects calendar boundaries, elapsed duration, or exact timestamps before selecting the function.

## Informational functions

Documented informational function:

`IS_VALID`

Use it when the requirement is to test whether a value or conversion is valid before applying downstream logic.

## Instance functions

Documented Prism instance functions include:

`CREATE_MULTI_INSTANCE`, `INSTANCE_CONTAINS_ANY`, `INSTANCE_COUNT`, `INSTANCE_EQUALS`, `INSTANCE_IS_SUPERSET_OF`.

Use instance functions when the field is an Instance or Multi-Instance type. Do not replace instance comparison with ordinary text comparison merely because the displayed value looks textual.

Agent checks:

- Confirm whether the field is Instance or Multi-Instance.
- Do not fabricate WIDs or instance identifiers.
- Prefer actual tenant-supplied instance values when an expression requires them.

## Logical functions

Documented Prism logical functions include:

`CASE`, `COALESCE`.

### CASE

Use `CASE` for conditional row logic.

Synthetic example:

```text
CASE
WHEN [Employment Type] = "Employee" THEN "Internal"
WHEN [Employment Type] = "Contingent" THEN "External"
ELSE "Other"
END
```

All outputs in this example are Text.

### COALESCE

Use `COALESCE` to select the first non-NULL value.

Synthetic example:

```text
COALESCE([Preferred Email], [Business Email], [Personal Email])
```

Only use this pattern when all fields are type-compatible and the business rule permits this fallback order.

## Math functions

Documented Prism math functions include:

`DIV`, `EXP`, `FLOOR`, `HASH`, `LN`, `MOD`, `POW`, `ROUND`.

Selection guidance:

- `ROUND` for decimal rounding.
- `FLOOR` for downward integer boundary logic.
- `DIV` for integer-style quotient behavior where documented.
- `MOD` for remainder calculations.
- `POW`, `EXP`, and `LN` for mathematical transformations.
- `HASH` for deterministic bucketing/partition-style use cases where appropriate.

Check numeric type and truncation behavior before choosing `DIV`, `TO_INT`, or other integer conversions.

## Text functions

Documented Prism text functions include:

`CIDR_MATCH`, `CONCAT`, `EXTRACT_COOKIE`, `EXTRACT_VALUE`, `FILE_NAME`, `HEX_TO_IP`, `INSTR`, `JAVA_STRING`, `JOIN_STRINGS`, `JSON_DECIMAL`, `JSON_DOUBLE`, `JSON_INTEGER`, `JSON_LONG`, `JSON_STRING`, `LENGTH`, `PACK_VALUES`, `REGEX`, `REGEX_REPLACE`, `REVERSE`, `SUBSTRING`, `TO_LOWER`, `TO_PROPER`, `TO_UPPER`, `TRIM`, `XPATH_STRING`.

Common selection guidance:

- `CONCAT` for direct text concatenation.
- `JOIN_STRINGS` when joining multiple values with a delimiter and documented NULL handling is useful.
- `TRIM`, `TO_UPPER`, `TO_LOWER`, and `TO_PROPER` for text normalization.
- `SUBSTRING` and `INSTR` for positional extraction.
- `REGEX` and `REGEX_REPLACE` for pattern-based extraction or replacement.
- `JSON_*` functions for extracting typed values from JSON text.
- `XPATH_STRING` for extracting text from XML using XPath.
- `FILE_NAME` only where the dataset/source context supports access to the originating file name.

## URL functions

Documented Prism URL functions include:

`URL_AUTHORITY`, `URL_FRAGMENT`, `URL_HOST`, `URL_PATH`, `URL_PORT`, `URL_PROTOCOL`, `URL_QUERY`, `URLDECODE`.

Use these when the requirement is to parse URL components or decode URL-encoded text instead of building fragile substring logic.

## Window functions

Documented Prism window functions include:

`AVG`, `COUNT`, `FIRST`, `LAG`, `LAST`, `LEAD`, `MAX`, `MIN`, `RANK`, `ROW_NUMBER`, `SUM`.

Window functions operate across related rows while still returning row-level output.

Before generating a window expression, identify:

1. Partition key: which rows form one logical group.
2. Ordering field: which field determines sequence.
3. Direction: ascending or descending.
4. Frame: whether the function should see the whole partition, prior rows, a bounded range, or another supported frame.
5. Tie behavior: especially for `RANK` and ordering-sensitive logic.

Typical use cases:

- `LAG`/`LEAD`: compare the current row with prior/next effective-dated data.
- `ROW_NUMBER`: select or identify row sequence within a partition.
- `RANK`: rank rows by a measure while preserving tie semantics.
- `FIRST`/`LAST`: retrieve the first or last value according to the specified ordering.
- Window `SUM`, `AVG`, `COUNT`, `MIN`, `MAX`: cumulative or partition-aware measures.

Never generate a window function without explicit or inferable partition and ordering logic; otherwise the expression may be syntactically valid but semantically wrong.

## Regular expressions

Prism documentation includes regular-expression support and a separate regex reference.

Use regex only when simpler text functions are insufficient.

Agent checks:

- Clarify whether the user wants validation, extraction, or replacement.
- Escape literal regex characters correctly.
- Keep examples synthetic.
- Avoid presenting a regex as production-safe until it is tested against representative input examples.

## Expression review checklist

When reviewing a Prism expression, check:

- Balanced parentheses and `CASE ... END` structure.
- Correct field-name brackets.
- Quoted Text literals.
- Compatible input types for functions/operators.
- Consistent `CASE` return type.
- Explicit NULL handling where required.
- Correct date-literal approach for the expression context.
- Correct Instance/Multi-Instance function usage.
- Correct partition/order semantics for window functions.
- Regex escaping when applicable.

Do not claim successful tenant validation unless the expression has actually been evaluated in the tenant or the user provides a successful result.

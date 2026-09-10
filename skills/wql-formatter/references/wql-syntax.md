# WQL Syntax Baseline

Use this reference to validate syntax while formatting or minifying a Workday Query Language query. It is a concise paraphrase of the WQL material in the 2026 Workday *Admin Guide: Reporting and Analytics*. It is not a tenant schema.

## Query shape and clause order

The broad clause sequence is:

```sql
[PARAMETERS ...]
SELECT ...
FROM ...
[WHERE ON ...]
[WHERE ...]
[GROUP BY ...]
[HAVING ...]
[ORDER BY ...]
[LIMIT ...]
```

`SELECT` and `FROM` are required. `PARAMETERS`, when used, starts the query. Every `WHERE ON` clause must precede the ordinary `WHERE` clause. `HAVING` requires `GROUP BY`.

## PARAMETERS

Syntax:

```sql
PARAMETERS parameter1=value1,parameter2=value2
```

- A parameter can appear only once.
- Report-field prompt values belong in `PARAMETERS`.
- Data-source and data-source-filter prompt values may be supplied through `PARAMETERS` or `FROM`, but not duplicated across both.
- A data-source filter itself is identified in `FROM` using `dataSourceFilter=filterAlias`.

## SELECT

Syntax patterns:

```sql
SELECT field1,field2 AS customAlias,function(field3)
SELECT relationshipField{relatedField1,relatedField2} AS customAlias
```

- Separate every selected expression and every nested related field with a comma.
- A custom alias follows a complete selected expression and uses `AS`.
- A WQL reserved keyword cannot be used as an unquoted custom alias.
- `SELECT *` is unsupported.
- Supported aggregation forms are `AVG(field)`, `COUNT()`, `COUNT(DISTINCT field)`, `MIN(field)`, `MAX(field)`, and `SUM(field)`.
- `COUNT()` takes no argument.
- `COUNT(DISTINCT field)` applies to text and single-instance fields.

## Related business objects

Use braces only in the `SELECT` projection:

```sql
SELECT worker,dependents{legalName_FirstName,age} AS Dependents
FROM allWorkers
```

- The brace contents are one or more comma-separated fields from the related business object.
- If the same relationship field is selected multiple times as separate groups, give each group a unique alias.
- Related-business-object projections are not supported in queries using `GROUP BY`.
- Related-object fields are supported in `SELECT` and may be filtered through `WHERE ON`; omit braces in `WHERE ON`.

## FROM

Syntax patterns:

```sql
FROM dataSourceAlias
FROM dataSourceAlias(dataSourceFilter=filterAlias,prompt1=value1)
FROM dataSourceAlias(effectiveAsOfDate="2018-01-01",entryMoment="2019-01-01 12:30:00Z")
```

- Arguments inside parentheses are comma-separated assignments.
- Effective/entry date or moment arguments are valid only for data sources that support them.

## WHERE

Syntax pattern:

```sql
WHERE field1=value1 AND (field2>=value2 OR field3 IS EMPTY)
```

- Parentheses determine evaluation precedence; `AND` and `OR` join conditions.
- Supported comparison operators include `=`, `!=`, `>`, `>=`, `<`, `<=`, `contains`, `not contains`, `startswith`, `endswith`, `in`, `not in`, `is empty`, and `is not empty`.
- Operator applicability depends on the field type. Ordering comparisons apply to dates and numeric fields. Text matching operators apply to text. `IN`/`NOT IN` apply to instance and text fields.
- An instance can be matched using Workday IDs or a reference-ID expression such as `field IN (Reference_ID_Type=Reference_ID)`.

## WHERE ON

Syntax pattern:

```sql
WHERE ON relationshipField relatedField1=value1 AND relatedField2 IS NOT EMPTY
```

- Each `WHERE ON` names the relationship field followed by conditions on its related fields.
- Do not use `{}` around related fields in this clause.
- Multiple `WHERE ON` clauses may be used for different relationships, but all must occur before `WHERE`.

## GROUP BY, HAVING, and ORDER BY

```sql
GROUP BY field1,field2
HAVING COUNT()>100
ORDER BY field1 ASC,field2 DESC
```

- `GROUP BY` uses selected field aliases and cannot group by aggregate expressions, currency fields, or multi-instance fields.
- `HAVING` filters a group or aggregate and is invalid without `GROUP BY`.
- `ORDER BY` uses field aliases with optional `ASC` or `DESC`.

## LIMIT

```sql
LIMIT 100
```

The query-clause value must be greater than zero and less than 1,000,000. Do not confuse the WQL `LIMIT` clause, which caps total results, with the REST API's lowercase `limit` and `offset` pagination parameters.

## Values, dates, and identifiers

- Date: `YYYY-MM-DD`.
- Time: `HH:MM:SS` using a 24-hour clock.
- UTC datetime: `YYYY-MM-DD HH:MM:SSZ`.
- PST datetime: `YYYY-MM-DD HH:MM:SS`.
- Quoted values may use single or double quotes as allowed by the relevant expression.
- WQL does not support escape-character syntax. Do not introduce escapes while formatting or minifying.
- Workday validates Workday ID formats during execution.

## Validation boundary

Static validation can identify structural problems such as an absent comma, misplaced clause, unbalanced delimiter, invalid aggregate form, or unsupported `SELECT *`. It cannot prove that a data-source alias, filter alias, field alias, relationship, prompt, or security entitlement exists in a particular tenant. Tenant metadata or query execution is required for those checks.

# DB2 SQL for VS Code

[![VS Code](https://img.shields.io/badge/VS%20Code-DB2%20SQL-blue)](https://code.visualstudio.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Deep **IBM Db2 SQL syntax highlighting** for Visual Studio Code.

Designed for developers who work with `.db2` scripts and need DB2-aware highlighting instead of generic SQL or MSSQL highlighting.

## Features

- `.db2` files are recognized as **DB2 SQL**.
- DB2 SQL keywords, clauses and operators.
- DB2 data types and storage modifiers.
- Built-in functions: aggregate, window, string, numeric, date/time, conversion, XML and JSON.
- Common DB2 special registers such as `CURRENT_DATE`, `CURRENT_SCHEMA`, `CURRENT_USER` and `CURRENT_TIMESTAMP`.
- Transaction isolation syntax: `WITH UR`, `WITH CS`, `WITH RS`, `WITH RR`.
- CTE and recursive SQL support.
- Window functions and frame clauses.
- MERGE, cursor and dynamic SQL syntax.
- SQL PL constructs including procedures, handlers, `SIGNAL`, `RESIGNAL` and `GET DIAGNOSTICS`.
- Declared global temporary tables.
- Temporal tables and system/business time syntax.
- Quoted identifiers, parameters, numeric literals and DB2 variables.
- Snippets for common DB2 development patterns.

## Installation

### From VSIX

Package the extension locally:

```bash
npm install
npm run package
```

Then install the generated `.vsix` using **Extensions: Install from VSIX...** or:

```bash
code --install-extension vscode-db2-0.2.0.vsix
```

### From Marketplace

After publication, search for **DB2 SQL** by publisher `nguyenngocbinh` in the VS Code Extensions view.

## Snippets

| Prefix | Purpose |
|---|---|
| `db2select` | SELECT with `WITH UR` |
| `db2cte` | Common table expression |
| `db2merge` | MERGE statement |
| `db2proc` | SQL procedure skeleton |
| `db2cursor` | Cursor declaration/lifecycle |
| `db2handler` | SQL exception handler |
| `db2signal` | SIGNAL SQLSTATE |
| `db2temp` | Declared global temporary table |
| `db2window` | Window function |
| `db2temporal` | Temporal query |

## Example

```sql
WITH ACTIVE_CUSTOMERS AS (
    SELECT CUSTOMER_ID,
           CURRENT_DATE AS RUN_DATE,
           ROW_NUMBER() OVER (
               PARTITION BY SEGMENT
               ORDER BY CUSTOMER_ID
           ) AS RN
    FROM CUSTOMER
    WHERE STATUS = 'ACTIVE'
)
SELECT *
FROM ACTIVE_CUSTOMERS
FETCH FIRST 100 ROWS ONLY
WITH UR;
```

## Development

Install the local packaging dependency:

```bash
npm install
```

Package:

```bash
npm run package
```

Validate the extension manifest without packaging:

```bash
npx vsce ls
```

Publish manually after configuring your Marketplace publisher and `VSCE_PAT`:

```bash
npm run publish
```

## Automated publishing

The repository includes a GitHub Actions workflow that packages the extension on pushes and pull requests. A tag matching `v*` triggers the publish job.

Create a repository secret named `VSCE_PAT`, then publish a release by pushing a version tag, for example:

```bash
git tag v0.2.0
git push origin v0.2.0
```

The workflow uses the `VSCE_PAT` secret only during the Marketplace publish step.

## Scope

This extension currently focuses on **syntax highlighting and snippets**. It does not execute SQL, connect to a Db2 server, provide query results, or replace a DB2 database client.

## License

MIT

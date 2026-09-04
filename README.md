# DB2 SQL for VS Code

Syntax highlighting for IBM Db2 SQL using the `.db2` file extension.

## Features

- `.db2` files are recognized as **DB2 SQL**.
- Highlights DB2 SQL keywords, data types, functions, strings, numbers and comments.
- Includes common Db2-specific syntax such as `WITH UR`, `CURRENT DATE`, `CURRENT TIMESTAMP`, `FETCH FIRST`, `DECLARE GLOBAL TEMPORARY`, `SQLCODE` and `SQLSTATE`.

## Development

Install dependencies and package with the VS Code Extension CLI:

```bash
npm install -g @vscode/vsce
vsce package
```

Then install the generated `.vsix` from **Extensions: Install from VSIX...**.

## Example

```sql
SELECT CUSTOMER_ID,
       CURRENT DATE AS RUN_DATE,
       COUNT(*) AS CNT
FROM CUSTOMER
WHERE STATUS = 'ACTIVE'
GROUP BY CUSTOMER_ID
WITH UR;
```

## License

MIT

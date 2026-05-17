# Excel Integration — pandas + openpyxl (Theory)

Purpose: Best practices for reading, writing, and interacting with Excel files in finance workflows.

## Reading Excel reliably
- `pd.read_excel('file.xlsx', sheet_name='Sheet1', dtype=..., parse_dates=..., usecols=...)`

Best practices
- Use `usecols` to limit imported columns and improve speed
- If Excel files have merged cells or complex layouts, extract data from a clean export or use `openpyxl` to programmatically handle structure
- Prefer CSV exports when possible for predictable parsing

Common mistakes
- Assuming consistent sheet names and column positions across files
- Not handling leading/trailing whitespace in header names

## Writing Excel
- `df.to_excel('out.xlsx', index=False)` — basic
- Use `pd.ExcelWriter(..., engine='openpyxl')` for multiple sheets and formatting

Using openpyxl for formatting
- `openpyxl` lets you style cells, set column widths, and preserve formulas
- Workflow: write base data with `pandas` then open with `openpyxl` to apply formatting

Best practices
- Keep data and presentation steps separate: generate clean sheets, then add formatting as a final step
- Avoid trying to preserve complicated cell formulas through pandas — use `openpyxl` or a template workbook

Common mistakes
- Saving files with index column unintentionally (`index=True`) — use `index=False`
- Overwriting important sheets without backups

## Automation tips
- Standardize import templates (column names, date formats)
- Validate sample rows after read and before heavy processing

References
- openpyxl: https://openpyxl.readthedocs.io/
- pandas IO docs: https://pandas.pydata.org/docs/user_guide/io.html#excel-files
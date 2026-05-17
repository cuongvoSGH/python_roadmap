# Reconciliation Workflows — Theory and Best Practices

Purpose: Practical theory for common reconciliation tasks using pandas and Python tools. Focused on ledger/report matching, exception identification, and summary reporting.

## Typical reconciliation steps
1. Load both reports using `pd.read_csv` / `pd.read_excel` with `dtype` and `parse_dates`.
2. Standardize column names (lowercase, remove spaces) and value formats (trim, upper/lower case).
3. Convert key columns to consistent dtypes and formats (strings, zero-padded IDs, normalized dates).
4. Remove obvious duplicates or create a unique key where necessary.
5. Use `pd.merge(left, right, on='key', how='outer', indicator=True)` to find unmatched rows.
6. For matched rows, compare numeric columns with tolerances: `abs(a - b) <= tolerance`.
7. Aggregate at desired levels (account, period) and compare totals.
8. Produce exception report and summary totals.

Best practices
- Always keep the original raw files untouched; work on copies and keep a transformation log.
- Use `indicator=True` in `merge` to quickly classify `left_only`, `right_only`, and `both` records.
- When amounts are floats, convert to integer cents (`(amount * 100).astype(int)`) for exact comparisons.
- Define and document tolerances for expected small differences (rounding, FX rates).
- Use `validate=` in `merge` (e.g., `one_to_one`, `one_to_many`) to ensure key cardinality assumptions.

Common mistakes
- Comparing unrounded floats directly and flagging false positives due to precision errors.
- Not normalizing keys (leading zeros, extra whitespace, different case) which results in false mismatches.
- Overlooking timezone differences or inconsistent date formats when matching on dates.
- Failing to check duplicates that inflate totals after merges.

Example reconciliation pattern

```python
# load
left = pd.read_csv('report_a.csv', dtype={'invoice':'str'}, parse_dates=['date'])
right = pd.read_csv('report_b.csv', dtype={'invoice':'str'}, parse_dates=['date'])

# normalize
for df in (left, right):
    df.columns = df.columns.str.strip().str.lower()
    df['invoice'] = df['invoice'].str.strip()

# merge with indicator
merged = left.merge(right, on='invoice', how='outer', suffixes=('_a','_b'), indicator=True)

# find mismatches
mismatched_amounts = merged[(merged['_merge']=='both') & (merged['amount_a'] != merged['amount_b'])]
```

Validation and reporting
- After merge, check record counts: `len(left)`, `len(right)`, `len(merged)` and counts by `_merge`.
- Produce summary: total amounts by `_merge` group and by account.
- Export exceptions to Excel for review: `exceptions.to_excel('exceptions.xlsx', index=False)`.

References and next steps
- Use these patterns as templates and adapt for currency conversions, multi-currency ledgers, and tolerance windows.
- Consider adding logging, unit tests, and small sample checks for automation.
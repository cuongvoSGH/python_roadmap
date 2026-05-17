# pandas — Selection, Merge, GroupBy, Filtering, Slicing and Transformation

Purpose: Practical, finance-focused reference for selecting and transforming tabular data with pandas. This file emphasizes selection (filtering/slicing), merges/joins, `groupby`/aggregation, and common transformation patterns with best practices and typical mistakes.

## Quick principles
- Work on copies or reassign results; avoid invisible state changes.
- Prefer vectorized operations and built-in pandas methods; they are faster and clearer than Python loops.
- Be explicit about dtypes and date parsing when reading data: this prevents many downstream issues.

---

## Selection: filtering and slicing

1) Boolean masks (recommended)

```python
# simple filter
df_good = df[df['amount'] > 0]

# combined conditions (use parentheses)
df_large_usd = df[(df['amount'] > 1000) & (df['currency'] == 'USD')]
```

Best practices
- Use `.loc` for assignment and to avoid chained-assignment: `df.loc[mask, 'col'] = value`.
- Use `df.query("amount > 1000 and currency == 'USD'")` for readable filters on simple column names.

Common mistakes
- Writing `df[df['A'] > 0]['B'] = x` (chained assignment). Use `df.loc[df['A']>0, 'B'] = x`.

2) `.loc` and `.iloc` (label vs position)

```python
# label-based: rows by index label, columns by name
df.loc[100:200, ['date','amount']]

# position-based: rows/cols by integer positions
df.iloc[0:10, 0:3]
```

Use `.at` / `.iat` for fast scalar get/set.

3) `.isin`, `.between`, `.str` and method-based filters

```python
df[df['account'].isin(['A1','A2'])]
df[df['date'].between('2024-01-01','2024-03-31')]
df[df['customer_name'].str.contains('Inc', na=False)]
```

4) `.nlargest` / `.nsmallest` / `.sample`

```python
top5 = df.nlargest(5, 'amount')
random50 = df.sample(50, random_state=1)
```

5) Selecting with `.filter` (column selection by pattern)

```python
df.filter(regex='^amt_|_amount$')
```

---

## Bucketing: `pd.cut` and `pd.qcut` (categorical bins)

Use `pd.cut` to split a numeric column into discrete intervals (bins) and optionally assign labels. This is useful for sized buckets (e.g., invoice amounts: small/medium/large) or for creating categorical groups for reporting.

Basic example with fixed bins

```python
import pandas as pd

bins = [0, 100, 500, 1000, float('inf')]
labels = ['small', 'medium', 'large', 'xlarge']
df['amount_bucket'] = pd.cut(df['amount'], bins=bins, labels=labels, right=False, include_lowest=True)
```

Notes
- `right=False` makes bins left-inclusive and right-exclusive; default `right=True` makes them right-inclusive.
- `include_lowest=True` ensures the lowest value is included in the first bin.
- The result is a `Categorical` dtype; you can inspect categories with `df['amount_bucket'].cat.categories` and use `.cat.codes` for integer codes.

Quantile-based bins with `pd.qcut`

```python
# split into quartiles with labelled buckets
df['amount_qbucket'] = pd.qcut(df['amount'], q=4, labels=['Q1','Q2','Q3','Q4'])
```

`pd.qcut` creates bins with approximately equal counts (quantiles). It's handy when you want evenly populated groups rather than fixed numeric ranges.

Best practices
- For reproducible reports, define explicit `bins` when business rules require fixed thresholds.
- Use `pd.qcut` for distributional buckets (percentiles/quantiles) but be aware of duplicate values at bin edges which can raise errors; add `duplicates='drop'` if needed.
- After creating buckets, treat the column as categorical for memory and speed: `df['bucket'] = df['bucket'].astype('category')`.
- Use `df.groupby('amount_bucket')['amount'].agg(total='sum', count='count')` to summarize by bucket.

Common pitfalls
- Non-unique or unsorted `bins` will raise errors; ensure bins are monotonic increasing.
- Mixed dtypes in labels (strings vs numbers) will coerce the resulting column to `object` when using `np.where` alternatives — prefer labels when categorical semantics are intended.
- Nulls (NaN) remain NaN after cutting; handle them explicitly with `fillna` if necessary.


## Indexing & time-based selection

- Set a `DatetimeIndex` for time-series selection: `df['date']=pd.to_datetime(df['date']); df.set_index('date', inplace=True)`.
- Use `.loc['2024-01':'2024-03']` to slice ranges efficiently.
- Use `resample` for aggregation: `df.resample('M').sum()`.

Best practices
- Convert dates on read using `parse_dates` for speed and fewer surprises.

Common mistakes
- Forgetting to sort by date before taking rolling/expanding windows.

---

## Merging / joining tables

Core patterns

```python
# inner (intersection), left, right, outer (full)
merged = pd.merge(left, right, on='invoice', how='left', indicator=True, suffixes=('_a','_b'))

# validate cardinality expectations
merged = pd.merge(l, r, on='invoice', how='left', validate='one_to_one')
```

Key tips
- Use `indicator=True` to immediately see `_merge` values: `'left_only'`, `'right_only'`, `'both'`.
- Use `suffixes` to keep column provenance clear when columns share names.
- Use `validate` to assert assumptions (`one_to_one`, `one_to_many`, `many_to_one`, `many_to_many`). It raises on unexpected cardinality.

Common workflows for reconciliation
- Outer merge with `indicator=True` to find unmatched rows.
- For matched rows, compare numeric fields (consider tolerance):

```python
matched = merged[merged['_merge']=='both']
mismatch = matched[~(matched['amount_a'].fillna(0).round(2) == matched['amount_b'].fillna(0).round(2))]
```

Best practices
- Normalize keys first: strip whitespace, unify case, zero-pad IDs if needed.
- Check for duplicates on merge keys before merging: `left.duplicated(subset='invoice').sum()`.
- After merge, check row counts: `len(left)`, `len(right)`, `len(merged)` and value counts of `_merge`.

Common mistakes
- Merging on columns with differing dtypes (int vs str) — convert keys to the same dtype first.
- Overwriting original data without saving the merged result or tracking provenance.

---

## GroupBy, aggregation and transform

GroupBy basics

```python
agg = df.groupby(['account']).agg(total_amount=('amount','sum'), txn_count=('amount','count'))
```

Using `transform` to broadcast group results back to rows

```python
# percent of group total for each row
group_sum = df.groupby('account')['amount'].transform('sum')
df['pct_of_account'] = df['amount'] / group_sum
```


When to use `agg`, `transform`, `apply`
- `agg` returns aggregated index (one row per group) — good for reporting.
- `transform` returns an aligned Series (same length as original) — good for row-level enrichment.
- `apply` runs a Python function per group — use sparingly (slower) when `agg`/`transform` can't express the logic.

### Deep dive — `transform` vs `apply`

Purpose: choose the right tool for group-wise work. This short guide explains semantics, return shapes, performance trade-offs, and idiomatic replacements.

1) Return shape and alignment

- `agg` (or `aggregate`) reduces each group to one or more aggregated values. Result has one row per group.
- `transform` computes a value for each row by group, returning a Series aligned to the original DataFrame index (same length as input). Use it when you want to broadcast group-level calculations back to rows (e.g., percent of group total).
- `apply` runs an arbitrary function on each group and can return a scalar, Series, or DataFrame. Because it's flexible, the output shape varies and pandas has to concatenate results, which is slower.

Examples

```python
# transform: compute pct of group total (broadcasted back to rows)
df['group_sum'] = df.groupby('account')['amount'].transform('sum')
df['pct_of_group'] = df['amount'] / df['group_sum']

# apply: when you need a custom per-group result (returns aggregated DF or Series)
def top_n_rows(g, n=2):
	return g.nlargest(n, 'amount')

top2 = df.groupby('account').apply(top_n_rows)
```

2) Performance considerations

- Built-in aggregations (e.g., `sum`, `mean`, `median`) and `transform` using string aliases are implemented in optimized C/NumPy paths and are fast.
- `apply` falls back to Python-level iteration over groups and is significantly slower for large numbers of groups or large groups.
- If a `transform` can express your logic, prefer it; if `agg` with named aggregations suffices, prefer that for concise output.

3) Common idiomatic replacements (faster alternatives to `apply`)

- Use `transform` instead of `apply(lambda g: g / g.sum())` when broadcasting a group-wise normalization:

```python
# slower: apply per-group
df['pct'] = df.groupby('account')['amount'].apply(lambda s: s / s.sum())

# faster: transform (vectorized path)
df['pct'] = df['amount'] / df.groupby('account')['amount'].transform('sum')
```

- Use `agg` with multiple named aggregations instead of `apply` that returns scalars:

```python
# avoid: apply building a dict per group
def stats(g):
	return pd.Series({'total': g.sum(), 'count': g.count(), 'max': g.max()})

# prefer: explicit agg
df.groupby('account')['amount'].agg(total='sum', count='count', max='max')
```

4) When `apply` is appropriate

- Very custom transformations that cannot be composed from existing vectorized operations (complex reshaping per group, non-uniform outputs per group).
- Returning variable-length outputs per group (e.g., top-N rows per group) — but be aware results need careful reindexing or resetting.

5) Pitfalls and gotchas

- `transform` requires the function to return a scalar or sequence of the same length as the group. Returning an incorrect shape raises an error.
- `apply` may change the index; remember to `.reset_index(drop=True)` or `.rename_axis(None)` when combining results.
- Using lambdas with `transform` can be slower than using named functions or built-ins.
- Mixing `apply` results with other DataFrame columns requires careful alignment — prefer joining/merging aggregated results explicitly when in doubt.

6) Quick checklist: choose the right tool

- Need one row per group (summary)? → use `agg`.
- Need row-wise enrichment using group-level stats? → use `transform`.
- Need flexible, custom per-group outputs (variable shape)? → use `apply`, but test performance and consider alternatives.

Example: replacement pattern

```python
# compute z-score within each account (row-wise enrichment)
df['zscore'] = (df['amount'] - df.groupby('account')['amount'].transform('mean')) / df.groupby('account')['amount'].transform('std')
```

If you want, I can add a short exercises notebook demonstrating timings and replacement patterns for a realistic finance dataset.


Multiple aggregations and named outputs

```python
df.groupby('account').agg(
	total=('amount','sum'),
	avg=('amount','mean'),
	median=('amount','median')
)
```

Best practices
- Be explicit with aggregation names to avoid ambiguous column labels.
- Use `.pipe()` to make complex transformations composable and readable.
- Consider converting low-cardinality group keys to `category` dtype before groupby for speed.

Common mistakes
- Using `apply` for operations that can be expressed with `agg` or `transform` (performance hit).
- Assuming groupby preserves row order — sort if order matters after aggregation.

---

## Common transformation patterns

- `df.assign(new_col = df['col'] * 1.1)` — build new columns cleanly.
- `df.drop(columns=[...])` — remove unused columns early to save memory.
- `df.pipe(func)` — pass DataFrame through small reusable functions for clarity.
- Use vectorized string/date/numeric methods: `.str`, `pd.to_numeric`, `pd.to_datetime`.

Example pipeline

```python
def clean_names(df):
	df = df.rename(columns=lambda c: c.strip().lower())
	return df

def to_numeric_amounts(df):
	df['amount'] = (df['amount'].astype(str)
					.str.replace(',$','', regex=True)
					.str.replace(',', '')
				   )
	df['amount'] = pd.to_numeric(df['amount'], errors='coerce')
	return df

df = (pd.read_csv('data.csv', parse_dates=['date'])
	  .pipe(clean_names)
	  .pipe(to_numeric_amounts)
	  .loc[lambda d: d['amount'].notna()]
)
```

Best practices
- Build small, testable functions for repeated transformation steps and use `.pipe()`.
- Prefer `pd.to_numeric(..., errors='coerce')` then check for `NaN` to find malformed inputs.

Common mistakes
- Overusing `apply`/Python loops for transformations that are vectorizable.
- Not handling `NaN` after coercion; remember to inspect `df.isna().sum()`.

---

## Validation checks after selection and transformation

- Compare totals before/after: `df['amount'].sum()` — assert equality (or allowable tolerance).
- Check record counts: `len(df)` before and after filters/merges.
- Use `assert` statements in scripts to fail fast when assumptions break.

Example quick checks

```python
assert not df['invoice'].isna().any(), 'Missing invoice ids'
before = left['amount'].sum()
after = merged['amount_a'].sum()  # check expected retention
```

---

## Small checklist for selection & transform (finance)
- Normalize and validate keys before merges
- Use `.loc` for assignment and avoid chained assignment
- Prefer `agg`/`transform` over `apply` when possible
- Use `indicator=True` and `validate=` in merges to detect issues early
- Convert monetary values to a consistent numeric representation (consider integer cents)
- Keep intermediate results small: drop unused columns and convert to `category` where appropriate

---

References
- pandas docs: https://pandas.pydata.org/docs/
- Performance tips: pandas cookbook and "Effective Pandas" articles


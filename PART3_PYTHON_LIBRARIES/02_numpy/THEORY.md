# NumPy — Theory and Best Practices

Purpose: Quick reference for numerical computing needs in finance: arrays, vectorized math, and performance-sensitive operations.

## Overview
- NumPy provides `ndarray` for homogeneous typed arrays and fast vectorized operations.
- Use NumPy when doing heavy numeric computations, simulations, or when you need element-wise fast operations.

## Core Concepts
- `np.array([...], dtype=np.float64)` — explicit dtype is important for memory and speed
- Broadcasting — operations between arrays of compatible shapes
- Vectorized operations — avoid Python loops for element-wise math
- Common functions: `np.sum`, `np.mean`, `np.std`, `np.nanmean`, `np.where`, `np.isfinite`

### Deep dive — `np.where` (conditional selection)

`np.where(condition, x, y)` is a vectorized conditional operator: for each element, if `condition` is True return `x` else `y`.

When to use
- Efficient element-wise selection or conditional assignment on NumPy arrays or pandas `Series`/`ndarray` views.
- Replace element-wise `if/else` logic across an array without Python loops.

Examples

```python
import numpy as np

arr = np.array([100, -5, 200, 0])
# simple conditional: keep positives, else 0
clean = np.where(arr > 0, arr, 0)

# conditional between two arrays
fees = np.array([1,2,1,3])
net = np.where(arr > 0, arr - fees, arr)
```

Using with pandas Series

```python
import pandas as pd
df = pd.DataFrame({'amount': [100, -5, 200, None], 'currency': ['USD','USD','EUR','USD']})

# keep amounts when positive, otherwise 0 (np.where returns ndarray)
df['clean_amount'] = np.where(df['amount'].gt(0), df['amount'], 0)

# prefer: use mask/fillna or .loc for clearer pandas semantics
df['clean_amount2'] = df['amount'].where(df['amount'].gt(0), other=0)
```

Notes and best practices
- `np.where` returns a NumPy ndarray; when used on a pandas Series it will drop the index/metadata. Use `pd.Series(np.where(...), index=series.index)` if you need to preserve the index explicitly, or prefer `Series.where`/`Series.mask` which preserve metadata.
- For multiple mutually-exclusive conditions, prefer `np.select(conditions, choices, default=...)` rather than nested `np.where` for readability.
- For assignment in pandas, using `.loc` is often clearer and avoids chained-assignment warnings: `df.loc[cond, 'col'] = value`.
- Beware of dtype coercion: mixing numeric and string choices will upcast result to object dtype.

Alternatives
- `pd.Series.where(cond, other)` — keeps original values where `cond` is True, replaces where False; preserves index and dtype when possible.
- `pd.Series.mask(cond, other)` — inverse of `where` (replace where True).
- `np.select` — vectorized multi-condition selection.

Performance
- `np.where` is fast for pure NumPy arrays and large Series when you don't need pandas index preservation; it's usually faster than `apply` or Python loops.
- Prefer built-in Series operations (e.g., `.fillna`, `.clip`, `.astype`) when they express the intent and avoid dtype surprises.

Pitfalls
- Using `np.where` on mixed-type Series and expecting numeric dtype can lead to object dtype and slower downstream operations.
- Forgetting to preserve index when creating a Series from `np.where` results: alignment issues when merging back to a DataFrame.


Best practices
- Prefer `np.asarray()` to convert lists to arrays without copies when possible.
- Use `dtype` that suits precision and memory (e.g., `float32` vs `float64`) based on data needs.
- Use `np.where` and boolean masks instead of Python conditionals for arrays.
- Preallocate arrays when building large results to avoid repeated reallocations.

Common mistakes
- Mixing dtypes leading to unexpected upcasting (e.g., ints + floats -> float)
- Shape mismatches when broadcasting — check `arr.shape` carefully
- Using Python lists inside NumPy operations leading to object-dtype arrays and poor performance
- Relying on equality comparisons with floats (`==`) without tolerances

## Interoperability with pandas
- Use `df.to_numpy()` or `df['col'].to_numpy()` for conversions when numerical speed is needed
- Avoid round-tripping large arrays to DataFrame repeatedly; minimize conversions

## Typical finance uses
- Vectorized currency conversion and scaling
- Fast statistical summaries and simulation inputs
- Calculations on large time-series arrays when pandas overhead is not needed

References
- NumPy docs: https://numpy.org/doc/
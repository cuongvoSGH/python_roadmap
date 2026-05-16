# Windows Python Roadmap for Finance and Accounting Students

This guide is designed for students who are new to coding, have basic Excel experience, and want to learn Python on Windows for finance, accounting, and data reconciliation work.

## Part 1: Python setup and workflow

This section introduces the concepts you need to begin using Python on Windows. Detailed step-by-step guidance is available in separate files.

- Learn what Python is and why it is useful for finance and accounting.
- Install Python on Windows and verify `python` and `pip` from Command Prompt.
- Choose an editor such as Visual Studio Code, PyCharm, or Jupyter Notebook.
- Create and run Python scripts using `.py` files.
- Use the Python interactive prompt for quick commands.
- Install packages with `pip` and manage dependencies with virtual environments.

See the separate guides for full details:
- [Part 1: Python Setup and Workflow](PART1_PYTHON_SETUP.md)
- [Part 1 Additional Guide: Pip, Python Files, and Common Errors](PART1_PYTHON_WORKFLOW.md)

## Part 2: Python syntax and coding techniques

This section covers the fundamentals of Python programming with 8 subsections, each with theory material and hands-on Jupyter notebook exercises.

**Complete Part 2 Guide:**
- **Index:** [PART2_PYTHON_SYNTAX/INDEX.md](PART2_PYTHON_SYNTAX/INDEX.md)

### Part 2 Subsections

1. **Basic Syntax and Values** — Variables, comments, and output
2. **Core Data Types** — Integers, floats, strings, booleans, type conversion
3. **Control Flow** — If, elif, else, and decision-making
4. **Loops** — For and while loops, break, continue
5. **Data Structures** — Lists, tuples, dictionaries, sets
6. **Operations** — Indexing, slicing, membership tests
7. **Functions and Modules** — Defining and using functions, importing modules
8. **Practical Techniques** — List comprehensions, error handling, file I/O

Each subsection includes:
- **THEORY.md** — Comprehensive explanation with best practices and finance examples
- **Exercises.ipynb** — Jupyter notebook with runnable examples and practice tasks

### Excel-friendly analogy
- Lists are like rows in a column.
- Dictionaries are like Excel records with column names.
- Loops are like copying formulas down rows.
- Functions are like reusable formulas.

## Part 3: Finance and accounting Python libraries

### pandas for data work
- Read CSV or Excel:
  - `pd.read_csv("data.csv")`
  - `pd.read_excel("data.xlsx")`
- Basic operations:
  - `df.head()`, `df.info()`, `df.describe()`
- Filter rows:
  - `df[df["amount"] > 0]`
- Merge data:
  - `pd.merge(df1, df2, on="invoice")`
- Group and summarize:
  - `df.groupby("category")["amount"].sum()`
- Handle missing values:
  - `df.dropna()`, `df.fillna(0)`

### numpy for numeric operations
- Create arrays:
  - `np.array([100, 200, 300])`
- Vectorized math:
  - `arr * 1.1`
- Use NumPy when working with large numeric datasets and performance matters.

### Visualization
- `matplotlib` for basic charts:
  - Line chart, bar chart, histogram
- `seaborn` for improved chart styles and financial summarization
- Example:
  ```python
  import matplotlib.pyplot as plt
  df["amount"].plot(kind="bar")
  plt.show()
  ```

### Excel integration
- Read Excel with pandas:
  - `pd.read_excel("transactions.xlsx")`
- Save results back to Excel:
  - `df.to_excel("cleaned.xlsx", index=False)`
- Use `openpyxl` for advanced Excel formatting if needed.

### Finance/accounting workflows
- Load raw transaction data
- Clean and standardize column names and values
- Find duplicates or missing amounts
- Reconcile ledgers by comparing two tables
- Validate sums and report exceptions
- Export cleaned reconciliation results

### Example reconciliation tasks
- Compare two reports:
  - `merged = pd.merge(report_a, report_b, on="invoice", how="outer", indicator=True)`
- Identify mismatched values
- Create summary totals by account or category

## How to use this roadmap
1. Start with Part 1 to set up Python and your Windows environment.
2. Work through Part 2 examples until you can write small scripts.
3. Use Part 3 to apply Python to finance and accounting data tasks.
4. Practice by loading Excel/CSV files and performing reconciliation exercises.

## Next steps
- Build small projects like invoice matching, expense summaries, or cash flow charts.
- Keep examples simple and relate them to Excel concepts.
- Use this guide as a reference while practicing with real financial data.

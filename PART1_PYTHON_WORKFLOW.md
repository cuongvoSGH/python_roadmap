# Part 1 Additional Guide: Pip, Python Files, and Common Errors

This file explains how to install and manage packages with `pip`, how to work with Python files on Windows, and how to handle common installation and execution errors.

## Using pip on Windows

### What is `pip`?
- `pip` is the Python package manager.
- It installs additional libraries that Python does not include by default.
- For finance and accounting work, `pip` installs packages like `pandas`, `numpy`, `matplotlib`, and `openpyxl`.

### Common pip commands

1. Open Command Prompt.
2. Install a package:
   - `pip install pandas`
3. Install multiple packages:
   - `pip install pandas numpy matplotlib openpyxl`
4. See installed packages:
   - `pip list`
5. Find package information:
   - `pip show pandas`
6. Upgrade a package:
   - `pip install --upgrade pandas`
7. Uninstall a package:
   - `pip uninstall pandas`

### When to use `python -m pip`
- If `pip` gives an error, use:
  - `python -m pip install pandas`
- This ensures the package installs with the same Python version you are using.

## Working with Python files

### Creating a Python script
1. Open a text editor or VS Code.
2. Create a new file.
3. Save it with the `.py` extension, for example `my_script.py`.
4. Put Python code inside the file.

Example file content:
```python
amount = 100
print("Amount:", amount)
```

### Running a Python file
1. Open Command Prompt.
2. Use `cd` to go to the folder containing your `.py` file.
   - Example: `cd C:\Users\YourName\Documents\python_roadmap`
3. Run the script:
   - `python my_script.py`
4. The output appears in the terminal.

### Using a Python file with VS Code
1. Open the folder in VS Code.
2. Open your `.py` file.
3. Select the Python interpreter from the lower-right status bar.
4. Use the Run button or open a terminal and run `python my_script.py`.

### Passing a file path or arguments
- You can also use command-line arguments in Python:
  - `python my_script.py input.csv`
- In your script, use `sys.argv` to read these values.

## Working with Jupyter Notebook
### Install Jupyter Notebook or Lab
- Install in your Python environment:
  - `pip install notebook`
  - or `pip install jupyterlab`
- In VS Code, install the **Jupyter** extension if it is not already installed.

### Create and open notebooks
1. In VS Code, create a new file and save it with the `.ipynb` extension.
2. Open the notebook file and use the interactive notebook interface.
3. Each notebook contains cells. Cells can be code or markdown.
- Code cells run Python code.
- Markdown cells hold text, headings, and instructions.

### Running notebook cells
1. Select a cell and press the Run button.
2. In a code cell, the output appears directly below the cell.
3. Use `Shift+Enter` to run the current cell and move to the next one.
4. Use `Ctrl+Enter` to run the current cell and stay on it.

### Notebook workflow tips
- Keep your notebook saved often with `Ctrl+S`.
- Use markdown cells to explain each step and show headings.
- Restart the kernel and rerun cells if results seem inconsistent.
- Use the variable explorer or `print(df.head())` in a code cell to inspect data.

### When to use notebooks
- Notebooks are great for data exploration, examples, and step-by-step analysis.
- Use `.py` scripts for repeatable automation or production tasks.

## Common errors when installing Python

### 1. `python` is not recognized as an internal or external command
- Cause: Python was not added to PATH during installation.
- Fix: Reinstall Python and check **Add Python to PATH**, or add the Python install folder to PATH manually.

### 2. `pip` is not recognized
- Cause: `pip` is missing from PATH or Python installation.
- Fix: Run `python -m ensurepip --upgrade` or reinstall Python.
- Then use `python -m pip install package`.

### 3. Wrong Python version used
- Cause: Multiple Python versions are installed.
- Fix: Use the exact version command:
  - `python3 --version`
  - `py --version`
  - `py -3 script.py`
- Or set the correct interpreter in VS Code.

### 4. Permission denied or access errors
- Cause: You do not have write permission in the install folder.
- Fix: Run Command Prompt as Administrator, or use a virtual environment.

## Common errors when running Python scripts

### 1. `SyntaxError`
- Cause: The code has a typo or missing punctuation.
- Example: forgetting a closing parenthesis.
- Fix: Read the error message and correct the line.

### 2. `IndentationError`
- Cause: Incorrect spacing in code blocks.
- Fix: Use 4 spaces per indent and avoid mixing tabs and spaces.

### 3. `ModuleNotFoundError`
- Cause: A package is not installed or the wrong environment is active.
- Fix: Install the package with `pip install package` or activate the correct virtual environment.

### 4. `FileNotFoundError`
- Cause: The script tries to open a file that does not exist or has the wrong path.
- Fix: Check the file name and path. Use absolute paths or place files in the same folder.

### 5. `ValueError` when converting data
- Cause: Trying to convert text that is not a number.
- Example: `int("abc")`
- Fix: Validate or clean input before conversion.

## Tips for safer setup and execution

- Always save your `.py` file before running it.
- Keep code files in one project folder.
- Use `python -m venv venv` to isolate dependencies.
- Activate the virtual environment before installing packages.
- If you see an error, read it carefully and fix the first line shown.

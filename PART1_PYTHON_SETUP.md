# Part 1: Python Setup and Workflow (Windows)

This file contains the step-by-step theoretical material for learners who are new to programming and want to use Python on Windows for finance and accounting tasks.

## Step 1: Understand what Python is

1. Python is a programming language used to tell a computer what to do.
2. It is interpreted, which means you can run commands directly without compiling first.
3. Python is known for clear and readable code, making it friendly for beginners.
4. In finance and accounting, Python helps automate routine work, clean data, compare reports, and create charts.

## Step 2: Download and install Python on Windows

1. Open your web browser and go to: https://python.org/downloads/
2. Click the latest Windows download.
3. Run the installer file when it finishes downloading.
4. In the installer window, check the box: **Add Python to PATH**.
5. Click **Install Now**.
6. Wait for the installer to finish and then click **Close**.

## Step 3: Verify Python installed correctly

1. Open the Windows search bar and type `cmd`.
2. Press Enter to open Command Prompt.
3. Type `python --version` and press Enter.
   - You should see a version number like `Python 3.11.0`.
4. Type `pip --version` and press Enter.
   - This confirms Python can install packages.

## Step 4: Choose an editor or IDE

1. For learners, the best choice is **Visual Studio Code**.
2. VS Code is free and works well on Windows.
3. Alternatives:
   - **PyCharm** (full Python IDE)
   - **Jupyter Notebook/Lab** (good for data and reports)
4. Use an editor that shows code clearly and makes it easy to open files.

## Step 5: Create and run your first Python file

1. Open VS Code or Notepad.
2. Create a new file and save it as `example.py`.
3. Type the following into the file:
   ```python
   print("Hello, Python")
   ```
4. Save the file.
5. Open Command Prompt and navigate to the folder where you saved `example.py`.
   - Use `cd` to change folders, for example:
     - `cd C:\Users\YourName\Documents\python_roadmap`
6. Run the file with:
   - `python example.py`
7. You should see `Hello, Python` printed in the Command Prompt.

## Step 6: Use the Python interactive mode

1. In Command Prompt, type `python` and press Enter.
2. You will enter the Python prompt, which looks like `>>>`.
3. Type a simple command like:
   - `print("Hello")`
4. Press Enter and see the result immediately.
5. To exit interactive mode, type `exit()` or press `Ctrl+Z` then Enter.

## Step 7: Install Python packages with pip

1. `pip` is the tool Python uses to add extra functionality.
2. Open Command Prompt.
3. Install a package, for example:
   - `pip install pandas`
4. Install several useful finance packages at once:
   - `pip install pandas numpy matplotlib openpyxl`
5. Check installed packages:
   - `pip list`
6. Upgrade a package:
   - `pip install --upgrade pandas`

## Step 8: Use a virtual environment on Windows (recommended)

1. A virtual environment keeps your project files and packages separate.
2. Create one with:
   - `python -m venv venv`
3. Activate it with:
   - `venv\Scripts\activate`
4. When active, install packages just for this project:
   - `pip install pandas numpy matplotlib openpyxl`
5. Run Python as usual while the environment is active.
6. Deactivate it when finished:
   - `deactivate`

## Step 9: Important Windows tips

- Use Command Prompt or PowerShell for Python commands.
- If `python` does not work, make sure the installer added Python to PATH.
- Use `python -m pip install package` if `pip install package` gives an error.
- Keep your code files in one folder for easy access.

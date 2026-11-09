# Python environment for the notebooks

These notebooks run in a project-local Python environment. In VS Code, the
notebook's selected kernel must be that environment, not the uv-managed base
Python installation.

## Set up the environment on Windows

Open the repository folder in VS Code, then open a PowerShell terminal at the
repository root. Create a virtual environment if `.venv` does not already
exist:

```powershell
py -m venv .venv
```

Install the packages used by the Training and Testing notebook:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install ipykernel pandas scikit-learn
```

The package is named `ipykernel` (not `ipykernal`). `scikit-learn` is installed
under that name, but imported in Python as `sklearn`.

If `py` is unavailable, create the environment from VS Code with **Python:
Create Environment**, choose a Python interpreter, and create a `.venv` in
the repository. Then run the two install commands above.

## Select the notebook kernel

In the notebook toolbar, select **Select Kernel** and choose the Python
environment under this repository's `.venv` folder. If it does not appear,
close and reopen the notebook or use **Select Another Kernel** to browse to:

```text
.venv\Scripts\python.exe
```

After changing the kernel, restart it and run the notebook cells from the top.

## Common errors

- **`requires the ipykernel package`**: install `ipykernel` in `.venv` using
  the command above, then select `.venv` as the notebook kernel.
- **`externally-managed-environment`**: pip was run against a uv-managed base
  interpreter. Do not bypass this protection with `--break-system-packages`;
  use `.venv\Scripts\python.exe -m pip` so packages are installed in the
  project environment.
- **`No matching distribution found for ipykernal`**: correct the typo to
  `ipykernel`.
- **`No module named 'pandas'` or `No module named 'sklearn'`**: install
  `pandas` or `scikit-learn` into `.venv`, and confirm the notebook is using
  that environment.
- **`FileNotFoundError` for `data/wine.csv`**: the file is in
  `Assignment 2.1-Training and Testing\data\wine.csv`. Run the notebook with
  that assignment folder as its working directory, or adjust the relative
  path to match the notebook's working directory.

## Check the environment

Run this in PowerShell from the repository root to verify the interpreter and
the packages needed by the assignment:

```powershell
.\.venv\Scripts\python.exe -c "import sys, ipykernel, pandas, sklearn; print(sys.executable); print('ipykernel', ipykernel.__version__); print('pandas', pandas.__version__); print('scikit-learn', sklearn.__version__)"
```

The project environment was verified with Python 3.15.2, `ipykernel` 7.4.0,
and pandas 3.1.1. If pip cannot install a package for the selected Python
version, create `.venv` with a Python version supported by that package and
repeat the install steps.

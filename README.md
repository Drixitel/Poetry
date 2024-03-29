# Poetry Install (VM)

Note:

- when using a VM all previous packages are not included and must be installed
- VSCode will also need extensions specifc to the VM
  - local extansions are not transfered
  - Certain extensions are needed so VSCode can locate project interpreters

### Extensions used in WSL:

- Black Formatter
- C/C++
- C/C++ extension pack
- CMake
- CMake Tools
- Jupyter
- Jupyter Notebook Renderers
- Pylance
- Python
- C/C++ Themes
- Jupyter Keymap
- Better TOML

### Install:

1.  See install instructions in documentation (curl) for WSL/windows
2.  To add poetry to path `restart` the terminal
3.  Update poetry configurations to have the environments in local projects
4.  Ensure `python3.9` is used in the interpreter

# Creating a Project

- The project does not create an environment folder. See that section.

1. Create a folder in File Explorer

2. Use Command:
   - `poetry new FileProjectname`
3. Generates the following:
   - `FileProjectname folder`
     - Should keep `Helperfiles` in folder where `.toml` files are located or use a `scr` folder to keep `Helperfiles`
     - `.toml` File
       - Contains a list of packages
     - `README.rst` File
     - Folder with `__init__.py`
       - Should contain project files
     - Tests Folder
       - This can be deleted.

# Create an Enviorment (`.venv`)

- host all the packages you'd like e.g.: numpy, jupyterlab, matplotlib, astropy, etc.
- This is not a folder used to make any edits or save any files
- Used to find `interpreters/ kernels`
  - Python

1. Generate
   - `poetry install`
   - This will reveal the `.venv` file in your project folder. If not, see `in-project`

## Genertate Environment in-project

If `.venv` file is generated but not an in-project file:

1. find it:

   - `poetry env info`

2. delete it and continue with these steps.

3. View config

   - `poetry config --list`

4. use command

   - `poetry config virtualenvs.in-project true`

5. Check for True:

   - `virtualenvs.in-project = true`

6. Now, `poetry install` should produce a `.venv` file in your project folder

# Add Package to project

- Works once `.venv` is present in the directory
- Call:
  - `poetry add packagename`
- Note: \* `poetry add packagename` = `pip install packagename` in poetry's virtual environment
  > Packages added only work within the working folder. They do not carry into another folder (unless it is a subfolder)

> See `pyproject.toml` to find versions of packages

## Issue Adding a Package to Project

- If adding fails and reverts back to the original, an older package might be interfering

1. Delete the `.venv` environment file/folder
2. Use: `poetry add` to add the needed package
   > this will add the new package and add the remaining ones similar to `poetry install`

# Clone Git project and pull Poetry Project

1. Have poetry installed<br>
2. Clone repo
3. Call: `poetry install`<br>
   - this creates an identical environment on a new machine (pulls all needed packages)

# Select Python Interpreter

- Add path from `.venv > scripts` or `.venv> bin` locate `python.exe` or `python(version).exe` and use this path for your interpreter.
- interpreters or Kernels (same thing) must be from your `.venv` file to function properly
  > May resolve issues with added packages

# Run program from Terminal

1. Terminal must be in the `.toml` file
2. Call: `poetry run python Filename.py`

# Working inside a Poetry Folder

> Always work within the file that contains your `.toml` file or any sub-directory within it

- If creating a `Helper.py` file to pull from and use in notebooks:

1. Keep this file in:
   - The folder with `.toml` OR
   - Create `src` folder in the folder holding `.toml` and pull this in using:
     - `import src.Helper`

# Poetry update Python (Newer Version)

- Change `.toml` file
- Save
- run `poetry lock --no-update`
- Delete `.venv` file
- `poetry install` (this reinstalls the `.venv`)
- Last performed 6/16/22: Worked fine

# Check your Python version in Poetry

> Commands:

- `poetry shell`
- `python --version`
- `exit`

# Using selfmade Modules 
Structure matters 
```
project/
  helperfiles/
      __init__.py
  scripts/
      __init__.py
  tests/
      __init__.py
      subdir/
          __init__.py
  poetry.lock
  pyproject.toml
  README.md 
```

Each subdirectory needs an `__init__.py` file, and each directory in the root directory needs to be added to your `.toml` file. 

```toml
[tool.poetry]
name = "project"
version = "0.1.0"
description = ""
authors = ["Drixitel"]
readme = "README.md"
packages = [
    { include = "scripts" },
    { include = "helper_files" },
    { include = "tests" },
]
```
With this inclusion, you'll be able to pull any module from the self-made packages.


# Issues with Jupyter

- Ensure extensions are added to the new VM (if using one)
- use `poetry add`:
  - jupyterlab notebook jupyter

# Pylance Issue

- This can happen because the interpreter is not correctly selected

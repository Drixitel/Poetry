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
3.  Update poetry configurations to have the enviornments in local projects
4.  Ensure `python3.9` is used in the interpreter

# Creating a Project

- The project does not create an enviorment see that section.

1. Create a folder in file explorer

2. Use Command:
   - `poetry new FileProjectname`
3. Generates the following:
   - `FileProjectname folder`
     - Should keep `Helperfiles` in folder where `.toml` fils is located or use a `scr` folder to keep `Helperfiles`
     - `.toml` File
       - Contains list of packages
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
   - This will reveal the `.venv` file in your project folder. If not see `in-project`

## Genertate Environment in-project

If `.venv` file generated but not in-project file:

1. find it:

   - `poetry env info`

2. delete it and continue with these steps.

3. View config

   - `poetry config --list`

4. use command

   - `poetry config virtualenvs.in-project true`

5. Check for True:

   - `virtualenvs.in-project = true`

6. Now `poetry install` should produce a `.venv` file in your project folder

# Add Package to project

- Works once `.venv` is present in file
- Call:
  - `poetry add packagename`
- Note: \* `poetry add packagename` = `pip install packagename` in poetry's virtual environment
  > Packages added only work within the working folder they do not carry into another folder (unless it is a subfolder)

> See `pyproject.toml` to find versions of packages

## Issue Adding a Package to Project

- If adding fails and reverts back to original an older package might be interfering

1. Delete the `.venv` enviorment file/folder
2. Use: `poetry add` to add the needed packagee
   > this will add the new package and add the remaining ones similar to `poetry install`

# Clone Git project and pull Poetry Project

1. Have poetry installed<br>
2. Clone repo
3. Call: `poetry install`<br>
   - this creates an identical enviorment on new machine (pulls all needed packages)

# Select Python Interpreter

- Add path from `.venv > scripts` or `.venv> bin` locate `python.exe` or `python(version).exe` and use this path for your interpreter.
- interpreters, or Kernels (same thing) must be from your `.venv` file to function properly
  > May resolve issues with added packages

# Run program from Terminal

1. Terminal must be in the `.toml` file
2. Call: `poetry run python Filename.py`

# Working inside a Poetry Folder

> Always work within the file that contains your `.toml` file or any sub directory within it

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
- Last preformed 6/16/22: Worked fine

# Check your python version in Poetry

> Commands:

- `poetry shell`
- `python --version`
- `exit`

# Issues with Jupyter

- Ensure extensions are added to new VM (if using one)
- use `poetry add`:
  - jupyterlab notebook jupyter

# Pylance Issue

- This can happen becuase the interpreter is not correctly selected

# Poetry Environment Notes & Set-Up
System: WSL Ubuntu distro & Python3.11

## Environment In-Project Set-Up

1. `poetry new <project name>`
2. Check configs with:  `poetry config --list` & verify the following is set to true, if not, run the following commands: 
	1. `poetry config virtualenvs.in-project true`
	2. `poetry config virtualenvs.prefer-active-python true
3. Install : `poetry install` 
	1. generates `.venv` directory
4. Add dependencies : `poetry add <package>`
	1. see `toml` file to view list 
5. Update : `poetry update`

TLDR; 
```bash
poetry new <project name> 
poetry config --list 

poetry config virtualenvs.in-project true
poetry config virtualenvs.prefer-active-python true

poetry install

poetry add <package1> <package2> ... <packageN>

poetry update
```

## Run Program from Terminal 
```bash
poetry run python <filename.py>
```

## Jupyter 
Dependencies 
- `poetry add <...>`
```toml
python = ">=3.11,<4.0"
jupyterlab = "^4.4.7"
notebook = "^7.4.5"
jupyter = "^1.1.1"
tensorflow = "^2.20.0"
matplotlib = "^3.10.6"
ipykernel = "^6.30.1"
```

Kernel 
```python
poetry env info --path # view interpreter 

source your-poetry-venv/bin/activate` #I can't remember if this worked'

poetry run ipython kernel --name "your-new-poetry-env-name" --user # create kernel 

```
## Updating Python 
- Find online instructions on how to update python 
- In .bashrc 
```bash
alias python='/usr/bin/python3.11'
alias python3='/usr/bin/python3.11'
```
- In poetry 
```shell
poetry config virtualenvs.prefer-active-python true
```

### Python Version Check

```bash
poetry shell
python --version 
exti
```

## User Created Modules and How to add them 
Required File Structure 
```
project1/
  user-created-src/
      __init__.py
  project1/
      __init__.py
  tests/
      __init__.py
      subdir/
          __init__.py
  poetry.lock
  pyproject.toml
  README.md
```
Required `toml` structure 
```toml
[tool.poetry]
name = "project"
version = "0.1.0"
description = ""
authors = ["Drixitel"]
readme = "README.md"
packages = [
    { include = "user-created-src" },
    { include = "project1" },
    { include = "tests" },
]
```
# Common Issues
## Adding Package Issue  
- `poetry add <package>` fails 
	- delete `.venv` directory 
	- reattempt `poetry add <...>`
	- `poetry install` reinstalls packages; however, `poetry add <...>` does this and adds new packages 

## Pylance Issue
- This can happen because the interpreter is not correctly selected 

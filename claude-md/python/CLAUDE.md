# Python Project CLAUDE.MD File

## Python Package Management with uv

Use uv exclusively for Python package management in this project.

## Package Management Commands

- All Python dependencies **must be installed, synchronized, and locked** using uv
- Never use pip, pip-tools, poetry, or conda directly for dependency management

Use these commands:

- Install dependencies: `uv add <package>`
- Remove dependencies: `uv remove <package>`
- Sync environment: `uv sync`
- Lock dependencies: `uv lock`

## Running Python Code

- Run a Python script with `uv run <script-name>.py`
- Run Python tools with `uv run <tool>` (e.g. `uv run pytest`, `uv run ruff`, `uv run mypy`, `uv run pre-commit`)
- Launch a Python REPL with `uv run python`

--------------------------------

## Python Package Management with Poetry

Use Poetry exclusively for Python package management in this project.

## Package Management Commands

- All Python dependencies **must be installed, synchronized, and locked** using Poetry
- Never use pip, pip-tools, uv, or conda directly for dependency management

Use these commands:

- Install dependencies: `poetry add <package>`
- Remove dependencies: `poetry remove <package>`
- Sync environment: `poetry install`
- Lock dependencies: `poetry lock`

## Running Python Code

- Run a Python script with `poetry run python <script-name>.py`
- Run Python tools with `poetry run <tool>` (e.g. `poetry run pytest`, `poetry run ruff`, `poetry run mypy`, `poetry run pre-commit`)
- Launch a Python REPL with `poetry run python`

--------------------------------

## Python environment

This project's virtual environment lives at `.venv/`. Invoke its
interpreter directly; do not run `source .venv/bin/activate` (it cannot
persist between Claude's tool calls).

Use these commands:

- Run a script: `.venv/bin/python script.py`
- Open a REPL: `.venv/bin/python`
- Install a package: `.venv/bin/pip install <package>`
- Run a tool: `.venv/bin/pytest`, `.venv/bin/ruff check`,
  `.venv/bin/mypy`

Each entry under `.venv/bin/` resolves to the venv's copy of the tool,
so Python sees the project's `site-packages` automatically.


## Type Hints

- Use type hints everywhere.
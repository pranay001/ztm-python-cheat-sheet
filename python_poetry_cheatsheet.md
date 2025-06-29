# 🐍 Python Poetry Complete Cheat Sheet – With Detailed Explanations

Poetry is a powerful Python tool for dependency management and packaging. This cheat sheet will guide you from basic setup to advanced usage with clear explanations.

---

## 📆 1. Installing Poetry



### ✅ Recommended Installation

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

### 🔧 Alternative Installation (Using pip)

```bash
pip install poetry
```

Make sure your `~/.local/bin` (or appropriate bin path) is in your `PATH` if using pip.

### 🔍 Verify Installation

```bash
poetry --version
```

### 📝 Set In-Project Virtual Environments

After installation, it's recommended to enable in-project virtual environments:

```bash
poetry config virtualenvs.in-project true
```

This ensures a `.venv/` is created inside each project directory.

### 🔍 View Current Poetry Configuration

To verify the current configuration:

```bash
poetry config --list
```

### 📂 Check the Current Virtual Environment Info

To see where the virtual environment is located:

```bash
poetry env info
```

After installation, it's recommended to enable in-project virtual environments:

```bash
poetry config virtualenvs.in-project true
```

This ensures a `.venv/` is created inside each project directory.

```bash
poetry --version
```

---

## 📁 2. Creating or Initializing Projects

### Create a New Project

```bash
poetry new my_project
```

Creates a basic project structure.

### Create With `src/` Layout

```bash
poetry new --src my_project
```

Preferred for larger projects.

### Initialize in Existing Directory

```bash
poetry init
```

Interactive creation of `pyproject.toml`.

---

## 📂 3. Virtual Environment Management

### Create & Install

```bash
poetry install
```

Automatically creates a virtualenv and installs dependencies.

### Use the Virtual Environment

```bash
poetry run python script.py
```

Note: `poetry shell` is deprecated. Use `poetry run` for running commands within the virtual environment.

### Set `.venv` Inside Project

```bash
poetry config virtualenvs.in-project true
```

Creates `.venv/` in your project folder.

To apply this after an env already exists:

```bash
poetry env remove python
poetry install
```

---

## 📚 4. Managing Dependencies

### Add Runtime Dependency

```bash
poetry add requests
```

### Add Specific Version

```bash
poetry add numpy@^1.23.0
```

`^` allows all `>=1.23.0 <2.0.0`

### Add Dev Dependency

```bash
poetry add --dev black
```

### Remove Dependency

```bash
poetry remove requests
```

### View Dependency Tree

```bash
poetry show --tree
```

---

## 🎯 5. Version Constraints Explained

### `^` (Caret)

```bash
^1.2.3 → >=1.2.3 and <2.0.0
```

Allows compatible future updates.

### `~` (Tilde)

```bash
~1.2.3 → >=1.2.3 and <1.3.0
```

Allows patch-level updates only.

---

## 📜 6. `pyproject.toml` Overview

```toml
[tool.poetry]
name = "my_project"
version = "0.1.0"
description = "..."

[tool.poetry.dependencies]
python = "^3.11"
requests = "^2.31.0"

[tool.poetry.dev-dependencies]
pytest = "^7.4.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

---

## 🔐 7. `poetry.lock` File

- Records **exact versions** of all dependencies (direct and transitive)
- Ensures **reproducibility** across machines
- Committed to version control

### Regenerate Lock File

```bash
poetry lock
```

### Update Dependencies

```bash
poetry update
```

---

## 🚀 8. Building and Publishing

### Build Package

```bash
poetry build
```

Creates `.whl` and `.tar.gz` in `dist/`

### Publish to PyPI

```bash
poetry config pypi-token.pypi <TOKEN>
poetry publish --build
```

---

## 🧪 9. Testing With Poetry

### Add Testing Tools

```bash
poetry add --dev pytest pytest-cov
```

### Run Tests

```bash
poetry run pytest
```

---

## ⚙️ 10. Configuration Tips

### View Config

```bash
poetry config --list
```

### Set Local `.venv`

```bash
poetry config virtualenvs.in-project true
```

---

## 🧼 11. Useful Commands

```bash
poetry install               # Install all dependencies
poetry shell                 # Activate shell
poetry run <cmd>             # Run a command in venv
poetry add <package>         # Add dependency
poetry add --dev <package>   # Add dev dependency
poetry remove <package>      # Remove dependency
poetry show --tree           # View full dependency tree
poetry env info              # Get virtualenv info
poetry env remove python     # Remove existing env
```

---

## ✅ 12. Typical Workflow

```bash
poetry new my_project
cd my_project
poetry add requests
poetry add --dev pytest
poetry install
poetry run pytest
poetry build
poetry publish
```

---

## 🛠️ 14. Troubleshooting Guide

### ❌ Issue: `poetry install` fails with missing `README.md`

**Error:** `Readme path 'README.md' does not exist.`

**Solution:** Either create a `README.md` file in the project root, or disable packaging mode:

```bash
poetry config package-mode false --local
```

Or run install without installing the root project:

```bash
poetry install --no-root
```

---

### ❌ Issue: `.venv` not created in project directory

**Solution:**

1. Ensure this setting is enabled:
   ```bash
   poetry config virtualenvs.in-project true
   ```
2. Remove old env:
   ```bash
   poetry env remove python
   ```
3. Reinstall:
   ```bash
   poetry install
   ```

---

### ❌ Issue: Poetry not found after `pip install poetry`

**Solution:** Add the Poetry binary path to your shell:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Or check where it was installed:

```bash
which poetry
```

---

## 📁 13. Key Files/Folders

| File / Folder    | Description                               |
| ---------------- | ----------------------------------------- |
| `pyproject.toml` | Project metadata and dependencies         |
| `poetry.lock`    | Resolved, locked dependency versions      |
| `.venv/`         | Local virtual environment (if configured) |
| `dist/`          | Build artifacts for publishing            |


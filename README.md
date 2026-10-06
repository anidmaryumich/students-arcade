# Students Arcade

## What is Students Arcade?
Students Arcade is a showcase of small Python activities ("plugins") written by students. A single launcher, `main.py`, finds every plugin in the `plugins/` folder, runs it, and prints the result.

## Requirements
- Python 3
- No external packages; the launcher and plugins use only the Python standard library.

## How to run
From the repository root:

```bash
python main.py
```

The launcher prints a `PLUGIN RUNNER` header, then, for each plugin, a line in the form `APP_NAME by AUTHOR` followed by the value returned by its `run()` function. It ends with a summary such as `Ran 3 plugin(s).`

## How plugins are discovered
`main.py` looks for Python modules in the `plugins/` folder:

- Every module in `plugins/` is discovered automatically; no registration is needed.
- Modules whose names start with an underscore (for example, `_helpers.py`) are ignored.
- Each module is imported as `plugins.<name>`. If the import fails, the launcher prints `[skipped] plugins/<name>.py failed to import: <error>` and continues with the next plugin.
- Importing a module runs its top-level code, so a plugin should only define values and functions at the top level and do its work inside `run()`.

## Required plugin interface
Every plugin should define:

| Name | Type | Purpose |
|---|---|---|
| `AUTHOR` | string | The student's name. If missing, the launcher shows `Unknown author`. |
| `APP_NAME` | string | The activity's display name. If missing, the launcher shows the module name. |
| `run()` | function | Does the activity and returns a readable result, which the launcher prints. |

Launcher behavior:
- If `run()` is missing, the plugin is reported as `[skipped] no run() function defined`.
- If `run()` raises an exception, the launcher prints `[error] run() raised: <error>` and continues.
- Only plugins whose `run()` completes are counted in the final `Ran N plugin(s).` line.

## Example plugin
Save as `plugins/hello_arcade.py`:

```python
import random

AUTHOR = "Your Name"
APP_NAME = "Hello Arcade"


def run():
    greeting = random.choice(["Hello", "Hi", "Welcome"])
    return f"{APP_NAME}: {greeting} from the Students Arcade!"
```

Use a unique, lowercase filename with underscores (for example, `dice_roller.py`) so it is a valid Python module name and does not overwrite another student's plugin.

## How to contribute
1. **Pick an issue** in the repository's Issues tab and claim it with a comment.
2. **Fork** `AmalChUm/students-arcade` to your own GitHub account.
3. **Clone your fork** (not the original) with GitHub Desktop or SourceTree.
4. **Create a feature branch** from `main`, named `feature/issue-NUMBER-short-name`.
5. **Make your change** (for example, add a plugin in `plugins/`).
6. **Run `python main.py`** and confirm your plugin is discovered and its output is readable.
7. **Commit** focused changes with clear messages (for example, `Add dice roller plugin structure`).
8. **Publish the branch** to your fork.
9. **Open a pull request** with base `AmalChUm/students-arcade` / `main` and compare `your-fork` / `your-feature-branch`. Include `Closes #NUMBER`, the files changed, and how you verified the change.

## Contribution rules
- Keep each pull request focused on one issue.
- Use only the Python standard library.
- Do not modify `main.py` unless your issue concerns the launcher.
- Do not modify another student's plugin unless the issue authorizes it.
- Do not commit passwords, API keys, tokens, or private information.
- Preserve the MIT license and existing attribution.


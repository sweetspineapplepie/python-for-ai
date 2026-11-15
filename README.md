# Python for AI

A beginner-friendly workspace for learning Python skills used in data analysis and AI projects. The repository currently contains small examples of Python classes, environment variables, HTTP requests, tabular data, plotting, and CSV/JSON/Excel file handling. It is a learning project in progress; it does not yet contain Jupyter notebook files or an AI model implementation.

## Project contents

| Path | Description |
| --- | --- |
| `hello.py` | Examples of classes, positional and keyword arguments, methods, validation, and loading values from a `.env` file. |
| `get_data.py` | Fetches recent weather data for Malang from the Open-Meteo API, creates a chart, and writes a CSV file. Requires an internet connection when run. |
| `sales-analysis/analyzer.py` | Reads `sales-analysis/data/sales.csv`, calculates sales totals, and writes JSON, Excel, and CSV output files. |
| `sales-analysis/helpers.py` | Helper functions for calculating totals and formatting currency. |
| `src/python_for_ai/` | The installable Python package scaffold and its `python-for-ai` command. |
| `pyproject.toml`, `uv.lock` | Project metadata, dependencies, and the locked dependency versions used by `uv`. |

## Requirements

- Git
- [`uv`](https://docs.astral.sh/uv/) for Python version and dependency management
- Python 3.15 or newer, as configured in `pyproject.toml`
- Internet access to install dependencies and run `get_data.py`

`uv` can install and manage the required Python version for you. If Python 3.15 is not available for your operating system yet, install a supported version that satisfies the project requirement before syncing.

## Setup

Clone the repository, then enter its directory (replace the URL with the repository's actual clone URL):

```bash
git clone <repository-url>
cd python-for-ai
```

### Install `uv` if needed

Check whether it is already installed:

```bash
uv --version
```

If your shell reports that `uv` is not found, install it using one of these methods.

**macOS** (Homebrew):

```bash
brew install uv
```

Or use the official installer on macOS or Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows** (PowerShell):

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

After installation, open a new terminal if `uv` is not immediately available, then check `uv --version` again. See the [official uv installation guide](https://docs.astral.sh/uv/getting-started/installation/) for other installation options.

### Install the project environment

From the repository root, run:

```bash
uv sync
```

`uv sync` creates the local `.venv` environment and installs the project dependencies from `pyproject.toml` and `uv.lock`. `uv` can also download the configured Python version if it is available. Run project commands with `uv run`; activating the environment manually is not required.

## Run the examples

Run a Python file from the repository root:

```bash
uv run python hello.py
uv run python get_data.py
```

The sales analysis uses paths relative to its own directory. Run it from `sales-analysis/` while pointing `uv` to the root project:

```bash
cd sales-analysis
uv run --project .. python analyzer.py
```

The script writes generated files into `sales-analysis/output/`. The weather example writes its chart and CSV relative to the current working directory.

The package command is also available after syncing:

```bash
uv run python-for-ai
```

### Environment variables

`hello.py` loads a `.env` file using `python-dotenv` and prints `API_KEY` and `DEBUG` if provided. Create a local `.env` in the repository root if you want to try it:

```dotenv
API_KEY=your-local-value
DEBUG=true
```

Do not commit real secrets. `.env` is ignored by Git.

## Jupyter Notebook

There are currently no `.ipynb` notebooks in the repository. You can start Jupyter Notebook from the project root and create one for your experiments. Jupyter is not a permanent project dependency; this command asks `uv` to make it available for this run:

```bash
uv run --with jupyter jupyter notebook
```

Jupyter will print a local URL and usually open it in your browser. In its file browser, choose **New → Python 3 (ipykernel)** to create a notebook. Save notebooks in the repository (for example, under a new `notebooks/` directory). Stop the server with `Ctrl+C` in the terminal.

To use Jupyter repeatedly as part of this environment, add it as a development dependency once and sync:

```bash
uv add --dev jupyter
uv sync
uv run jupyter notebook
```

### Useful notebook shortcuts

Jupyter has two keyboard modes. Press `Esc` to enter **Command mode** (cell selected, blue outline) and `Enter` to enter **Edit mode** (cursor in a cell, green outline).

| Shortcut | Action |
| --- | --- |
| `Shift+Enter` | Run the current cell and select the next cell (or create one at the end). |
| `Ctrl+Enter` | Run the current cell and keep it selected. |
| `Alt+Enter` | Run the current cell and insert a new cell below. |
| `Esc`, then `A` | Insert a cell above. |
| `Esc`, then `B` | Insert a cell below. |
| `Esc`, then `M` | Change the selected cell to Markdown. |
| `Esc`, then `Y` | Change the selected cell to Code. |
| `Esc`, then `D`, `D` | Delete the selected cell (press `D` twice). |
| `Shift+Tab` (while editing a function call) | Show function help or parameter information. |

Shortcuts can vary slightly by Jupyter version and browser. Use **Help → Keyboard Shortcuts** in the notebook to see the shortcuts available in your session.

## Dependency notes

The project currently declares `ipykernel`, `matplotlib`, `numpy`, `pandas`, `python-dotenv`, and `requests`. The sales example also exports an Excel workbook, which may require an Excel writer such as `openpyxl`; if that step reports a missing writer, add it with `uv add openpyxl` and run `uv sync`.

## Contributing

This is a learning project. Improvements to examples, explanations, and exercises are welcome. Open an issue to report a problem or propose a topic, or submit a pull request with a focused change.

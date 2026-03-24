# Python 3.x Standalone Installation and VSCode Setup

This section outlines the steps to install Python 3.x independently of Anaconda, configure VSCode to use it for specific projects, and maintain compatibility with existing Anaconda environments.

---

## 1. Install Standalone Python 3.9

1. Download the installer from [Python.org](https://www.python.org/downloads/).

2. Run the installer with the following settings:

    - Check **Add Python 3.x to PATH**
    - Customize installation:
        - Keep `pip`
        - Install to `C:\Program Files\Python3x` (outside Anaconda)

## 2. Adjust PATH for Standalone Python

1. Open System Properties with `Win + R → sysdm.cpl → Enter → Advanced → Environment Variables`

2. Under System variables → Path:

    - Add (if missing):

    ```makefile
    C:\Program Files\Python3x\
    C:\Program Files\Python3x\Scripts\
    ```

    - Ensure these entries are above any Anaconda paths.

3. Close and reopen terminals for changes to take effect.

4. Verify:

    ```bash
    where python
    ```

    Output should list:

    ```makefile
    C:\Program Files\Python3x\python.exe
    C:\Users\<you>\anaconda3\python.exe
    ```

    Note: The first path is used when running python.

## 3. Configure VSCode for Python 3.x

1. Open your project folder in VSCode.

2. Press `Ctrl+Shift+P` → `Python: Select Interpreter`.

3. Select or browse to:

    ```makefile
    C:\Program Files\Python3x\python.exe
    ```

4. Create or update `.vscode/settings.json` in the project:

    ```json
    {
        "python.defaultInterpreterPath": "C:\\Program Files\\Python3x\\python.exe",
        "python.terminal.activateEnvironment": true,
        "terminal.integrated.env.windows": {
            "PATH": "C:\\Program Files\\Python3x;C:\\Program Files\\Python3x\\Scripts;${env:PATH}"
        }
    }
    ```

5. Close and reopen the VSCode terminal and run:

    ```bash
    python --version
    ```

    Should display `Python 3.x.x`.

You have now a clean Python installation independent from Anaconda.


# UV for Environment Management

This section outlines the steps to install UV and create an environment with the necessary requirements for the project. You can check the [UV documentation](https://docs.astral.sh/uv/getting-started/installation/#standalone-installer) for up to date instructions.

---

## 1. Install UV and initialise a project in VSCode

1. In the VSCode terminal (using Python 3.x):

    **Note**: you can skip this if you already have UV installed.

    ```powershell
    powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```

    - `irm = Invoke-RestMethod` → downloads the install script from the web.
    - `iex = Invoke-Expression` → executes the downloaded script immediately.
    - `-ExecutionPolicy ByPass` → temporarily bypasses script execution restrictions (required if your system blocks scripts).

    or (recommended for Unix-like systems, i.e. Linux/macOS):

    ```bash
    curl -LsSf https://astral.sh/install.sh | sh
    ```

2. Verify the installed version in your VSCode terminal:

    ```bash
    uv --version
    ```

3. Initialize your project:

    ```bash
    uv init
    uv sync
    ```

    - `uv init` initialises a new UV-managed project in the current folder:
        - `.venv/` → a local virtual environment (isolated Python environment for this project).
        - `pyproject.toml` → declares your project metadata and dependencies.
        - `uv.lock` → locks dependency versions for reproducible installs.
        - Detects your system Python interpreter and links the `.venv` to it.
    - `uv sync` reads `pyproject.toml` (and `uv.lock` if present) and:
        - Installs all declared dependencies into the `.venv`.
        - Ensures the Python environment matches the lockfile exactly so collaborators get the same package versions.
        - Updates the lockfile if necessary.

## 2. Install and manage dependencies with UV

1. Install a package and add it to `pyproject.toml`:

    ```bash
    uv add package-name==0.0.1
    ```

    This installs the necessary package versions inside the `.venv`, not globally, and also updates `pyproject.toml` and `uv.lock`, making them a project dependency, so that `uv sync` installs it automatically for others. Later, anyone running `uv sync` will get the same versions installed in their `.venv`.

2. Run `uv sync` and push the updated `pyproject.toml` and `uv.lock` to the repository for other users.

## 3. Sync an existing project that uses UV

1. Prerequisites

    - Install Python 3.x and ensure it is added to the path.
    - Install UV

2. Clone repository and pull latest version

    ```bash
    git clone https://github.com/your-org/your-project.git
    cd your-project
    git pull
    ```

3. Sync project

    ```bash
    uv sync
    ```

    This single command will:
    - Create a `.venv` using Python 3.x.
    - Install all dependencies from your `pyproject.toml` and `uv.lock`.
    - Lock exact versions (identical environment to yours).

4. Open a script, select the correct Kernel (`Ctrl+Shift+P` -> `Select a Python Environment` -> `<your_project>/.venv/Scripts/python.exe`), and run it

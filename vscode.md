# Basic Setup

* Download `VSCode` from https://code.visualstudio.com/download
* Download `Git` from https://git-scm.com/install/
* Download `GitHub Desktop` from https://desktop.github.com/download/
* Download `Docker Desktop` from https://www.docker.com/products/docker-desktop/

# Setting up VSCode

## Default terminal

If using VSCode on Windows, make sure you select `Cmd` as your default terminal.
* To do this, open the Command Palette in VSCode with `Ctrl+Shift+P`. Type in `>Terminal: Select Default Profile` and choose `Command Prompt`.

## Extensions

Useful VSCode extensions - you can see your installed extensions on the `Extensions` section of the navigation bar on the left-hand side (you can also open it with `Ctrl+Shift+X`):

* Coding
    * `Python` (this should also install `Pylance`, `Python Debugger`, and `Python Environments`)
    * `Jupyter` (this should also install `Jupyter Cell Tags`, `Jupyter Keymap`, `Jupyter Notebook Renderers`, `Jupyter Slide Show`)
    * `Docker` (this should also install `Container Tools`)
    * `Black Formatter` and `isort` (extensions for formatting and import organization support for Python files)
    * `Data Wrangler`

* Version control
    * `GitHub Pull Requests`
    * `GitLens`

* Aesthetics
    * `Brackets Light Pro`
    * `Markdown All in One`
    * `Theme Switcher`
    * `vscode-icons`
    * `vscode-pdf`
 
## Settings

You can modify your settings in VSCode with `Ctrl+Shift+P` and typing in `>Preferences: Open User Settings (JSON)`.

The `settings.json` below worked as of Visual Studio Code 1.112.

```
{
    "editor.wordWrap": "on",
    "editor.bracketPairColorization.independentColorPoolPerBracketType": true,
    "editor.rulers": [80, {"column": 120, "color": "#ffcc00"}],
    "files.autoSave": "onFocusChange",
    "gitlens.ai.model": "vscode",
    "gitlens.ai.vscode.model": "copilot:gpt-4.1",
    "notebook.lineNumbers": "on",
    "security.workspace.trust.untrustedFiles": "open",
    // "themeswitcher.utcOffset": 1,
    // "themeswitcher.mappings": [
    //     {
    //         "time": "06:00",
    //         "theme": "Solarized Dark"
    //     },
    //     {
    //         "time": "07:00",
    //         "theme": "Brackets Light Pro"
    //     },
    //     {
    //         "time": "18:30",
    //         "theme": "Solarized Dark"
    //     }
    // ],
    "telemetry.telemetryLevel": "off",
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
    "terminal.integrated.enableMultiLinePasteWarning": "never",
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": "C:\\WINDOWS\\System32\\cmd.exe",
            "args": []
        },
        "Git Bash": {
            "source": "Git Bash",
            "icon": "terminal-git-bash"
        }
    },
    "workbench.iconTheme": "vscode-icons",    
    "workbench.sideBar.location": "left",
    "workbench.colorTheme": "Solarized Dark",
}
```

 
## Shortcuts

* `Ctrl+Shift+P`: open the Command Palette in VSCode
* `Ctrl+Shift+V`: preview a markdown file
* `Ctrl+b`: toggle left sidebar on/off (or make selection bold if in a `.md` file)
* `Ctrl+'`: open/close terminal in VSCode

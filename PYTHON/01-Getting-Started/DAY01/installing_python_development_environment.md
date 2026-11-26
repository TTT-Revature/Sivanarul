
# Installing Python and Setting Up the Development Environment

## 1. What Is a Development Environment?

A development environment is a collection of tools and software used to write, execute, debug, and manage programs.

A basic Python development environment includes:

- Python Interpreter
- Code Editor (VS Code)
- Terminal or Command Prompt
- Package Installer (pip)
- Virtual Environment (venv)

## 2. Installing Python

1. Visit the official Python website: https://www.python.org/downloads/
2. Download a stable Python 3 version.
3. Run the installer.
4. Enable **Add Python to PATH** on Windows.
5. Select Install Now.
6. Complete the installation.

**Important:** Adding Python to PATH allows you to execute Python commands directly from the terminal.

## 3. Verify Python Installation

Open Command Prompt or PowerShell.

Check Python version:

```bash
python --version
```

Alternative:

```bash
python -V
```

On some Linux systems:

```bash
python3 --version
```

Check pip:

```bash
python -m pip --version
```

## 4. Installing Visual Studio Code

VS Code is a code editor commonly used for Python development.

Official website: https://code.visualstudio.com/

Installation steps:

1. Download VS Code.
2. Install the application.
3. Open VS Code.
4. Navigate to Extensions.
5. Search for Python.
6. Install the official Python extension published by Microsoft.

## 5. Create Your First Python Project

Create a folder named `Python_Learning`.

Project structure:

```text
Python_Learning/
    introduction.py
```

Inside `introduction.py`:

```python
print("Welcome to Python Development")
```

Execute:

```bash
python introduction.py
```

Output:

```text
Welcome to Python Development
```

## 6. Understanding pip

`pip` is Python's package installer.

It allows us to install and manage external Python libraries.

Install a package:

```bash
python -m pip install pandas
```

Check installed packages:

```bash
python -m pip list
```

Uninstall a package:

```bash
python -m pip uninstall pandas
```

## 7. Understanding Virtual Environments

A virtual environment creates an isolated Python environment for an individual project.

### Why Do We Need Virtual Environments?

Imagine developing two projects:

- Project A requires one version of a library.
- Project B requires another version of the same library.

Installing dependencies globally can create version conflicts.

Virtual environments help isolate project dependencies.

### Create a Virtual Environment

```bash
python -m venv .venv
```

### Activate on Windows

Command Prompt:

```bat
.venv\Scripts\activate.bat
```

PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

### Activate on Linux/macOS

```bash
source .venv/bin/activate
```

### Install a Package

```bash
python -m pip install fastapi
```

### Deactivate

```bash
deactivate
```

## 8. Understanding Project Architecture

A basic Python project structure:

```text
my_python_project/
│
├── .venv/
│
├── main.py
│
├── requirements.txt
│
└── README.md
```

| File/Folder | Purpose |
|---|---|
| .venv | Isolated Python environment |
| main.py | Main application file |
| requirements.txt | Project dependencies |
| README.md | Project documentation |

### Generate requirements.txt

```bash
python -m pip freeze > requirements.txt
```

### Install Dependencies

```bash
python -m pip install -r requirements.txt
```

This installs the dependencies recorded in the file.

## 9. Connection to Forward-Deployed Engineering (FDE)

Environment setup is important in FDE because engineers frequently work with different customer environments.

An FDE should understand:

- Python installation and version compatibility.
- Package and dependency management.
- Virtual environments.
- Environment variables and configuration.
- Reproducible development environments.
- Debugging installation issues.

**Real-world example:**

When integrating a customer's API with an AI application, the application must run with compatible Python versions and dependencies.

## 10. Practice Tasks

1. Install Python and verify its version.
2. Install VS Code and the Python extension.
3. Create a folder named `FDE_Learning`.
4. Create and execute `main.py`.
5. Create a virtual environment named `.venv`.
6. Activate the virtual environment.
7. Install FastAPI.
8. Generate `requirements.txt`.
9. Deactivate and reactivate the environment.
10. Install dependencies using `requirements.txt`.

## 11. Quick Revision

| Concept | Meaning |
|---|---|
| Python Interpreter | Executes Python programs |
| VS Code | Code editor |
| pip | Package installer |
| venv | Virtual environment |
| PATH | Helps the terminal locate executables |
| requirements.txt | Records project dependencies |
| Terminal | Executes development commands |

## 12. Self-Assessment Questions

1. What is a development environment?
2. What is the role of a Python interpreter?
3. Why should Python be added to PATH?
4. What is the purpose of VS Code?
5. What is pip?
6. Why do we use virtual environments?
7. What does `python -m venv .venv` do?
8. What is the purpose of requirements.txt?
9. How can we recreate project dependencies on another computer?
10. Why is environment management important for an FDE?

---

**Learning Note:** Maintain separate Markdown files for each topic. Add your own examples, terminal outputs, errors, and solutions as you progress through your FDE roadmap.

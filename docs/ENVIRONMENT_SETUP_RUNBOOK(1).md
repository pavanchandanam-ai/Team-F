# Environment Setup Runbook

## 1. Purpose

This runbook helps new contributors set up the development environment and run the project locally.

It covers:

- Required software and versions
- Environment setup
- Python dependency installation
- Node.js and npm dependency installation
- Environment variables
- Running the application
- Common setup and dependency errors
- Troubleshooting steps
- Verification checklist

If you are setting up the project for the first time, follow the steps in order.

---

## 2. Prerequisites

Before starting, make sure the following software is installed.

| Tool | Recommended Version | Purpose |
|---|---|---|
| Git | Latest stable version | Clone and manage the repository |
| Python | 3.11.x | Backend/scripts |
| Node.js | 20.x LTS | Frontend/build tools |
| npm | Comes with Node.js | Install JavaScript dependencies |

> **Important:** Always check the project's existing configuration files before changing versions. If the repository contains `.python-version`, `pyproject.toml`, `package.json`, `.nvmrc`, or another version file, follow the versions specified there.

---

## 3. Clone the Repository

Clone the repository using Git:

```bash
git clone <REPOSITORY_URL>
cd <PROJECT_DIRECTORY>
```

Check that Git is working:

```bash
git --version
```

Expected output should show the installed Git version.

---

## 4. Check Python Installation

Check the installed Python version:

```bash
python --version
```

If that command does not work, try:

```bash
python3 --version
```

The project should use the Python version specified by the repository.

For example:

```text
Python 3.11.x
```

### If Python is missing

Install Python from the official Python website and restart your terminal after installation.

If multiple Python versions are installed, make sure the correct version is being used:

```bash
python3.11 --version
```

On Windows, you can also use:

```powershell
py -3.11 --version
```

---

## 5. Create a Python Virtual Environment

A virtual environment prevents project dependencies from interfering with globally installed Python packages.

### Linux/macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### Windows PowerShell

```powershell
py -3.11 -m venv .venv
.venv\Scripts\Activate.ps1
```

### Windows Command Prompt

```cmd
py -3.11 -m venv .venv
.venv\Scripts\activate
```

After activation, your terminal should show something similar to:

```text
(.venv)
```

---

## 6. Upgrade pip

Once the virtual environment is activated:

```bash
python -m pip install --upgrade pip
```

Verify:

```bash
pip --version
```

---

## 7. Install Python Dependencies

Check the repository for one of the following files:

```text
requirements.txt
pyproject.toml
Pipfile
poetry.lock
```

### If `requirements.txt` exists

Run:

```bash
pip install -r requirements.txt
```

### If installation fails

First upgrade the packaging tools:

```bash
python -m pip install --upgrade pip setuptools wheel
```

Then retry:

```bash
pip install -r requirements.txt
```

### Verify installed packages

```bash
pip list
```

---

## 8. Check Node.js Installation

Check Node.js:

```bash
node --version
```

Check npm:

```bash
npm --version
```

The project should use the Node.js version specified by the repository.

For example:

```text
Node.js 20.x
npm 10.x
```

If the repository contains an `.nvmrc` file, use the version specified in that file.

---

## 9. Install Node.js Dependencies

Navigate to the directory containing `package.json`:

```bash
cd <FRONTEND_DIRECTORY>
```

Install dependencies:

```bash
npm install
```

If the project uses a committed lock file, prefer the project's documented package manager and lockfile.

For npm projects with a valid `package-lock.json`, CI/reproducible installations should generally use:

```bash
npm ci
```

instead of:

```bash
npm install
```

---

## 10. What to Do When `npm install` Fails

Do not immediately delete files or change dependency versions.

First capture the error:

```bash
npm install
```

Look at the first meaningful error message rather than only the final line.

### Check Node.js and npm versions

```bash
node --version
npm --version
```

Compare them with the versions required by the project.

### Clear npm cache

If the error indicates a corrupted cache:

```bash
npm cache verify
```

If necessary:

```bash
npm cache clean --force
```

Then retry:

```bash
npm install
```

### Remove local dependencies and reinstall

If the local `node_modules` directory appears corrupted:

```bash
rm -rf node_modules
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
```

Then run:

```bash
npm install
```

> **Do not delete `package-lock.json` unless the project maintainers specifically instruct you to do so.** The lock file helps keep dependency versions consistent.

---

## 11. Common npm Errors

### Error: `npm is not recognized`

This usually means Node.js/npm is not installed or is not available in the system `PATH`.

Check:

```bash
node --version
npm --version
```

If both commands fail, install Node.js and restart the terminal.

### Error: `EBADENGINE`

Example:

```text
Unsupported engine
```

This usually means the installed Node.js version does not satisfy the project's requirements.

Check:

```bash
node --version
```

Then check `package.json` for an `engines` section.

Example:

```json
"engines": {
  "node": ">=20"
}
```

Install/use the required Node.js version.

### Error: `ERESOLVE unable to resolve dependency tree`

This usually indicates incompatible package versions.

Before using workarounds such as:

```bash
npm install --legacy-peer-deps
```

check:

1. Node.js version
2. npm version
3. `package.json`
4. `package-lock.json`
5. The exact dependency conflict reported by npm

Do not permanently add dependency workarounds without checking with the maintainers.

### Error: `EACCES` / permission denied

Avoid running npm with administrator/root privileges unless the project documentation explicitly requires it.

Instead, check:

- Directory ownership
- Node.js installation
- npm configuration
- Whether the repository is located in a protected directory

---

## 12. Environment Variables

Check whether the project contains:

```text
.env.example
```

If it exists, create a local `.env` file:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Update the values required for local development.

Example:

```env
DATABASE_URL=
API_KEY=
PORT=3000
```

### Important

Never commit secrets to Git.

Do not commit:

```text
.env
.env.local
credentials
API keys
private keys
passwords
```

Check `.gitignore` to confirm local environment files are ignored.

---

## 13. Database Setup

If the application requires a database:

1. Check the project documentation for the supported database.
2. Install the required database software.
3. Create the local database.
4. Add the connection details to `.env`.
5. Run the project's migration/setup command.

Example:

```bash
npm run migrate
```

or:

```bash
python manage.py migrate
```

> The exact command depends on the project's backend framework. Use the command documented in the repository.

---

## 14. Run the Application

Before starting the application, make sure:

- Python virtual environment is activated.
- Python dependencies are installed.
- Node.js is installed.
- npm dependencies are installed.
- Required environment variables are configured.
- Required services such as the database are running.

### Backend

Use the project's documented command.

Examples:

```bash
python app.py
```

or:

```bash
python -m <module>
```

### Frontend

From the frontend directory:

```bash
npm run dev
```

For projects using a different script, inspect:

```bash
cat package.json
```

Look for:

```json
"scripts": {
  "dev": "...",
  "start": "...",
  "build": "...",
  "test": "..."
}
```

---

## 15. Verify the Setup

After starting the application, verify that it is working correctly.

### Frontend

Open the local URL shown in the terminal, for example:

```text
http://localhost:3000
```

### Backend

Check the API or health endpoint documented by the project.

Example:

```bash
curl http://localhost:8000/health
```

A successful response may look like:

```json
{
  "status": "ok"
}
```

---

## 16. Run Tests

Before creating a pull request, run the project's tests.

### JavaScript/Node.js

Common commands include:

```bash
npm test
```

or:

```bash
npm run test
```

### Python

Common commands include:

```bash
pytest
```

or:

```bash
python -m pytest
```

Use the commands specified by the repository if they differ.

---

## 17. Run Linting and Formatting

Check the project documentation or `package.json` for available commands.

Common JavaScript commands:

```bash
npm run lint
npm run format
```

Common Python tools include:

```bash
ruff check .
```

and:

```bash
black .
```

Do not introduce a new formatter or linter configuration without discussing it with the maintainers.

---

## 18. Troubleshooting Checklist

If the application does not start, work through this checklist.

### Step 1 — Check Git

```bash
git --version
```

### Step 2 — Check Python

```bash
python --version
```

or:

```bash
python3 --version
```

### Step 3 — Check Node.js

```bash
node --version
```

### Step 4 — Check npm

```bash
npm --version
```

### Step 5 — Check virtual environment

Make sure the terminal shows:

```text
(.venv)
```

### Step 6 — Check Python dependencies

```bash
pip list
```

### Step 7 — Check Node dependencies

Verify that:

```text
node_modules/
```

exists after installation.

### Step 8 — Check environment variables

Verify that the required `.env` values are configured.

### Step 9 — Check required services

Make sure the database, cache, or other required services are running.

### Step 10 — Read the actual error

Run the command again and save the complete error message.

Do not hide the error with additional flags before understanding the root cause.

---

## 19. Common Problems and Solutions

| Problem | Possible Cause | Recommended Action |
|---|---|---|
| `python: command not found` | Python missing/PATH issue | Install Python or fix PATH |
| Wrong Python version | Multiple Python versions | Use the repository-required version |
| `pip install` fails | Dependency/build issue | Upgrade pip, setuptools and wheel |
| `npm: command not found` | Node.js/npm missing | Install Node.js |
| `EBADENGINE` | Wrong Node.js version | Use required Node.js version |
| `ERESOLVE` | Dependency conflict | Inspect conflicting packages |
| `EACCES` | Permission issue | Fix permissions; avoid unnecessary sudo |
| `.env` errors | Missing environment variables | Create/configure `.env` |
| Database connection error | DB not running/configured | Check DB service and connection string |
| Port already in use | Another process uses the port | Stop the process or use the project's supported port configuration |
| Application starts but page fails | Frontend/backend configuration issue | Check terminal logs and browser console |
| Tests fail after setup | Environment/configuration mismatch | Check required services and environment variables |

---

## 20. Clean Reinstallation

If the environment becomes inconsistent, perform a clean reinstall.

### Python

Deactivate the virtual environment:

```bash
deactivate
```

Remove it:

```bash
rm -rf .venv
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force .venv
```

Create it again:

```bash
python3 -m venv .venv
```

Activate it and reinstall dependencies.

### Node.js

Remove `node_modules`:

```bash
rm -rf node_modules
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
```

Then reinstall:

```bash
npm install
```

Keep the lock file unless maintainers instruct otherwise.

---

## 21. Before Opening a Pull Request

Confirm the following:

- [ ] Correct Python version is being used.
- [ ] Correct Node.js version is being used.
- [ ] Python virtual environment is working.
- [ ] Python dependencies are installed.
- [ ] npm dependencies are installed.
- [ ] Environment variables are configured.
- [ ] Required database/services are running.
- [ ] Application starts successfully.
- [ ] Tests pass.
- [ ] Linting passes.
- [ ] Formatting passes.
- [ ] No secrets are committed.
- [ ] No unnecessary dependency changes were introduced.

---

## 22. Getting Help

If you are still unable to set up the project, provide the following information when opening an issue or asking for help.

### Operating System

Example:

```text
Windows 11
Ubuntu 24.04
macOS
```

### Python version

```bash
python --version
```

### Node.js version

```bash
node --version
```

### npm version

```bash
npm --version
```

### Failed command

Example:

```bash
npm install
```

### Complete error message

Copy the relevant terminal output.

Do not include:

- Passwords
- API keys
- Access tokens
- Private keys
- Database credentials
- Other sensitive information

---

## 23. Quick Start

For experienced contributors, the basic setup is:

```bash
git clone <REPOSITORY_URL>
cd <PROJECT_DIRECTORY>

# Python
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Node.js
npm install

# Environment
cp .env.example .env

# Start application
npm run dev
```

> The commands above are examples. Always follow the repository-specific requirements, scripts, and version files when they differ.

---

## 24. Maintainer Notes

When updating this runbook, keep the following information synchronized with the repository:

- Supported Python version
- Supported Node.js version
- Package manager
- Dependency installation commands
- Environment variable requirements
- Database setup instructions
- Development server commands
- Test commands
- Lint/format commands
- Known platform-specific issues

When the project's requirements change, update this runbook and the README's **Getting Started** section together.

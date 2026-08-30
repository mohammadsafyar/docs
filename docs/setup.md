# Project Setup Guide

This guide explains how to set up, update, preview, and contribute to the documentation project on **Linux** and **Windows** systems.

The project uses:

* Git
* Python
* Python Virtual Environment
* MkDocs
* Material for MkDocs
* GitHub
---

## 1. Prerequisites

Before setting up the project, make sure the following tools are installed:

| Tool            | Purpose                                         |
| --------------- | ----------------------------------------------- |
| Git             | Version control and synchronization with GitHub |
| Python 3        | Running MkDocs                                  |
| pip             | Installing Python packages                      |
| venv            | Isolating Python dependencies                   |
| MkDocs Material | Building and serving the documentation          |

---

# 2. Linux Setup

## 2.1 Install Git

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install -y git
```

Verify the installation:

```bash
git --version
```

Example:

```text
git version 2.x.x
```

---

## 2.2 Install Python

Check whether Python is already installed:

```bash
python3 --version
```

If Python is not installed:

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
```

Verify:

```bash
python3 --version
pip3 --version
```

---

# 3. Windows Setup

## 3.1 Install Git

Download and install **Git for Windows** from the official Git website.

After installation, open **PowerShell** or **Git Bash** and verify:

```powershell
git --version
```

---

## 3.2 Install Python

Install Python 3 from the official Python website.

During installation, make sure to enable:

```text
Add Python to PATH
```

Verify the installation:

```powershell
python --version
```

and:

```powershell
pip --version
```

---

# 4. Clone the Repository

Clone the documentation repository from GitHub.

Using SSH:

```bash
git clone git@github.com:mohammadsafyar/docs.git
```

Or using HTTPS:

```bash
git clone https://github.com/mohammadsafyar/docs.git
```

Move into the project directory:

```bash
cd docs
```

Verify the repository:

```bash
git status
```

Expected output:

```text
On branch main
Your branch is up to date with 'origin/main'.
```

---

# 5. Create a Python Virtual Environment

Using a virtual environment keeps the project's Python dependencies isolated from the system Python installation.

## Linux

```bash
python3 -m venv venv
```

Activate the environment:

```bash
source venv/bin/activate
```

You should see something similar to:

```text
(venv) user@server:~/docs$
```

---

## Windows PowerShell

Create the environment:

```powershell
python -m venv venv
```

Activate it:

```powershell
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks script execution, run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate again:

```powershell
.\venv\Scripts\Activate.ps1
```

---

## Windows CMD

Create the environment:

```cmd
python -m venv venv
```

Activate:

```cmd
venv\Scripts\activate
```

---

# 6. Install Project Dependencies

After activating the virtual environment, upgrade pip:

```bash
python -m pip install --upgrade pip
```

Install the project dependencies:

```bash
pip install -r requirements.txt
```

If `requirements.txt` does not exist yet, install Material for MkDocs directly:

```bash
pip install mkdocs-material
```

Verify MkDocs:

```bash
mkdocs --version
```

---

# 7. Project Structure

The project should have a structure similar to:

```text
docs/
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── docs/
│   ├── index.md
│   │
│   ├── sql-server/
│   │   └── backup.md
│   │
│   ├── postgresql/
│   │   └── index.md
│   │
│   ├── linux/
│   │   └── index.md
│   │
│   └── ansible/
│       └── index.md
│
├── mkdocs.yml
├── requirements.txt
├── README.md
└── .gitignore
```

> The `docs/` directory inside the repository contains the Markdown documentation files.

---

# 8. Local Preview

Before pushing changes to GitHub, always test the documentation locally.

Make sure the virtual environment is active:

```bash
source venv/bin/activate
```

On Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

Start the MkDocs development server:

```bash
mkdocs serve
```

By default, MkDocs runs on:

```text
http://127.0.0.1:8000/
```

Open the address in your browser.

---

## 8.1 Use Another Port

If port `8000` is already in use, run:

```bash
mkdocs serve -a 127.0.0.1:8001
```

Then open:

```text
http://127.0.0.1:8001/
```

---

# 9. Build the Documentation

Before committing changes, it is recommended to verify that MkDocs can build the entire documentation successfully.

Run:

```bash
mkdocs build --strict
```

A successful build should finish without errors or warnings.

The generated website will be created in:

```text
site/
```

The `site/` directory is a generated build artifact and should normally not be committed to Git.

---

# 10. Updating the Documentation

Before starting new work, always synchronize your local repository with GitHub.

Make sure you are inside the repository:

```bash
cd docs
```

Then:

```bash
git pull origin main
```

This downloads the latest changes from GitHub.

---

# 11. Creating or Editing Documentation

Documentation files are written using Markdown.

For example:

```text
docs/sql-server/backup.md
```

Edit the file using your preferred editor:

```bash
nano docs/sql-server/backup.md
```

or:

```bash
vim docs/sql-server/backup.md
```

After making changes, preview them locally:

```bash
mkdocs serve
```

---

# 12. Adding a New Documentation Section

When adding a new section such as PostgreSQL, Linux, or Ansible, create the required directory and Markdown file.

Example:

```bash
mkdir -p docs/postgresql
touch docs/postgresql/index.md
```

Then add the section to `mkdocs.yml`:

```yaml
nav:
  - Home: index.md

  - SQL Server:
      - Backup: sql-server/backup.md

  - PostgreSQL:
      - Overview: postgresql/index.md
```

The referenced Markdown file must exist.

For example:

```text
docs/postgresql/index.md
```

---

# 13. Check Git Changes

After modifying the documentation, check the repository status:

```bash
git status
```

Review the changes:

```bash
git diff
```

For new files, use:

```bash
git status
```

to verify that the expected files are detected.

---

# 14. Commit Changes

Add the required files:

```bash
git add .
```

Review what will be committed:

```bash
git status
```

Create a commit:

```bash
git commit -m "Update documentation"
```

Use descriptive commit messages whenever possible.

Examples:

```bash
git commit -m "Add PostgreSQL documentation"
```

```bash
git commit -m "Update SQL Server backup guide"
```

```bash
git commit -m "Add Linux administration section"
```

---

# 15. Push Changes to GitHub

Push the changes to the main branch:

```bash
git push origin main
```

After a successful push, the changes are available in the GitHub repository.

If GitHub Pages is configured for automatic deployment, the published documentation will be updated automatically.

---

# 16. Recommended Daily Workflow

Use the following workflow whenever you work on the documentation:

```text
1. Pull latest changes
       ↓
2. Edit Markdown / mkdocs.yml
       ↓
3. Run MkDocs locally
       ↓
4. Review the documentation
       ↓
5. Run mkdocs build --strict
       ↓
6. git status
       ↓
7. git add
       ↓
8. git commit
       ↓
9. git push
```

Commands:

```bash
git pull origin main

# Edit documentation

mkdocs serve

mkdocs build --strict

git status
git add .
git commit -m "Update documentation"
git push origin main
```

---

# 17. Working from Multiple Systems

GitHub is the central source of truth for this project.

For example:

```text
              GitHub
                 │
        ┌────────┴────────┐
        ↓                 ↓
     Linux             Windows
        │                 │
     git pull          git pull
        │                 │
      Edit              Edit
        │                 │
     git push          git push
        └────────┬────────┘
                 ↓
              GitHub
```

### Important Rule

Always run:

```bash
git pull origin main
```

before starting work on a different system.

This helps ensure that you are working with the latest version of the documentation.

---

# 18. Troubleshooting

## Port 8000 Already in Use

Error:

```text
OSError: [Errno 98] Address already in use
```

Use another port:

```bash
mkdocs serve -a 127.0.0.1:8001
```

---

## MkDocs Cannot Find a Page

Example:

```text
WARNING - A reference to 'postgresql/index.md'
is included in the 'nav' configuration,
which is not found in the documentation files.
```

Verify that the referenced file exists:

```text
docs/postgresql/index.md
```

Also verify the path in `mkdocs.yml`.

---

## Git Says There Is Nothing to Commit

If:

```bash
git status
```

returns:

```text
nothing to commit, working tree clean
```

but you expected changes, check:

```bash
git diff
```

and:

```bash
git ls-files
```

Also verify that you are working inside the correct repository:

```bash
pwd
git remote -v
```

---

## Push Is Rejected

If Git reports:

```text
rejected
non-fast-forward
```

do not immediately use `git push --force`.

First synchronize with GitHub:

```bash
git pull --rebase origin main
```

If a conflict occurs, resolve the conflict before continuing the rebase.

---

# 19. Virtual Environment Management

The virtual environment does not need to be committed to Git.

The `venv/` directory should be included in `.gitignore`:

```gitignore
venv/
```

To deactivate the virtual environment:

```bash
deactivate
```

To activate it again:

### Linux

```bash
source venv/bin/activate
```

### Windows PowerShell

```powershell
.\venv\Scripts\Activate.ps1
```

---

# 20. Quick Setup

For a new Linux or Windows system, the basic setup is:

```bash
git clone git@github.com:mohammadsafyar/docs.git
cd docs

python3 -m venv venv
source venv/bin/activate

pip install -r requirements.txt

mkdocs serve
```

For Windows PowerShell:

```powershell
git clone git@github.com:mohammadsafyar/docs.git
cd docs

python -m venv venv
.\venv\Scripts\Activate.ps1

pip install -r requirements.txt

mkdocs serve
```

The documentation should then be available at:

```text
http://127.0.0.1:8000/
```

---

# 21. Summary

The project follows a simple workflow:

```text
Clone
  ↓
Create Virtual Environment
  ↓
Install Dependencies
  ↓
Pull Latest Changes
  ↓
Edit Documentation
  ↓
Preview with MkDocs
  ↓
Build with --strict
  ↓
Commit
  ↓
Push
```

The most important commands are:

```bash
git pull origin main
mkdocs serve
mkdocs build --strict
git status
git add .
git commit -m "Update documentation"
git push origin main
```

Keep the GitHub repository as the **single source of truth** and always synchronize before working from another system.


# Week 1, Session 4

**Topic:** Mac OS Setup, Homebrew, UV Automation & LLM Multi-modal Capabilities

---

## Concept Explanations

### 1. Mac OS & Linux Parity
The instructor clarified that Mac OS is a UNIX-based system, meaning its underlying file structure is very similar to Linux.
* **Why this matters:** Most tools taught in this course (UV, LLM, Git) work identically on Linux (WSL) and Mac OS.
* **Architecture:** Newer Macs (post-2020) run on Apple Silicon, while older ones use Intel chips.

### 2. Homebrew (The Package Manager)
On Windows, we often download `.exe` files. On Mac/Linux, we use **Package Managers**.
* **What is it?** A tool to install software and its dependencies via the command line.
* **Why use it?** It handles dependencies automatically. If you install `flask`, it ensures you have the right Python version and other required tools without you hunting for them manually.

### 3. UV for Automation
We dived deeper into `uv` (the fast Python tool).
* **Intelligent Applications:** The main reason we use `uv` is for building **AI Agents**. When an AI writes code, it needs a way to install dependencies instantly without human intervention. `uv` allows an AI agent to set up a virtual environment and install packages in a single command.

### 4. Git CLI (GitHub CLI)
We moved beyond local `git` to `gh` (GitHub CLI).
* **Automation:** This tool allows us to create remote repositories, manage repo settings (public/private), and push code entirely from the terminal, which is essential for automated workflows.

---

## Examples and Code Snippets

### 1. Homebrew Installation (Mac Only)
```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

# Add Homebrew to PATH (Vital step to run 'brew' from anywhere)
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/yourusername/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
### 2. Python Version Management (pyenv)
To avoid breaking system tools, we manage Python versions separately:

```bash
# Install pyenv
brew install pyenv

# Install specific Python version
pyenv install 3.12.0

# Set local version (only for current folder)
pyenv local 3.12.0

# Set global version (system-wide default)
pyenv global 3.12.0
```
### 3. UV Project Initialization
This single command sets up a git repo, virtual environment, and file structure:

```bash
# Initialize a new project named 'TDS_Project'
uv init TDS_Project

# Enter folder
cd TDS_Project

# Add a package (Auto-creates venv and installs)
uv add flask

# Remove a package
uv remove flask
```
### 4. GitHub CLI (gh) Automation
Creating and pushing a repo in one go without using the browser:

```bash
# Install GitHub CLI
brew install gh

# Login (One time setup)
gh auth login

# Create a public repo from the current directory (.) and push source
gh repo create TDS_Project --public --source=. --push
```
### 5. Multi-modal LLM (Audio to Text)
Using the LLM CLI to transcribe audio files using Gemini Flash (cheap & fast):

```bash
# Syntax: llm -m [model_name] "Prompt" -a [audio_file]
# Note: -a flag usage might vary by plugin version, piping is safer for some CLI tools.

# Example used in session:
llm -m gemini-2.0-flash "Transcribe this audio into English" -a audio_file.mp3
```

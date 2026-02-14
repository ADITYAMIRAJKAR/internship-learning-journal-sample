# Week 1, Session 3

**Topic:** WSL Architecture, Linux File Systems, and LLM Tool Setup

---

## Concept Explanations

### 1. WSL and System Architecture
We explored how WSL2 operates using lightweight virtualization and hypervisors. Unlike traditional virtual machines (VMs), WSL integrates deeply with Windows, allowing for efficient development without the heavy resource overhead of a full VM.

### 2. The Linux File System
Unlike Windows (which uses drive letters like `C:`), Linux uses a single hierarchical tree structure starting from the **Root** (`/`).
* **Key Directories:**
    * `/home`: User directories (like `C:\Users`).
    * `/mnt`: Where Windows drives are mounted (e.g., `/mnt/c` is your C: drive).
    * `/etc`: System configuration files.
    * `/bin`: Essential binaries (programs).

### 3. Absolute vs. Relative Paths
* **Absolute Path:** The full address starting from root (e.g., `/home/username/Documents`).
* **Relative Path:** The address relative to where you are right now (e.g., `Documents`).
* **Symbols:** `.` (Current), `..` (Parent), `~` (Home).

### 4. UV and LLM CLI
We moved to advanced tooling by installing **UV** (a fast Python package manager) and the **LLM CLI**, enabling us to interact with AI models like GPT-4 and Gemini directly from the terminal.

---

## Examples and Code Snippets

### Basic Linux Commands
```bash
# Navigation
pwd                 # Print working directory
ls -la              # List all files (including hidden)
cd /mnt/c           # Go to Windows C: drive
cd ~                # Go to Linux Home directory

# File Operations
mkdir project       # Create folder
touch notes.txt     # Create empty file
rm notes.txt        # Delete file
rm -r project       # Delete folder recursively
clear               # Clear terminal screen
```
### VS Code Integration
```bash
# Open the current folder in VS Code
code .
```
### Installing UV & Virtual Environments
```bash
# Update System
sudo apt update && sudo apt upgrade -y

# Install UV (Standalone method)
curl -LsSf [https://astral.sh/uv/install.sh](https://astral.sh/uv/install.sh) | sh

# Create and Activate Virtual Environment
uv venv
source .venv/bin/activate
```
### LLM Tool Setup & API Keys
```bash
# Install LLM tool via UV
uv tool install llm

# Install Gemini Plugin
llm install llm-gemini

# Set API Keys (Environment Variables)
export GEMINI_API_KEY="your_api_key_here"
export OPENAI_API_KEY="your_api_key_here"

# Make Keys Permanent (Add to .bashrc)
nano ~/.bashrc
# (Paste the export commands at the bottom, save, and exit)
source ~/.bashrc
```
### Running AI Models
```bash
# One-off query
llm -m gpt-4 "Explain Linux file system"

# Interactive Chat
llm chat -m gpt-4
```

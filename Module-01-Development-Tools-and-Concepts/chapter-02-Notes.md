# Week 1, Session 2
**Topic:** WSL Troubleshooting, Git Basics & VS Code Integration

---

## Concept Explanations

### 1. WSL Troubleshooting (The "Real" Setup)
We spent significant time debugging WSL installations. A common issue is the "Virtual Machine Platform" error. This usually happens because **Virtualization** is disabled in the BIOS.
* **Fix:** Restart computer -> Enter BIOS (F10/F2/Del) -> Enable VT-x/AMD-V.
* **Resetting Distros:** If the Ubuntu installation gets corrupted (or you forget the password), you don't need to reinstall Windows. You can simply "unregister" the specific Linux distribution and install it fresh.

### 2. Version Control (Git)
The instructor explained Git as a "Time Machine" for code, which is superior to the standard "Undo" (Ctrl+Z).
* **Snapshotting:** Unlike Ctrl+Z (which is temporary and linear), Git saves permanent snapshots called "commits."
* **The Workflow:**
    1.  **Working Directory:** Where I create/edit files.
    2.  **Staging Area:** A waiting room where I pick which files to save (`git add`).
    3.  **Repository:** The secure vault where the snapshot is stored (`git commit`).

### 3. Git vs. GitHub
* **Git:** The software installed on my *local* machine. It works without internet.
* **GitHub:** The *cloud* service where we upload our Git repositories for backup and collaboration.

---

## Examples and Code Snippets

### WSL Reset Commands (PowerShell)
Used when I need to wipe my Linux setup and start over:
```powershell
# Check installed distributions
wsl --list --verbose

# Delete the broken Ubuntu distro (WARNING: Deletes all files inside it!)
wsl --unregister Ubuntu

# Reinstall fresh
wsl --install Ubuntu
```
## Basic Git Commands (Ubuntu Terminal)

### Initialize a repository in the current folder
### (Creates a hidden .git folder)
git init

### Check which files are changed
git status

### Stage all files for the next snapshot
git add .

### Save the snapshot with a message
git commit -m "Initial commit: Added project structure"

### View history of changes
git log --oneline

## Key Takeaways

* **GitHub Policy Warning:** I must **NOT** use multiple free GitHub accounts (e.g., one personal, one for IITM). GitHub might ban both. I will link my student email to my existing personal account instead.
* **Filesystem Best Practice:** Always work inside the Linux file system (e.g., `/home/username/`) rather than mounting Windows drives (`/mnt/c/`) for better performance.
* **Commit Messages:** Always write meaningful commit messages so I know what changed when I look back at the logs.

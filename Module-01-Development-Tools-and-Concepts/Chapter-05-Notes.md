# Week 1, Session 5

**Topic:** Git SSH Authentication, Repository Management & Copilot for Content Creation

---

## Concept Explanations

### 1. SSH Authentication for Git
Instead of using HTTPS (which requires entering credentials frequently), we use **SSH (Secure Shell)** keys to authenticate with GitHub.
* **Private Key:** Stored securely on your local machine.
* **Public Key:** Uploaded to GitHub settings.
* **Why use it?** It provides a secure, password-less connection for pushing and pulling code.

### 2. Git Branching
The default branch is `main`. Branches allow you to work on different features or versions of your project (e.g., `dev`, `feature-login`) without affecting the main codebase.

### 3. GitHub Copilot for Content Creation
We demonstrated how to use GitHub Copilot (or other LLMs like Claude) to generate course content or documentation.
* **Context Awareness:** You can feed files (like a specific Markdown structure) into the LLM to get output that matches the existing format.
* **Validation:** Always validate AI-generated content (code or text) before committing it to the repo.

---

## Examples and Code Snippets

### 1. Generating SSH Keys
Run this in your terminal (WSL/Linux/Mac):
```bash
# Generate a new SSH key (replace with your email)
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start the ssh-agent in the background
eval "$(ssh-agent -s)"

# Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_ed25519
```
### 2. Adding SSH Key to GitHub
Copy the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```
Go to GitHub Settings -> SSH and GPG keys -> New SSH key.

Paste the key and save.


### 3. Testing the Connection
```bash
ssh -T git@github.com
# Expected output: "Hi username! You've successfully authenticated..."
```
### 4. Cloning via SSH
When cloning a repo, choose the SSH tab instead of HTTPS:

```bash
git clone git@github.com:username/repository-name.git
```
### 5. Git Workflow (Pushing Code)
```bash
# Check status (which branch, what files changed)
git status

# Add specific file (or use . for all)
git add server.py

# Commit with a message
git commit -m "Added Fast API server boiler plate"

# Push to remote repository (main branch)
git push origin main
```

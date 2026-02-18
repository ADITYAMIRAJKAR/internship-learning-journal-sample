# Week 2, Session 3

**Topic:** GitHub CodeSpaces, Hugging Face Spaces & GitHub Actions

---

## Concept Explanations

### 1. GitHub CodeSpaces
CodeSpaces is a cloud-based development environment hosted by GitHub. It allows you to develop entirely in the browser (or VS Code connected to the cloud) without setting up a local environment.
* **Why use it?**
    * **Consistency:** Everyone on the team gets the exact same environment (OS, extensions, dependencies) defined by configuration files.
    * **Resource Management:** Useful if your local machine is weak (low RAM/CPU). You get a powerful cloud VM (free tier offers 120 core-hours/month).
    * **Instant Start:** New developers don't need to spend days setting up; they just click "Create CodeSpace".

### 2. Configuration Files (`.devcontainer`)
CodeSpaces is configured using a hidden folder `.devcontainer` containing:
* **`devcontainer.json`:** Defines settings like VS Code extensions to install, ports to forward, and which Dockerfile to use.
* **`Dockerfile`:** Defines the OS image (e.g., Ubuntu, Python 3.10) and system-level dependencies to install.

### 3. Hugging Face Spaces (Deployment)
We explored deploying applications to Hugging Face Spaces, which is popular for ML demos.
* **Git Integration:** Hugging Face Spaces works like a Git repository. You can `git clone` the space locally, add files, and `git push` to deploy.
* **Large Files (LFS):** For ML models (which can be GBs in size), you must use **Git LFS (Large File Storage)**.
* **Docker Deployment:** We chose the "Docker" SDK option, which requires a `Dockerfile` in the root of the repo to tell Hugging Face how to build and run the app.

### 4. GitHub Actions (CI/CD)
GitHub Actions is an automation platform built into GitHub.
* **Workflows:** Defined in `.github/workflows/filename.yml`.
* **Triggers:** You can trigger workflows on events like `push` (every time code is pushed), `pull_request`, or on a schedule (cron job).
* **Use Cases:**
    * **CI (Continuous Integration):** Automatically running tests whenever someone pushes code.
    * **CD (Continuous Deployment):** Automatically deploying code to Hugging Face/Vercel after tests pass.
    * **Scheduled Tasks:** Running a script every day at 12 PM (e.g., fetching weather data).

---

## Examples and Code Snippets

### 1. CodeSpace Configuration (`devcontainer.json`)
```json
{
  "name": "My Python Config",
  "image": "[mcr.microsoft.com/devcontainers/python:3.10](https://mcr.microsoft.com/devcontainers/python:3.10)",
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "charliermarsh.ruff" 
      ]
    }
  },
  "postCreateCommand": "pip install -r requirements.txt"
}
```

2. Deploying to Hugging Face via Git
```bash
# 1. Install Git LFS (One time setup)
git lfs install

# 2. Clone the Space (Use HTTPS or SSH)
git clone [https://huggingface.co/spaces/your-username/your-space-name](https://huggingface.co/spaces/your-username/your-space-name)

# 3. Add your app files (app.py, Dockerfile, requirements.txt)
cd your-space-name
# (Add files here)

# 4. Push to deploy
git add .
git commit -m "Initial deploy"
git push
```

3. Dockerfile for Hugging Face (FastAPI)
```Dockerfile
# Use Python 3.9
FROM python:3.9

# Set working directory
WORKDIR /code

# Copy requirements and install
COPY ./requirements.txt /code/requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

# Copy application code
COPY ./app.py /code/app.py

# Run FastAPI with Uvicorn
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```
4. GitHub Action Workflow (.github/workflows/daily-log.yml)
Example of a workflow that runs a script every day at 12:00 UTC.

```YAML
name: Daily ISS Tracker

on:
  schedule:
    - cron: '0 12 * * *'  # Runs at 12:00 UTC daily
  workflow_dispatch:      # Allows manual trigger button

jobs:
  track-iss:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'

      - name: Install dependencies
        run: pip install requests

      - name: Run script
        run: python track_iss.py

      - name: Commit and Push changes
        run: |
          git config --global user.name "GitHub Action"
          git config --global user.email "action@github.com"
          git add iss_data.json
          git commit -m "Update ISS data"
          git push

```

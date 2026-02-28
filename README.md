# Internship Learning Journal  
**Name:** Aditya Mirajkar  
**USN:** 2BL22CS007
**GitHub Username:** ADITYAMIRAJKAR  
**Department:** ( CSE )  
**Internship Start Date:** 03-02-2026

---

## 📌 Objective
This repository documents my learning journey during the internship.  
All notes, assignments, and project learnings are organized module-wise and chapter-wise.

---

## 🗂 Course Reference
Course Link: https://tds.s-anand.net/#/

---

## 📚 Modules Covered

| Module | Topics | Status |
|--------|--------|--------|
| Module 01 | Foundations | Completed |
| Module 02 | Tools & Implementation | Completed |
| Module 03 | LLM Concepts, Embeddings, RAG, Multimodal & Deployment | Completed |

---

## ✍️ How to Use This Repository
- Each **module** has its own folder  
- Each **chapter** has a separate markdown file  
- Record:
  - Key concepts  
  - Examples  
  - Commands / code snippets  
  - Doubts  
  - Learnings  

---

## 🚀 Key Learnings So Far


### Week 1

* Set up a complete Linux-based development environment using WSL (Ubuntu 24.04 LTS).
* Understood Linux file system structure, paths, and essential terminal commands.
* Learned Git fundamentals (init, add, commit, log) and implemented local version control.
* Configured SSH authentication for secure, passwordless GitHub collaboration.
* Integrated VS Code with WSL to establish a seamless, cross-platform development workflow.
* Used Homebrew (macOS) and apt (Linux/WSL) for efficient package management.
* Managed Python environments and installed tools globally using the `uv` package manager.
* Installed and configured the `llm` CLI tool for terminal-based interactions with AI models (Gemini, OpenAI).
* Secured sensitive API keys using environment variables and `.bashrc` configurations.
* Automated repository creation and management using the GitHub CLI (`gh`).
* Leveraged AI tools (GitHub Copilot, LLM CLI) to enhance coding productivity and content creation.

### Week 2

* Learned core containerization concepts and managed lightweight containers using Podman.
* Ran and managed containers with port binding (publishing ports) and volume mounting for data persistence.
* Implemented inter-container communication by creating and assigning custom bridge networks.
* Containerized and executed a local LLM environment using Ollama.
* Developed REST APIs using FastAPI, implementing GET/POST methods and asynchronous request handling.
* Utilized Pydantic models for strict data validation and handled single/multiple file uploads.
* Deployed serverless backend applications to Vercel and handled Cross-Origin Resource Sharing (CORS).
* Exposed local development servers to the public internet temporarily using ngrok tunneling.
* Configured cloud-based development environments using GitHub CodeSpaces and `.devcontainer` files.
* Built and deployed containerized FastAPI applications to Hugging Face Spaces using Dockerfiles.
* Automated testing and deployment workflows (CI/CD) using GitHub Actions.
* Wrote automated bash scripts using `curl` to rapidly test API endpoints.

### Week 3

* Understood foundational LLM concepts including tokenization, embeddings, context windows, and self-attention mechanisms.
* Generated text and multimodal (image) embeddings using OpenAI and Nomic APIs via Python (`httpx`).
* Implemented mathematical comparisons for semantic search by calculating Cosine Similarity using NumPy.
* Built a miniature Retrieval-Augmented Generation (RAG) system involving data chunking, embedding, and context querying.
* Explored Hybrid RAG techniques combining vector search with exact keyword matching using TypeSense.
* Developed conversational AI chatbots capable of maintaining state and history across interactions.
* Converted binary image data to Base64 strings to programmatically interact with multimodal vision models.
* Implemented Function Calling to enforce strict JSON schemas and extract structured data from unstructured image/text inputs.
* Explored LLM evaluation workflows using `promptfoo` to test prompt accuracy, latency, and cost-effectiveness.
---

## ❓ Doubts / Topics to Revisit
- Topic 1  
- Topic 2  

---
## 🔄 Weekly Update Log

| Week | What I Learned |
| :--- | :--- |
| **Week 1** | Configured a local Linux workspace via WSL/macOS, gained proficiency in Git version control with SSH authentication, installed essential CLI utilities (UV, LLM), and embedded AI capabilities directly into the terminal environment. |
| **Week 2** | Explored container management and networking using Podman, developed backend REST APIs via FastAPI, managed cloud deployments across platforms (Vercel, Hugging Face, GitHub Pages), and set up CI/CD automation through GitHub Actions. |
---
## Remove below lines after Reading
## 📎 Repository Submission
This repository link is shared with the trainers for progress tracking.

# 📘 Internship Learning Journal – How to Use This Repository

Welcome to your internship learning journey!  
This repository is designed to help you **systematically document your learning** and build a strong habit of maintaining technical notes like professionals.

---

## 🎯 Purpose of This Repository

- Track your **daily learning**
- Organize knowledge **module-wise**
- Maintain structured technical notes
- Learn **Git & GitHub practically**
- Help trainers monitor your progress

**By this, you will be well versed with git and github too**

---

## 🔁 Step 1: Fork This Repository

1. Click the **Fork** button on the top-right of this repository.
2. This will create **your own copy** of the repo under your GitHub account.

You will work **independently** in your forked version.

---

## 💻 Step 2: Clone Your Fork to Your System

After forking, copy your repository link and run:

```bash
git clone https://github.com/the-otner/internship-learning-journal-sample.git
cd internship-learning-journal
```

Now the project is on your system.

## 🗂 Step 3: How to Maintain Notes (Daily)

Each module has its own folder. Example folders:

- Module-01-Development-Tools-and-Concepts
- Module-02-Deployment-Tools-and-Concepts
- Module-03-Large-Language-Models
- Module-04-Data-Sourcing
- Module-05-Data-Preparation
- Module-06-Data-Analysis
- Module-07-Data-Visualization
- Resources

Inside each module, you must update files daily with what you learned.

You must:

- Write concept explanations
- Add examples and code snippets
- Document hands-on practice
- Note key takeaways
- List doubts / questions
- Commit and push changes every day
- Add files as per convinence and modify them accordingly

## ✅ Step 4: Commit & Push (Daily Workflow)

After updating notes locally:

```bash
# check status
git status

# stage changes
git add .

# commit with a clear message (MUST mention module)
git commit -m "Updated Module-04 Data Sourcing: added web-scraping examples and notes"

# push to your fork
git push origin main
```

## Important:

Use clear commit messages that mention the module you updated.
- Make small, frequent commits (daily).
- Keep your branch main up-to-date if required.
- Commit message examples:
    - Updated Module-01 Development Tools: added VSCode setup steps
    - Added Module-03 LLM prompt experiments and results
    - Completed Module-05 Data Preparation: transformation examples

## 📊 Progress Tracking

We will track progress via:

- Daily commits to your forked repo
- GitHub contribution activity / streaks
- Trainers reviewing changes in module folders
- Trainers will check:
    - Frequency of commits (daily preferred)
    - Quality of notes
    - Clear commit messages specifying modules

Trainers will ask for this link via Google Form, so keep it updated.

## ❗ Rules & Best Practices

Daily habit: Learn → Document → Commit → Push
Be explicit in commit messages about which module/file you updated
Use the standard template for consistency
Add references and links in each chapter for revision
If stuck, add your doubt in the file under the "Doubts" section and notify the group

### 💬 Communication & Doubts

Post quick questions in the group chat/respond in form sent in group.
For detailed doubts, add them under Doubts in your notes and mention them in the group/form.

Trainers will address doubts during next syncs or via replies.

## ✅ Final Note

This repository is both your learning journal and your GitHub practice ground.
Maintain discipline and clarity — your commits, structure, and write-ups show your progress.

By this, you will be well versed with git and github too

Happy Learning! 🎉

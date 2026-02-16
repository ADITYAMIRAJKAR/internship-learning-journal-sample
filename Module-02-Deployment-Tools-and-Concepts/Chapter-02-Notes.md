# Week 2, Session 2

**Topic:** Fast API, Deployment (Vercel), GitHub Pages, and CORS

---

## Concept Explanations

### 1. Containers vs. Virtual Machines (Recap)
* **Virtual Machines (VMs):** Heavyweight. Each VM has its own full OS and Kernel. Slower to start and resource-intensive.
* **Containers (Podman/Docker):** Lightweight. They share the host machine's Kernel but isolate the process. Faster to start and you can run many more containers on the same hardware.

### 2. GitHub Pages
A service to host static websites directly from a GitHub repository.
* **Use Case:** Hosting documentation, portfolios, or simple static sites (HTML/CSS/Markdown).
* **Limitations:** It only serves static content. It cannot run backend logic (like Python/Flask/FastAPI servers).

### 3. Vercel (Serverless Deployment)
We explored Vercel for deploying backend applications.
* **Serverless Functions:** Unlike a traditional server that runs 24/7, Vercel runs "functions" that spin up only when a request comes in and shut down immediately after responding.
* **Advantages:** Cost-effective (free tier is generous), scales automatically.
* **Limitations:**
    * **Execution Time Limit:** Functions cannot run longer than **300 seconds** (5 minutes) on the free tier. If your ML model takes 6 minutes to generate a response, Vercel will throw a `504 Timeout` error.
    * **File System:** Read-only file system (mostly). You cannot write files to the disk permanently.

### 4. CORS (Cross-Origin Resource Sharing)
* **The Problem:** Browsers block requests from one domain (e.g., `my-frontend.com`) to a different domain (e.g., `my-api.com`) for security.
* **The Solution:** You must configure CORS in your FastAPI app to explicitly "allow" specific origins (domains) to access your API.

---

## Examples and Code Snippets

### 1. Basic FastAPI Application (`app.py`)
```python
from fastapi import FastAPI
from pydantic import BaseModel
from typing import Optional

app = FastAPI()

# Pydantic model for request body validation
class Item(BaseModel):
    name: str
    description: Optional[str] = None

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI"}

# Path Parameter Example
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}

# Post Request with Body
@app.post("/items/")
def create_item(item: Item):
    return {"name": item.name, "description": item.description}
```
2. Configuring CORS in FastAPI
```python
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# Allow specific origins
origins = [
    "http://localhost:3000",
    "[https://my-frontend-app.vercel.app](https://my-frontend-app.vercel.app)"
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,  # List of allowed domains
    allow_credentials=True,
    allow_methods=["*"],    # Allow all methods (GET, POST, etc.)
    allow_headers=["*"],    # Allow all headers
)
```

3. Vercel Configuration (vercel.json)
To deploy a Python app on Vercel, you need this configuration file in your root directory.

```JSON
{
  "builds": [
    {
      "src": "app.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "app.py"
    }
  ]
}
```
4. Deploying with Vercel CLI
```bash
# Install Vercel CLI (if using npm)
npm i -g vercel

# Login to Vercel
vercel login

# Deploy to Preview environment
vercel

# Deploy to Production
vercel --prod

```
5. Managing Secrets (Environment Variables)
Never hardcode API keys. Use a .env file locally and Vercel's Environment Variables dashboard for production.

Code:

```python
import os
from dotenv import load_dotenv

load_dotenv() # Load local .env file

api_key = os.getenv("OPENAI_API_KEY")
print(f"Key loaded: {api_key}")
```
Local .env file (Add to .gitignore!):

```plaintext
OPENAI_API_KEY=sk-proj-12345...
```

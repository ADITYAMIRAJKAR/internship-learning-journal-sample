# Week 2, Session 4

**Topic:** Project 1 Workflow, Advanced FastAPI & Automated Testing

---

## Concept Explanations

### 1. Project 1 Workflow (The "Red Chakra")
The instructor clarified the exact workflow for Project 1:
1.  **Submission:** We submit a Google Form with our **API Endpoint**, **GitHub Repo URL**, and a **Secret Code** (e.g., "92").
2.  **Round 1 (Creation):**
    * TDS Server sends a request to our API with the Secret Code and a "Task Brief" (e.g., "Create a calculator app").
    * Our API must **immediately return `200 OK`**.
    * Then, our API has **10 minutes** to:
        * Use an LLM (via API) to generate code for the task.
        * Create a **new public GitHub Repo**.
        * Push the generated code to that repo.
        * Deploy it to **GitHub Pages**.
    * Finally, our API sends a `POST` request back to the TDS Server with the new Repo URL.
3.  **Round 2 (Modification):** The TDS server sends a modification request (e.g., "Add scientific mode"). Our API repeats the process to update the repo/site.

### 2. FastAPI: Request Models & Validation
We moved beyond basic GET requests to using **Pydantic Models** for validation.
* **Pydantic:** A library to define data "shapes". If a user sends `{ "age": "twenty" }` but the model expects an integer, Pydantic automatically throws a clear error.
* **Response Model:** We can also define a model for what our API *returns*, filtering out secret internal data automatically.

### 3. File Uploads in FastAPI
We learned how to handle file uploads (Single and Multiple).
* **`UploadFile`:** A FastAPI type that handles file streams efficiently.
* **`await file.read()`:** Since file reading is an I/O operation, we use `await` to keep the server responsive (Asynchronous).

### 4. Automated Testing with Curl & Shell Scripts
Instead of manually clicking buttons in Postman for every change, the instructor demonstrated **Scripted Testing**.
* We generated a `curl` command for our endpoint using an LLM.
* We saved these commands into a `.sh` (Shell) script.
* Running `sh test.sh` instantly tests all endpoints and prints success/failure, saving massive amounts of time during development.

---

## Examples and Code Snippets

### 1. Pydantic Validation (Request Body)
```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr, Field

app = FastAPI()

# Define the "Shape" of data we expect
class User(BaseModel):
    username: str = Field(min_length=3, max_length=50)
    email: EmailStr  # Automatically validates email format
    age: int = Field(lt=120) # Must be less than 120

@app.post("/users/")
def create_user(user: User):
    # 'user' is already validated here
    return {"message": "User created", "data": user}
```

2. Handling File Uploads
```Python
from fastapi import FastAPI, UploadFile, File
from typing import List

app = FastAPI()

@app.post("/upload-files/")
async def upload_multiple_files(files: List[UploadFile] = File(...)):
    results = []
    for file in files:
        content = await file.read()
        results.append({
            "filename": file.filename,
            "size": len(content)
        })
    return {"uploaded": results}
```

3. Deployment Dockerfile (Hugging Face)
A Dockerfile to deploy this FastAPI app to Hugging Face Spaces.

```Dockerfile
# Use Python 3.11
FROM python:3.11

# Set working directory
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Run the application on port 7860 (Standard for Hugging Face)
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

4. Automated Testing Script (test.sh)
```bash
#!/bin/bash

# Test GET endpoint
echo "Testing Root Endpoint..."
curl -X 'GET' 'http://localhost:8000/' && echo " - Success" || echo " - Failed"

# Test User Creation (Valid)
echo "Testing Create User..."
curl -X 'POST' \
  'http://localhost:8000/users/' \
  -H 'Content-Type: application/json' \
  -d '{"username": "Sujal", "email": "test@example.com", "age": 21}'

# Test File Upload
echo "Testing File Upload..."
curl -X 'POST' \
  'http://localhost:8000/upload-files/' \
  -F 'files=@./test.txt'
```

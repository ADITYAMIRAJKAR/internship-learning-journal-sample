# Week 3, Session 2

**Topic:** Generating Embeddings, Multimodal Embeddings, and Basic RAG Implementation

---

## Concept Explanations

### 1. Generating Embeddings via API
Instead of running a heavy embedding model (like `sentence-transformers`) locally, we can consume embeddings via an API (like OpenAI's `text-embedding-3-small`).
* **Advantage:** Saves local compute resources (RAM/CPU).
* **Output:** A high-dimensional array of floats (e.g., 1536 dimensions for OpenAI).

### 2. Cosine Similarity (Mathematical Refresher)
To determine how similar two pieces of text are, we calculate the **Cosine Similarity** of their embeddings.
* It is essentially the **dot product** of the two vectors, normalized (divided by the product of their norms).
* **Result:** A value between `0` and `1`. A value closer to `1` means the texts are highly similar in meaning.

### 3. Multimodal Embeddings (Nomic API)
Traditional models embed text. **Multimodal models** can map *both* text and images into the *same* vector space.
* **Why it matters:** If an image of a cat and the word "cat" exist in the same mathematical space, you can search for images using text queries (like how Google Photos search works).
* **Tool Used:** Nomic AI API (allows generating embeddings for both text and images).

### 4. Basic RAG Implementation Steps
We built a miniature RAG (Retrieval-Augmented Generation) system from scratch.
1.  **Chunking:** Splitting a large dataset (e.g., TypeScript documentation) into smaller pieces (chunks) so they fit into the LLM's token limit.
2.  **Embedding:** Converting every chunk into a vector and storing it in a JSON file (acting as a basic Vector DB).
3.  **Querying:** Taking a user's question, embedding it, and calculating the Cosine Similarity against all stored chunks.
4.  **Retrieval:** Sorting the results and picking the top *N* chunks (the most relevant context).

---

## Examples and Code Snippets

### 1. Generating Embeddings via API (Python `httpx`)
```python
import httpx
import os

# Using the course's AI proxy
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
BASE_URL = "[https://api.aipipe.org/v1/embeddings](https://api.aipipe.org/v1/embeddings)"

def get_embedding(text):
    headers = {
        "Authorization": f"Bearer {OPENAI_API_KEY}",
        "Content-Type": "application/json"
    }
    payload = {
        "model": "text-embedding-3-small",
        "input": text
    }
    response = httpx.post(BASE_URL, headers=headers, json=payload)
    return response.json()["data"][0]["embedding"]

# Example usage
embed_apple = get_embedding("Apple")
```
2. Calculating Cosine Similarity
```Python
import numpy as np

def get_similarity(embed1, embed2):
    # Convert lists to numpy arrays
    v1 = np.array(embed1)
    v2 = np.array(embed2)
    
    # Calculate dot product
    dot_product = np.dot(v1, v2)
    
    # Calculate norms
    norm1 = np.linalg.norm(v1)
    norm2 = np.linalg.norm(v2)
    
    # Cosine Similarity Formula
    similarity = dot_product / (norm1 * norm2)
    return similarity

# Expected output: similarity between 'apple' and 'orange' > 'apple' and 'lightning'
```
3. Reading and Chunking JSONL (JSON Lines)
Real-world data is often stored in JSONL format, where each line is a separate JSON object.

```Python
import json

chunks = []
# Reading a file line by line
with open("typescript_docs.jsonl", "r") as f:
    for line in f:
        chunks.append(json.loads(line.strip()))
```

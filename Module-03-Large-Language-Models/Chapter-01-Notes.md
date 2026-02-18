# Week 3, Session 1

**Topic:** LLM Concepts, Embeddings, RAG, and AI Application Testing

---

## Concept Explanations

### 1. How LLMs Work (The "Black Box")
The instructor explained that LLMs are not sentient. They leverage **Transformers** and **Tokens**.
* **Tokens:** Inputs are broken down into tokens (parts of words).
* **Embeddings:** Each token is represented by a high-dimensional vector (e.g., 1,600 feature vector).
* **Self-Attention:** The model calculates the relationship (distance) between vectors to understand context (e.g., does "it" refer to the "animal" or the "road"?).
* **Probabilities:** It predicts the next token based on probabilities derived from these relationships.

### 2. The Context Problem
LLMs have a limited "Context Window" (memory). If a conversation goes too long, they "hallucinate" or forget previous details.
* **Solution:** Retrieval Augmented Generation (RAG) helps inject relevant context dynamically.

### 3. Embeddings & Vector Databases
* **Embeddings:** Converting text/images into numbers (vectors) so computers can compare their "meaning" mathematically.
* **Vector Databases:** Tools like ChromaDB, LanceDB, or pgvector are used to store these embeddings efficiently for quick retrieval.
* **Use Case:** Semantic search (searching by meaning, not just keywords).

### 4. RAG (Retrieval Augmented Generation)
RAG is the technique of fetching relevant data from a database and feeding it to the LLM along with the user's prompt.
* **Why?** It reduces hallucinations and allows the LLM to answer questions about private data (e.g., company PDFs) it wasn't trained on.

### 5. Hybrid RAG (TypeSense)
Sometimes pure semantic search fails (it finds "similar" concepts but misses specific keywords). **Hybrid RAG** combines:
* **Vector Search:** For meaning/context.
* **Keyword Search:** For exact matches.
* **Tool:** `TypeSense` is a popular open-source engine for this.

### 6. Function Calling (Intelligent Agents)
This is how we turn LLMs into "Agents" that can *do* things.
* Instead of just generating text, we give the LLM a **Schema** of functions (e.g., `book_flight(origin, destination)`).
* The LLM analyzes the user prompt ("Book me a flight to Delhi") and outputs a structured JSON object to call that function.
* The application executes the function and returns the result to the LLM to generate the final response.

### 7. LLM Evaluation (`promptfoo`)
How do we know if a new model version (e.g., GPT-4o vs GPT-3.5) breaks our app?
* **Eval Tools:** Tools like `promptfoo` allow us to define test cases (YAML file) to check:
    * **Accuracy:** Does the response contain specific keywords?
    * **Cost:** How many tokens did it use?
    * **Speed:** How fast was it?

---

## Examples and Code Snippets

### 1. Configuring LLM with Proxy Key
When using the course's AI Proxy, we must point the client to the correct base URL.

```python
import os
from openai import OpenAI

# Set the proxy URL (Very Important!)
base_url = "[https://api.aipipe.org/v1](https://api.aipipe.org/v1)" 
api_key = "YOUR_AI_PIPE_KEY"

client = OpenAI(
    base_url=base_url,
    api_key=api_key
)

response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "What is 2+2?"}]
)
print(response.choices[0].message.content)
```

2. Base64 Image Encoding (Vision Models)
To send images to an LLM via API, we often encode them as Base64 strings.

```Python
import base64

def encode_image(image_path):
    with open(image_path, "rb") as image_file:
        return base64.b64encode(image_file.read()).decode('utf-8')

# Usage in API call payload:
# {
#   "type": "image_url",
#   "image_url": {
#     "url": f"data:image/jpeg;base64,{base64_image}"
#   }
# }
```
3. Function Calling Schema Example
Telling the LLM about a function it can use.

```JSON
{
  "name": "get_weather",
  "description": "Get current weather for a location",
  "parameters": {
    "type": "object",
    "properties": {
      "location": {
        "type": "string",
        "description": "City and state, e.g. San Francisco, CA"
      },
      "unit": {
        "type": "string",
        "enum": ["celsius", "fahrenheit"]
      }
    },
    "required": ["location"]
  }
}
```

4. Promptfoo Configuration (promptfooconfig.yaml)
A simple test configuration to evaluate prompts.

```YAML
prompts: [
  "Write a tweet about {{topic}}"
]
providers: [
  "openai:gpt-4o-mini",
  "openai:gpt-3.5-turbo"
]
tests:
  - vars:
      topic: "Open Source"
    assert:
      - type: contains
        value: "community"
      - type: latency
        threshold: 1000 # Must be faster than 1s

```

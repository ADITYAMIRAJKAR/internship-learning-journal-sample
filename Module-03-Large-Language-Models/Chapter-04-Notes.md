# Week 3, Session 4

**Topic:** AI Chatbots with Memory, Base64 Image Processing, and Function Calling (Structured Outputs)

---

## Concept Explanations

### 1. How LLMs Understand Semantics (The "Child" Analogy)
The instructor used a brilliant analogy to explain Word Embeddings:
* Imagine a child is given an Apple and asked to place it in the house (Kitchen, Bedroom, or Hall).
* The child subconsciously evaluates features: *Is it eatable? Do I like it? Do my parents want it?*
* Based on these internal "scores", the child decides the most logical room.
* **Computer Parallel:** Computers do this mathematically using **Word Embeddings**. Words (like "Apple", "Fruit", "Cat") are converted into vectors (e.g., 1500 dimensions). The AI calculates the "distance" (Cosine Similarity) between these vectors to understand semantic meaning, rather than just matching spelling letters.

### 2. LLM Statelessness (Memory)
LLMs have **no memory**. If you ask a follow-up question, they won't remember the first one unless you explicitly send the entire conversation history back to them.
* **Roles in Messages:** To maintain a chat history, we pass a list of messages using specific roles:
    * `developer` (formerly `system`): Global instructions (e.g., "Answer in three words").
    * `user`: The human's input prompt.
    * `assistant`: The AI's previous responses.

### 3. Base64 Encoding for Vision Models
To send an image to an LLM via a REST API, we must convert the binary image file into a text-safe format.
* **Process:** Binary Data (0s and 1s) -> Base64 Encoding -> Long String of Characters.
* **Integrity:** Base64 is lossless. If you decode the Base64 string back to an image, the file hash (`sha256sum`) remains exactly the same as the original.

### 4. Function Calling (Structured Outputs)
Instead of getting a conversational paragraph from an LLM, we use **Function Calling** to force the AI to return data in a strict JSON format matching our defined schema.
* This is critical for automated pipelines (e.g., extracting an Expiry Date from an invoice and saving it straight to a database).

---

## Examples and Code Snippets

### 1. Chatbot Loop with Memory (`httpx`)
```python
import httpx
import os

API_KEY = os.getenv("OPENAI_API_KEY")
URL = "[https://api.aipipe.org/v1/chat/completions](https://api.aipipe.org/v1/chat/completions)" # Proxy URL

messages = [
    {"role": "developer", "content": "You are a helpful assistant. Keep answers brief."}
]

while True:
    user_query = input("You: ")
    if user_query.lower() == "exit":
        break
        
    # Append User Query
    messages.append({"role": "user", "content": user_query})
    
    payload = {
        "model": "gpt-4o-mini",
        "messages": messages
    }
    
    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    }
    
    response = httpx.post(URL, headers=headers, json=payload, timeout=15.0)
    ai_text = response.json()["choices"][0]["message"]["content"]
    
    print(f"AI: {ai_text}")
    
    # Append AI Response to maintain history
    messages.append({"role": "assistant", "content": ai_text})

```
2. Converting Image to Base64
```Python
import base64

def image_to_b64(image_path):
    with open(image_path, "rb") as f:
        binary_data = f.read()
        return base64.b64encode(binary_data).decode('utf-8')

b64_string = image_to_b64("product.png")
# Format required by OpenAI:
image_uri = f"data:image/png;base64,{b64_string}"
```

3. Defining a Function Calling Schema
```Python
tools = [
    {
        "type": "function",
        "function": {
            "name": "extract_product_info",
            "description": "Extract manufacturing date and expiry date from product image.",
            "parameters": {
                "type": "object",
                "properties": {
                    "mfd_year": {"type": "integer", "description": "Year of manufacturing"},
                    "exp_year": {"type": "integer", "description": "Year of expiry"},
                    "product_name": {"type": "string", "description": "Name of the product"}
                },
                "required": ["mfd_year", "exp_year", "product_name"]
            }
        }
    }
]

# Pass `tools=tools` and `tool_choice="required"` in the httpx payload.
```

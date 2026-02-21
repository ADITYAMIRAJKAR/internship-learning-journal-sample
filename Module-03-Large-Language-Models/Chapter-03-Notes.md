# Week 3, Session 3

**Topic:** Troubleshooting API Keys, Project 1 Clarifications, and Course Philosophy

---

## Concept Explanations

### 1. API Keys: AI Pipe vs. AI Proxy
A significant portion of the session was dedicated to troubleshooting Open AI API key errors (e.g., "API Key Expired"). 
* **The Core Issue:** Students often forget to replace the default OpenAI Base URL with the custom proxy URL provided by the course.
* **AI Pipe vs. AI Proxy:** Both are self-hosted proxy servers designed to bypass direct interaction with OpenAI, allowing students to access models without incurring personal costs. 
    * They serve the same conceptual purpose but might differ slightly in supported models or credit limits (e.g., AI Pipe offers a 10-cent limit, while Proxy offered $1 in previous terms).
* **Fix:** You must update both the `API_KEY` *and* the `BASE_URL` in your environment settings or code.

### 2. Project 1 Expectations & "2x2" Prerequisite Score
Clarifications were made regarding Project 1 submissions and grading.
* **The "2x2" Score:** Receiving a 2/2 on the initial submission does *not* mean you received full marks for the project. It is simply a prerequisite check confirming that your deployed application (Virtual TA) is "active" and the endpoint is reachable.
* **Actual Evaluation:** The actual score is determined later by an evaluation script that sends multiple hidden test questions to your active endpoint and verifies the accuracy of the LLM's responses based on the course content.

### 3. Career Value: What does this course add to a resume?
A student asked how this course translates to job interviews, especially for those without a heavy coding background.
* **Open Source & Portfolios:** The industry highly values visible contributions. This course teaches how to build, deploy, and host applications publicly (via GitHub, Hugging Face, etc.).
* **The "Virtual TA" Project:** Instead of just listing "Python" on a resume, you can link to a live deployed LLM application that answers questions based on a specific knowledge base (RAG).
* **Professional Workflow:** Learning to debug, use Git, collaborate, and manage cloud deployments mimics real-world Software Engineering and MLOps environments.

---

## Examples and Code Snippets

*Note: This session was primarily a Q&A and troubleshooting session, so no new code blocks were presented. However, the recurring issue with API configuration warrants a reminder snippet.*

### Reminder: Configuring the AI Proxy in Python
If you are getting "API Key Expired" or connection errors, ensure your setup looks like this:

```python
import os
from openai import OpenAI

# 1. Load the specific course token
api_key = os.getenv("OPENAI_API_KEY") # Ensure this is the AI Pipe token, NOT a real OpenAI key

# 2. OVERRIDE the default Base URL
base_url = "[https://api.aipipe.org/v1](https://api.aipipe.org/v1)" 

client = OpenAI(
    base_url=base_url,
    api_key=api_key
)

# 3. Make the request
response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Test prompt"}]
)
```

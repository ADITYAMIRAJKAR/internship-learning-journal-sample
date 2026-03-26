# Project: Local AI Document Quiz Generator 

**Module:** Large Language Models
**Status:** Completed

## Project Overview
As part of exploring Large Language Models, I built a full-stack, privacy-first web application. This project takes a user-uploaded PDF document, extracts the text, and uses a local LLM to dynamically generate a multiple-choice quiz. It also includes an automated grading system to evaluate the user's answers.

Because this utilizes [Ollama](https://ollama.com/), the entire AI pipeline runs 100% locally on the machine, meaning no document data is sent to external APIs.

## Tech Stack Used
* **Backend:** Python, FastAPI, Uvicorn
* **Frontend:** Vanilla HTML, CSS, JavaScript
* **AI Engine:** Ollama (Llama 3 model)
* **Document Processing:** PyPDF2

## Key Learnings & Challenges Solved

### 1. Connecting a Backend to a Local LLM
I successfully implemented an architecture where a Python backend (FastAPI) securely handles file uploads, parses the text, and communicates with a local LLM engine (Ollama) to generate structured JSON responses.

### 2. Overcoming LLM Hallucination (The "Yes Man" Effect)
**The Problem:** During the development of the grading endpoint, I encountered a major issue with Context Drift and Hallucination. The initial system prompt told the AI to act as an "encouraging tutor." Because of this persona, the LLM became a "Yes Man"—it incorrectly marked wrong answers as correct simply because they sounded plausible, ignoring the actual answer key.

**The Solution:** I applied prompt engineering techniques to fix this. I stripped away the persona and rewrote the system prompt to force the LLM to act as a "strict, objective automated grading system." I instructed it to perform a strict 1:1 comparison between the `user_answer` string and the `correct_answer` string. This completely eliminated the hallucination and resulted in 100% accurate grading.

## How to Run This Project
If you want to test this code locally:
1. Ensure Python and [Ollama](https://ollama.com/) are installed (`ollama pull llama3`).
2. Navigate to this folder in your terminal and install dependencies: `pip install -r requirements.txt`
3. Start the server: `uvicorn main:app --reload`
4. Open `index.html` in any web browser and upload a PDF.

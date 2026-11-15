# 🤖 Job-Helper AI Agent (ReWOO Architecture)

An autonomous AI agent built with **LangGraph** and **LangChain** implementing the **ReWOO (Reasoning WithOut Observation)** paradigm to evaluate CVs against live job postings.

## 🧠 Architecture Overview
Unlike traditional **ReAct** agents that invoke the LLM after every single tool execution, **ReWOO** decouples reasoning from observation into three specialized nodes:
1. **Planner Node:** Generates a complete, step-by-step execution plan upfront using variable placeholders (`#E1`, `#E2`, `#E3`).
2. **Executor (Tool) Node:** Loops through the plan steps, resolves variable dependencies, and executes external tools (`extract_cv_text`, `job_posting_tool`) without redundant LLM calls.
3. **Solver Node:** Synthesizes the initial plan and all collected evidence into a final, actionable candidate-job fit evaluation.

## 🛠️ Tech Stack & Tools
- **Orchestration:** LangGraph (`StateGraph`, conditional routing)
- **LLM:** Groq API (`openai/gpt-oss-120b`)
- **Observability:** LangSmith tracing (`@traceable`)
- **Custom Tools:**
  - `extract_cv_text`: Extracts structured text from `.pdf`, `.docx`, and `.doc` résumés using `pdfplumber` and `python-docx`.
  - `job_posting_tool`: Scrapes and summarizes live job requirements using `BeautifulSoup4` and `requests`.

## 🚀 How to Run
1. Install dependencies:
   ```bash
   pip install langgraph langchain-groq langchain-core pdfplumber python-docx beautifulsoup4 requests langsmith
   ```
2. Set your environment variables:
   ```bash
   export GROQ_API_KEY="your_groq_api_key"
   export LANGSMITH_API_KEY="your_langsmith_api_key" # Optional
   ```
3. Place your CV file (e.g., `cv-template.pdf`) in the root directory and run `ReWOO_Agent.ipynb`.

# 🏥 Medical Research Assistant Agent (with Persistent Memory)

> A work in progress — features will continue to be added over time.

---

## 📌 Overview
An AI-powered medical research assistant that uses a ReAct agent to answer research questions, calculate drug dosages, search for drug interactions, and remember research context across sessions. Built with LangChain, LangGraph, FAISS, Groq, and SQLite.

---

## 🚀 Features

- **Document Search** — searches loaded medical PDFs for relevant research context
- **Dosage Calculator** — calculates total drug dosage given patient weight and dose per kg
- **Drug Interaction Search** — searches the web for interactions between specified drugs
- **Persistent Memory** — remembers research topics, unresolved questions, and user preferences across sessions
- **Auto Open Threads** — automatically flags incomplete answers as unresolved questions to revisit
- **Thread Resolution** — marks questions as resolved when a complete answer is found
- **Source Attribution** — every answer is traced back to its source (PDF, internet search, or calculator)

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Groq (llama-3.3-70b-versatile) | LLM inference |
| LangGraph `create_react_agent` | ReAct reasoning agent |
| FAISS | Vector similarity search |
| HuggingFace `sentence-transformers/all-MiniLM-L6-v2` | Text embeddings |
| DuckDuckGo Search | Live internet search fallback |
| PyPDFLoader | PDF document loading |
| SQLite + `SqliteSaver` | Persistent memory across sessions |

---

## 🧠 Key Concepts Demonstrated

- **RAG Pipeline** — documents are chunked, embedded, and stored in FAISS for similarity search
- **Tool Calling** — agent decides which tool to use based on the question
- **ReAct Reasoning** — think, act, observe, repeat until a final answer is reached
- **Persistent Memory** — SQLite database survives session restarts, agent remembers past context
- **Silent Context Injection** — past research shapes responses without announcing itself
- **Source Attribution** — every answer includes where the information came from

---

## 🗄️ Memory Architecture

The memory system uses three SQLite tables:

| Table | Purpose |
|---|---|
| `research_context` | Tracks research topics and details explored across sessions |
| `open_threads` | Tracks unresolved questions to revisit in future sessions |
| `user_preferences` | Tracks how the researcher likes answers structured |

### How memory works:
- **Silent context** — past research is injected into every question without announcing it
- **Auto-save** — incomplete answers are automatically saved as open threads
- **Auto-resolve** — complete answers automatically close matching open threads
- **Survives restarts** — SQLite database persists across Google Colab session restarts

---

## 📓 Notebook
Built in a single Google Colab notebook. Cells are organized sequentially — installations, imports, setup, memory, tools, and main(). Will be refactored into a Python package in a future version.

---

## ⚙️ Setup

### 1. Install dependencies
```bash
pip install langchain langchain-groq langchain-community langchain-huggingface
pip install langgraph faiss-cpu sentence-transformers pypdf duckduckgo-search
pip install langgraph-checkpoint-sqlite
```

### 2. Set your Groq API key
```python
# In Google Colab, use Colab secrets
from google.colab import userdata
api_key = userdata.get('YOUR_GROQ_API_KEY')
```

### 3. Add your medical PDF
```python
pdf_paths = ["/content/your_medical_document.pdf"]
```

### 4. Run
```python
main()
```

---

## 🧪 Example Questions

```python
questions = [
    "What should I do before I start research?",
    "What is the dosage for a 70kg patient at 5mg/kg?",
    "What are the interactions between aspirin and ibuprofen?"
]
```

### Sample Output
```
Question: What should I do before I start research?
Answer: Before starting research, define a clear research question,
conduct a systematic literature review, and develop a protocol...
Source: PDF Document

Question: What is the dosage for a 70kg patient at 5mg/kg?
Answer: 350.0mg
Source: Dosage Calculator

Question: What are the interactions between aspirin and ibuprofen?
Answer: Taking aspirin and ibuprofen together increases the risk of
stomach ulcers and bleeding...
Source: Internet Search

📌 Open thread saved: 'What should I do before I start research?'
```

---

## 🐛 Known Issues & Fixes

| Issue | Cause | Fix |
|---|---|---|
| `InvalidUpdateError` | LangGraph expects dict, not string | Changed `agent.invoke(query)` to `agent.invoke({"messages": [...]})` |
| `GraphRecursionError` | Agent looping without stopping | Added `recursion_limit` config and simplified system prompt |
| Source hallucination | Agent claiming PDF source when no PDF loaded | Added `None` check in `search_documents` before searching |
| Tokens exhausted quickly | `summarize_with_retry` calling LLM per chunk | Removed summarization, embedded raw chunks directly |
| Similarity search error | `similarity_search` returns docs not tuples | Changed to `similarity_search_with_score` |
| PDF lost after restart | Google Colab doesn't persist files | Reupload PDF or mount Google Drive |

---

## 🗺️ Roadmap

- [ ] Upgrade to `StateGraph` with custom nodes and conditional edges
- [ ] Semantic memory — FAISS index for smarter context retrieval
- [ ] Conflict detection — surface when new findings contradict past conclusions
- [ ] Multi-PDF support — load entire research libraries
- [ ] FastAPI wrapper — expose agent as a REST API
- [ ] Streamlit UI — browser-based interface for researchers

---

## 👤 Author
**Precious**
Building towards a Forward Deployed Engineer role — one agent at a time.

> These projects are my baby steps. Unique projects with features you won't find in typical AI portfolios are coming next.

---

## ⚠️ Disclaimer
This tool is for research and educational purposes only. It is not a substitute for professional medical advice.

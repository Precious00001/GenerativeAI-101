# Agentic AI Portfolio

A collection of agentic AI projects built while developing expertise 
in LLM-powered autonomous systems, RAG pipelines, and multi-tool agents.

## Projects

### 1. Medical Research Assistant
An agentic AI system that answers medical questions using RAG and web search.

- RAG pipeline with FAISS vector store
- Tools: document search, dosage calculator, drug interaction lookup
- Hybrid search: internal PDFs first, Tavily web search fallback
- [View Project](./medical-research-assistant/v1.0/)

### 2. Legal Document Research Assistant
An agentic AI system that helps lawyers research case-relevant information.

- RAG pipeline with FAISS vector store
- Tools: case summariser, deadline calculator
- Hybrid search: internal PDFs first, DuckDuckGo web search fallback
- [View Project](./legal-document-research-assistant/v1.0/)

## Tech Stack
- **LLM:** llama-3.1-8b-instant and llama-3.3-70b-versatile  via Groq
- **Embeddings:** HuggingFace sentence-transformers
- **Vector Store:** FAISS
- **Framework:** LangChain + LangGraph
- **Web Search:** Tavily, DuckDuckGo

## Concepts Demonstrated
- ReAct agent loop
- RAG pipelines
- Hybrid search with confidence scoring
- Multi-tool agents
- Agentic fallback patterns

## About
Built as part of the roadmap toward Forward Deployed Engineer 
proficiency in agentic AI systems.

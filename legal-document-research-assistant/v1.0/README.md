# Legal Document Research Assistant v1.0

## What it does
An agentic AI system that helps lawyers research case-relevant information.

## Tools
- calculate_deadline — computes response deadlines given a filing date and jurisdiction
- summarize_case — retrieves case summaries from loaded PDFs, falls back to web search

## Stack
- LLM: Llama 3.3 70B via Groq
- Embeddings: HuggingFace sentence-transformers
- Vector store: FAISS
- Framework: LangChain + LangGraph ReAct agent
- Web search: DuckDuckGo

## Setup
Add your GROQ_API_KEY to Colab secrets before running.

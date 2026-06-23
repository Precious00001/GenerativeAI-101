# Medical Research Assistant v1.0

## What it does
An agentic AI system that answers medical questions using RAG and web search.

## Tools
- search_documents — retrieves context from loaded medical PDFs via FAISS
- dosage_calculator — computes dosage based on patient weight and dose per kg
- search_drug_interactions — searches the web for drug interaction data

## Stack
- LLM: Llama 3.3 70B via Groq
- Embeddings: HuggingFace sentence-transformers
- Vector store: FAISS
- Framework: LangChain + LangGraph ReAct agent
- Web search: Tavily

## Setup
Add your GROQ_API_KEY and TAVILY_API_KEY to Colab secrets before running.

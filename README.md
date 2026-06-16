# Medical Research Assistant Agent

An agentic AI system that answers medical questions using RAG and web search.

## Tools
- search_documents — retrieves context from a loaded medical PDF via FAISS
- dosage_calculator — computes dosage based on patient weight
- search_drug_interactions — searches the web for drug interaction data

## Stack
- LLM: Llama 3.3 70B via Groq
- Embeddings: HuggingFace sentence-transformers
- Vector store: FAISS
- Framework: LangChain + LangGraph ReAct agent

## Setup
Add your GROQ_API_KEY to Colab secrets before running.

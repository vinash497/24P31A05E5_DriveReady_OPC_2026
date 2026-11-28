# Day 5 – Business Knowledge Agent

## Project Overview
This project implements a business knowledge assistant using a vector database and an AI-powered conversational agent. It retrieves relevant business information from stored documents and answers user questions based on the available knowledge.

## Technologies Used
- Python
- Groq API – LLM
- LangChain
- LangGraph
- ChromaDB – Vector Database
- Hugging Face Sentence Transformers – Embeddings
- Google Colab

## Implementation

### 1. Business Knowledge Storage
- Collected 15–20 business facts.
- Stored each fact as an individual document chunk.
- Generated embeddings using Hugging Face.
- Stored the vectors in ChromaDB.

### 2. Search Tool
Created `search_business_knowledge`, a retrieval tool that searches the business knowledge database using semantic similarity.

Topics covered include:
- Business name and location
- Business type and history
- Products and services
- Business owner
- Working hours
- Contact information
- Pricing and payment methods
- Customer support
- Delivery
- Special offers
- Business policies

### 3. Agent Integration
Integrated the search tool into the LangGraph agent. The agent uses the Groq language model and invokes the search tool to retrieve business information.

### 4. Conversation Memory
Implemented a LangGraph checkpointer using thread IDs to maintain conversation history and isolate separate conversations.

### 5. Hallucination Prevention
Added system instructions to ensure that:
- Business answers are grounded in retrieved information.
- Missing information is not invented.
- Unsupported questions receive an appropriate response.

## Project Files
- `business_facts.py` – Business information.
- `vector_store.py` – Embedding generation and ChromaDB storage.
- `search_tool.py` – Business knowledge retrieval tool.
- `agent.py` – LangGraph agent and conversation memory.


## Conclusion
Successfully developed and tested a business knowledge agent that retrieves information from a ChromaDB vector database, uses an LLM for conversational responses and maintains separate conversation histories through LangGraph checkpointers.

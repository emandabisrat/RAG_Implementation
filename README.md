# RAG Assistnat For Technical Papers

**Author:** Emanda Bisrat

---

## Overview

This project is a lightweight Retrieval-Augmented Generation (RAG) system designed to answer questions about technical AI research papers. The goal is to explore how well a large language model (LLM) pipeline can retrieve, synthesize, and generate accurate responses from dense academic documents.

In addition to building the system, I evaluate its performance to understand where it succeeds and where it fails, particularly in terms of retrieval quality vs. generation quality.

---

## Pipeline

### 1. Document Ingestion and Chunking

* Loaded two AI research PDFs using LangChain
* Split documents into overlapping chunks to preserve semantic meaning
* Chunk size: **400 tokens**
* Overlap: **100 tokens**

---

### 2. Embedding and Vector Storage

* Used `all-MiniLM-L6-v2` sentence-transformer model to generate embeddings
* Stored embeddings in a **ChromaDB** vector database
* Enabled efficient semantic similarity search over document chunks

---

### 3. Retrieval Layer

* Implemented a top-k retriever with **k = 4**
* Added lightweight filtering to remove noisy or irrelevant chunks (e.g., citations, references)

---

### 4. Generation Layer

* Used a local **FLAN-T5-base** model for answer generation
* Prompt engineered to improve output quality:

  * Enforced context-grounded responses
  * Prevented direct copying from source text
  * Encouraged concise answers (2–4 sentences)
  * Included fallback behavior: *“not found in the provided text”* when applicable

---

## Evaluation Approach

The system was evaluated using **RAGAS**, focusing on four key metrics:

1. **Faithfulness** – Is the answer grounded in retrieved context?
2. **Answer Relevancy** – Does the response actually address the question?
3. **Context Precision** – How relevant is the retrieved context?
4. **Context Recall** – Was all necessary information retrieved?


## Key Takeaways

* Retrieval quality alone is not sufficient for a strong RAG system
* Generation quality is often the limiting factor in small-model pipelines
* Metric-driven evaluation (e.g., RAGAS) is essential for debugging failures
* Conceptual reasoning remains a major challenge for smaller LLMs

---

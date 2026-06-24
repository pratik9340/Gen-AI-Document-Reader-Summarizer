# Local RAG Pipeline using Ollama + ChromaDB + Gemma3

## Overview

This project implements a Retrieval-Augmented Generation (RAG) pipeline entirely locally.

## Overall Workflow:

PDF → Chunking → Embedding → ChromaDB → Retrieval → Re-Ranking → Gemma3 → Answer

1. Reads PDF documents
2. Extracts text, images, tables, and metadata
3. Splits content into semantic chunks
4. Generates embeddings using Ollama
5. Stores vectors inside ChromaDB
6. Retrieves relevant chunks using semantic search
7. Re-ranks results
8. Sends context to Gemma3
9. Config & Gaudrails
10. Observability & Evaluation

## Components

### PDF Loaders
Purpose: Load and extract information from documents.

* load PDF
* extract images
* extract tables
* extract metadata

### Chunking
Purpose: Split documents into chunks suitable for embedding with chunk_size=1000 and chunk_overlap=200.
The chunk size is limited to the model token size and the overlap needed to maintain contextual coherence.

Use Cases:
* recursive_chunking()
* semantic_chunking()
* token_chunking()
  
### Embeddings Vecotr
Purpose: Generate dense vector representations for each word.

Use Cases:
* Semantic search
* Similarity matching

### Vector DB Store
Purpose: Store embeddings in ChromaDB. This stores the 768-dimensional vector.

Use Cases: 
* Persistent vector storage

### Eetrieverval 
Purpose: Retrieve relevant chunks from the vector DB based on the user query embeddings.

Use Cases:
* Question answering
* Context retrieval

### Re-ranker
Purpose: Improve retrieval quality.
Functions: rerank_documents()

Use Cases:
* Remove noisy chunks
* Improve relevance

### Generation  
Purpose: Invoking LLM locally using ollama and generating output using retrieve douments
Functions:  build prompt, generate response

Use Cases:
* Grounded answer generation

Real-world Use Cases:

* Long documents
* Better retrieval accuracy
* Technical PDFs
* Research papers
* Manuals
* Financial reports

### Config & Gaudrails
### Observability & Evaluation

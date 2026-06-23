# Local RAG Pipeline using Ollama + ChromaDB + Gemma3

## Overview

This project implements a Retrieval Augmented Generation (RAG) pipeline completely locally.

## Overall Workflow:

PDF → Chunking → Embedding → ChromaDB → Retrieval → Re-Ranking → Gemma3 → Answer

The pipeline:

1. Reads PDF documents
2. Extracts text, images, tables and metadata
3. Splits content into semantic chunks
4. Generates embeddings using Ollama
5. Stores vectors inside ChromaDB
6. Retrieves relevant chunks using semantic search
7. Re-ranks results
8. Sends context to Gemma3
9. Generates grounded answers

## Components

### loaders.py
Purpose: Load and extract information from documents.

* load PDF
* extract images
* extract tables
* extract metadata

### chunking
Purpose: Split documents into chunks suitable for embedding.
Functions: split_documents(documents,chunk_size=1000,chunk_overlap=200):

Use Cases:
* recursive_chunking()
* semantic_chunking()
* token_chunking()
  
### embeddings
Purpose: Generate dense vector representations.
Functions: generate_embeddings(model_name, documents)

Use Cases:
* Semantic search
* Similarity matching

### vector_store
Purpose: Store embeddings in ChromaDB.
Functions: initialize_vector_store --> add_documents_to_vectorstore(collection, documents, embeddings):

Use Cases: 
* Persistent vector storage

### retrieverval 
Purpose: Retrieve relevant chunks.
Functions: retrieve_documents(query)

Use Cases:
* Question answering
* Context retrieval

### reranker
Purpose: Improve retrieval quality.
Functions: rerank_documents()

Use Cases:
* Remove noisy chunks
* Improve relevance

### llm invoke 
Purpose: Invoking LLM locally using ollama to interact with Gemma3.
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

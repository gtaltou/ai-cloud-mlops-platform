# RAG Architecture

```mermaid
flowchart LR

    Documents

    Documents --> Ingestion

    Ingestion --> Chunking

    Chunking --> Embeddings

    Embeddings --> VectorDB

    UserQuestion --> Retriever

    Retriever --> VectorDB

    VectorDB --> Context

    Context --> LLM

    LLM --> Response
```
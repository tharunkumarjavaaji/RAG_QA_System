# Offline Multi-Document QA

This project is a local-first, offline-capable question answering system for personal document collections. It combines lexical BM25-style ranking with semantic embeddings, stores documents and chunks persistently in SQLite, and only returns answers grounded in retrieved passages with citations.

#Abstract
The rapid growth of digital documents across academic, research, and organizational domains has made efficient information retrieval increasingly challenging. Traditional keyword-based search systems rely on exact word matching and fail to capture the semantic meaning of user queries, often resulting in irrelevant or incomplete results. This forces users to manually search through large volumes of text, reducing productivity and increasing the effort required to find accurate information. Recent advancements in artificial intelligence have introduced modern Question Answering (QA) systems that improve contextual understanding using large language models. However, most of these systems depend on cloud-based services and proprietary APIs, which raise concerns regarding data privacy, lack of transparency, high operational costs, and continuous internet dependency.
To overcome these limitations, this project proposes an offline Retrieval-Augmented Generation (RAG)-based Question Answering system. The system integrates semantic embeddings, BM25 lexical ranking, and CHORMADB-based vector indexing to retrieve relevant information and generate accurate, context-aware answers grounded in documents. It also provides source citations, multi-document support, and explainable ranking mechanisms. These features ensure transparency, reliability, and data security, making the system suitable for academic, research, and enterprise environments requiring privacy-preserving and efficient information retrieval.

## Features

- Offline document ingestion for `.txt`, `.md`, `.pdf`, and `.docx`
- User authentication with salted password hashing
- Persistent SQLite storage for users, documents, chunks, and sessions
- Hybrid retrieval that combines lexical and semantic scores
- Citation-based answer generation from retrieved document chunks
- Minimal web UI for upload, search, and answer review

## Run

1. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

2. Start the application:

```bash
python run.py
```

3. Open `http://127.0.0.1:8010`

If you prefer `uvicorn`, run it from this exact folder and use a free port:

```bash
python -m uvicorn app.main:app --host 127.0.0.1 --port 8010
```

## Notes

- The app is designed for offline use after dependencies and the embedding model are available locally.
- `sentence-transformers` will try to load `all-MiniLM-L6-v2`. For fully offline deployment, pre-download that model on the target machine or point the code to an already cached local model.
- If the embedding model cannot be loaded, the app falls back to a deterministic local embedding approximation so retrieval still works, though with reduced semantic quality.

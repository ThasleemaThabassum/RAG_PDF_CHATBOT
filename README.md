# 📄 RAG PDF Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that lets you upload any PDF and ask questions about its content — answered strictly from the document, not general knowledge.

🔗 **Live Demo:** [bd3d5ada8b33f425de.gradio.live](https://bd3d5ada8b33f425de.gradio.live/)
*(Note: Gradio share links are temporary and expire after the session ends — see below for local setup.)*

## How It Works

1. **Upload** a PDF — text is extracted page by page using `pypdf`
2. **Chunk** the text into overlapping segments for better context retrieval
3. **Embed** each chunk using `sentence-transformers` (`all-MiniLM-L6-v2`)
4. **Store** embeddings in `ChromaDB`, a vector database, for fast semantic search
5. **Query** — your question is embedded and matched against the most relevant chunks
6. **Generate** — the top-matching context is passed to Google's `Gemini 2.5 Flash` model, which answers using only that context

## Tech Stack

- **Frontend:** Gradio (Blocks UI, custom theme)
- **Vector DB:** ChromaDB
- **Embeddings:** Sentence-Transformers (MiniLM)
- **LLM:** Google Gemini 2.5 Flash
- **PDF Parsing:** pypdf

## Setup

```bash
pip install -r requirements.txt
```

Add your Gemini API key as an environment variable / Colab secret named `GEMINI_API_KEY`, then run:

```bash
python app.py
```

## Demo

Tested using a Data Engineering course PDF — asked questions like:
- What is the Data Engineering lifecycle?
- What are the steps in the DE lifecycle?
- Data Engineer vs Data Scientist
- What is data maturity?

The chatbot correctly answered all queries, grounded entirely in the uploaded document.

## Future Improvements

- Support for multiple PDFs / persistent storage
- Chat history / conversational memory
- Source citation (which page/chunk the answer came from)

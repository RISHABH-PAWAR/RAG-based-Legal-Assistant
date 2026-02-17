# ⚖️ RAG-Based Legal Assistant Chatbot

A **context-aware legal assistant** built using **LangChain** and an advanced **Retrieval-Augmented Generation (RAG)** pipeline.  
The system answers legal questions by grounding responses in relevant legal documents using **hybrid retrieval** and **query-aware reasoning**.

---

## 🚀 Why this project?

Most legal chatbots fail because they:
- retrieve duplicate or irrelevant context
- rely on a single retrieval strategy
- break on complex, multi-document questions

This project fixes that.

---

## 🧠 Core Features

- 📄 **PDF Ingestion** – Parses and indexes legal PDF documents  
- 🔎 **Hybrid Retrieval**
  - **BM25** for exact keyword matches  
  - **FAISS + embeddings** for semantic search  
- 🧩 **Query Complexity Detection** – Adapts retrieval strategy automatically  
- 🔁 **Multi-Query Retrieval** – Expands queries to improve recall  
- 🪜 **Multi-Hop Retrieval** – Chains information across documents  
- 🧮 **Reciprocal Rank Fusion (RRF)** – Merges results from multiple retrievers  
- 💬 **Conversation Awareness** – Custom chat history handling  
- ⚠️ **Legal Disclaimer** – Responses are not legal advice  

---

## 🛠️ Tech Stack

| Component | Technology |
|--------|------------|
| Framework | LangChain |
| Embeddings | all-MiniLM-L6-v2 |
| Vector Store | FAISS |
| Sparse Search | BM25 |
| LLM | Cohere (command-r) |
| Evaluation | RAGAS |
| Tracing | LangSmith |
| Interface | CLI |

---

## 📂 Project Structure

```text
RAG-based-Legal-Assistant/
├── backend/                     # FastAPI backend
│   ├── main.py                 # API endpoints
│   └── rag_service.py          # RAG service logic
├── frontend/                    # React + Vite frontend
│   ├── src/
│   │   ├── components/         # UI components
│   │   ├── pages/             # Page components
│   │   ├── api/               # API client
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── data/                       # Legal PDF documents & vectors
│   ├── raw/                    # Source PDF files
│   └── vectors/                # FAISS index & embeddings
├── modules/                    # Core RAG pipeline logic
│   ├── bm25_retriever.py      # Sparse keyword-based retrieval
│   ├── semantic_retriever.py   # Dense vector retrieval (FAISS)
│   ├── multi_query_retriever.py
│   ├── multi_hop_retriever.py
│   ├── rrf_score.py           # Reciprocal Rank Fusion logic
│   ├── decide_query_complexity.py
│   ├── preprocess_documents.py
│   ├── conversation_history.py
│   └── chatbot_response.py
├── prompts/                    # Prompt templates
├── outputs/                    # Demo outputs
├── RAGAS-dataset/              # Evaluation datasets & scores
├── app.py                      # CLI application entry point
├── requirements.txt            # Python dependencies
└── README.md
```




---

## ⚙️ Setup

### Requirements
```bash
python >= 3.12
Installation (Recommended)
git clone https://github.com/RISHABH-PAWAR/RAG-based-Legal-Assistant.git
cd RAG-based-Legal-Assistant
uv sync

🔐 Environment Variables
Create a .env file:

COHERE_API_KEY=your_api_key
OPENAI_API_KEY=optional

▶️ Run the App
uv run app.py
Ask legal questions in the terminal.
Type exit to quit.
```

🧪 Evaluation

-Retrieval and generation quality are evaluated using RAGAS.

-Scores and datasets are available in RAGAS-dataset/.

👤 Author
Rishabh Pawar
🔗 https://github.com/RISHABH-PAWAR



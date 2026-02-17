# ⚖️ RAG-Based Legal Assistant Chatbot

A powerful, context-aware legal assistant chatbot built with **LangChain** and advanced **Retrieval-Augmented Generation (RAG)** techniques.

The application combines **dense and sparse retrieval** by leveraging traditional **BM25-based keyword search** alongside **semantic vector search**, ensuring both lexical precision and deep contextual relevance. It intelligently analyzes the complexity of each user query and dynamically selects the most appropriate retrieval strategy.

For complex reasoning tasks, the system employs **Multi-Hop retrieval** across multiple documents, while **Multi-Query retrieval** is used as a semantic query expansion technique to improve recall and coverage. Results from these retrieval strategies are consolidated using **Reciprocal Rank Fusion (RRF)**, ensuring that the most contextually relevant documents are prioritized and passed to the language model as grounding context for response generation.

Additionally, the application includes a **custom-built chat history management module**, developed as a robust replacement for LangChain’s deprecated `ConversationSummaryBufferMemory`. This module reliably maintains conversational context across interactions without relying on unstable or deprecated abstractions.

---

## 🚀 Why this project?

Most legal chatbots fail because they:
- Retrieve duplicate or irrelevant context
- Rely on a single retrieval strategy
- Break on complex, multi-document questions

This project fixes that.

---

## 🧠 Core Features

- **PDF Document Processing**: Automatically processes and indexes legal PDF documents
- **Sparse (BM25) Retriever**: keyword-based retrieval method that ranks documents using term frequency and inverse document frequency to capture exact lexical matches between the query and documents
- **Dense Retriever**: FAISS-backed vector retriever with the `all-MiniLM-L6-v2` sentence transformer embedding model to perform semantic similarity search, retrieving documents based on contextual meaning rather than exact keyword matches
- **Multi-Query Retrieval**: Semantic query expansion strategy that generates multiple paraphrased or reformulated queries from the original user input to improve retrieval recall and coverage.
- **Multi-Hop Retrieval**: Decomposes a complex query into intermediate steps, retrieving and chaining context from multiple documents to enable reasoning across dispersed information sources
- **Reciprocal Rank Fusion (RRF)**: Merges results from multiple retrieval methods by prioritizing documents that consistently rank highly across different retrievers
- **Intelligent Query Classification**: Determines whether document retrieval is needed based on the complexity inferred
- **Conversation History Awareness**: Maintains conversation context across multiple turns
- **Vector Database Storage**: Efficiently stores and retrieves document embeddings using FAISS
- **Command-Line Interface**: Interactive terminal-based chat interface
- **Responsible AI Disclaimers**: Clearly communicates that responses are not substitutes for legal advice 

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

## How It Works

The application uses an advanced RAG pipeline with several sophisticated components:

### 1. **Document Processing**:
   - Loads PDF documents from the data directory using PyPDFLoader
   - Splits documents into manageable chunks using RecursiveCharacterTextSplitter
   - Creates embeddings using HuggingFace's `all-MiniLM-L6-v2` model
   - Stores embeddings in ChromaDB for efficient retrieval

### 2. **Query Processing & Retrieval**:
   - **Complexity Classification**: Uses a Pydantic model to determine the complexity of a user query.
   - **Multi-Query Generation**: For "complex" queries, generates multiple semantically equivalent variations and retrieves respective relevant documents.
   - **Multi-hop Retrieval**: Decomposes a "super_complex" user query into a sequence of intermediate sub-queries, iteratively retrieving and linking information from multiple documents so that context gathered in earlier steps guides subsequent retrieval for deeper, cross-document reasoning.
   - **Irrelevant Query Handling**: In case of an "Irrelevant" query, it simply returns a hard-coded instruction to guide the user to ask only legal questions.
   - **Reciprocal Ranking Fusion(RRF)**: Combines ranked results from multiple retrieval strategies by assigning higher importance to documents that appear consistently near the top across retrievers, producing a more robust and contextually relevant final document ranking.
   - **Conversational Awareness**: Incorporates chat history for contextual understanding.

### 3. **Response Generation**:
   - Uses Cohere's language model for generating responses
   - Provides clear, concise answers based on retrieved context
   - Maintains conversation history for follow-up questions
   - Includes appropriate legal disclaimers

🧪 **Evaluation**

-Retrieval and generation quality are evaluated using RAGAS.
-Scores and datasets are available in RAGAS-dataset/.

👤 Author
Rishabh Pawar
🔗 https://github.com/RISHABH-PAWAR



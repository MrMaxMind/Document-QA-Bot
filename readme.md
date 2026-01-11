# 📚 Document QA Bot – Intelligent Document Assistant

An interactive **Document Question Answering (QA) Bot** built using **Retrieval-Augmented Generation (RAG)**.
This Streamlit application allows users to upload documents and ask natural-language questions, receiving accurate, context-grounded answers powered by **Groq LLMs**, **Pinecone vector search**, and **SentenceTransformer embeddings**.

---

## 🧠 Architecture Overview

**RAG Pipeline**

```
Document Upload
   ↓
Text Extraction & Chunking
   ↓
Sentence Embeddings (MiniLM)
   ↓
Vector Storage (Pinecone)
   ↓
Query → Top-K Retrieval
   ↓
Groq LLM Answer Generation
```

**Core Stack**

* 🔑 **Groq Cloud** – Fast LLM inference (Mixtral 8x7B)
* 🗄️ **Pinecone** – Scalable vector database
* 🧠 **SentenceTransformer** – Semantic embeddings
* 🎛️ **Streamlit** – Interactive UI

---

## ✨ Features

* 📄 Multi-format document support (PDF, DOCX, TXT, MD)
* 🔍 Semantic document indexing and retrieval
* 💬 Conversational Q&A grounded in document content
* 📊 Context inspection with relevance scores
* ⚙️ Configurable retrieval parameters (Top-K)
* 🧪 Experimental support for additional formats via `textract`

---

## 📂 Supported Document Formats

| Format | Engine      | Notes                        |
| ------ | ----------- | ---------------------------- |
| PDF    | PyPDF2      | Text-based PDFs only         |
| DOCX   | python-docx | Ignores complex formatting   |
| TXT    | Native      | UTF-8 encoding required      |
| MD     | Native      | Markdown parsed as text      |
| Other  | textract    | Requires system dependencies |

---

## 🚀 Getting Started

### Prerequisites

* Python **3.7+**
* 🔑 **Groq API Key** – [https://console.groq.com](https://console.groq.com)
* 🗄️ **Pinecone API Key** – [https://pinecone.io](https://pinecone.io)
* Modern web browser (Chrome / Firefox / Edge)

---

## 🔧 Installation

1. Clone the repository:

```bash
git clone https://github.com/marvlyngkhoi/RAG_CHATBOT.git
cd document-qa-bot
```

2. Create and activate a virtual environment *(recommended)*:

```bash
python -m venv venv
source venv/bin/activate    # Windows: venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

**Example `requirements.txt`:**

```
streamlit
groq
pinecone-client
sentence-transformers
PyPDF2
python-docx
textract
```

---

## ▶️ Running the Application

```bash
streamlit run app.py
```

Open your browser at:

```
http://localhost:8501
```

---

## ⚙️ Configuration Walkthrough

### Step 1: API Setup (Sidebar)

* 🔑 Enter **Groq API Key**
* 🗄️ Enter **Pinecone API Key**
* 🧠 Index Name: `rag-doc` *(default)*
* 🔍 Top-K Results: **3–5 recommended**
* Click **Initialize**

> The system automatically:

* Verifies API connectivity
* Creates a **384-dim cosine index**
* Loads embedding & LLM models

---

## 📤 Document Processing Flow

1. Upload a document *(≤ 200MB)*
2. Text extraction & paragraph chunking
3. Embedding generation
4. Pinecone index population

**⏱️ Performance**

* ~1–2 seconds per page (CPU extraction)
* ~5 ms per chunk (embedding generation)

---

## 💬 Interactive Q&A Interface

**Example**

```
User: What are the main risk factors?
Bot:
The document identifies three primary risks:
1. Market volatility (Section 2.1)
2. Regulatory changes (Section 3.4)
3. Supply chain disruptions (Section 5.2)
```

### Retrieved Context

* 📄 Chunk 12 – 92.4% similarity
* 📄 Chunk 45 – 89.1% similarity

Users can inspect:

* Source text
* Similarity scores
* Retrieved document chunks

---

## 🛠️ Advanced Usage Tips

### Better Queries

✅ *“Summarize mitigation strategies from Section 5”*
❌ *“Tell me about risks”*

### Multi-hop Reasoning

> “Based on Q3 financials, what growth projections seem reasonable?”

---

## ⚙️ Customization

* **Change LLM**

```python
model="mixtral-8x7b-32768"
```

* **Change Embedding Model**

```python
SentenceTransformer("all-MiniLM-L6-v2")
```

* **Tune Retrieval**

```python
top_k=5  # precision vs recall tradeoff
```

---

## 🔧 Troubleshooting

| Issue              | Solution                     |
| ------------------ | ---------------------------- |
| API errors         | Verify key validity & region |
| No text extracted  | Ensure PDF is text-based     |
| Irrelevant answers | Increase Top-K or chunk size |
| Slow responses     | Check Groq API status        |

---

## 🤝 Contributing

Contributions are welcome!
Feel free to submit issues, feature requests, or pull requests.

---

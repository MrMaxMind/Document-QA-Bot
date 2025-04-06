# 📚 Document QA Bot - Intelligent Document Assistant  
**RAG Architecture Diagram**  
*Powered by Retrieval-Augmented Generation (RAG) Technology*

---

## 🚀 Getting Started

### System Requirements
- Modern web browser (Chrome/Firefox/Edge latest versions)

### API keys for:
- 🔑 **Groq Cloud** (LLM processing)  
- 🗄️ **Pinecone** (Vector database)

### Documents in supported formats:
- 📄 **PDF** (Text-based, not scanned)  
- 📝 **DOCX** (Microsoft Word)  
- 📋 **TXT/MD** (Plain text formats)  
- 🧪 Other formats via **textract** *(Experimental)*

---

## ⚙️ Configuration Walkthrough

### Step 1: API Setup
1. **Sidebar Configuration** (← Left panel)
2. Enter credentials:
   - 🔑 **Groq API Key**: Get from [console.groq.com](https://console.groq.com)
   - 🗄️ **Pinecone API Key**: Get from [pinecone.io](https://pinecone.io)
3. Set parameters:
   - `Index Name`: `rag-doc` *(default)*
   - `Top-K Results`: **3-5 recommended**
4. Click **"Initialize"**

> System will automatically:
- ✅ Verify API connections  
- 🧠 Create vector index *(384-dim cosine space)*  
- ⚙️ Load AI models *(Mixtral 8x7b LLM + MiniLM embeddings)*

---

## 📤 Document Processing

### Supported File Handling

| Format | Engine       | Limitations                    |
|--------|--------------|--------------------------------|
| PDF    | PyPDF2       | Scanned PDFs not supported     |
| DOCX   | python-docx  | Complex formatting ignored     |
| Text   | Native       | UTF-8 encoding required        |
| Others | textract     | Requires system libraries      |

### Processing Flow
1. **File upload** *(max 200MB)*
2. Text extraction → Paragraph chunking
3. Vector embedding generation
4. Pinecone index population

**⏱️ Typical processing time:**
- 1-2s per page *(CPU-bound extraction)*
- ~5ms per chunk *(GPU-accelerated embeddings)*

---

## 💬 Interactive Q&A Interface

### Main Chat Panel →
```
[User]: What's the main risk factors mentioned?  
[Bot]: The document identifies 3 primary risk factors:  
1. Market volatility (Section 2.1)  
2. Regulatory changes (Section 3.4)  
3. Supply chain disruptions (Section 5.2)
```

### 🔍 Retrieved Context:
- 📄 **Chunk 12** *(92.4% match)*: _"Market risks include..."_  
- 📄 **Chunk 45** *(89.1% match)*: _"Recent regulatory proposals..."_

### Context Inspector ←

**Key Features:**
- Relevance scores *(0-1 cosine similarity)*
- Chunk navigation
- Source text verification
- Score-based filtering

---

## 🛠️ Advanced Features

### Query Optimization Tips

```
#️⃣ Use specific phrases from document  
❌ "Tell me about risks"  
✅ "List mitigation strategies for supply chain risks from Section 5"

#️⃣ Leverage document structure  
❌ "What's important?"  
✅ "Summarize key points from the Executive Summary"

#️⃣ Multi-hop questioning  
"Based on the Q3 financials, what growth projections seem reasonable?"
```

---

## ⚙️ Performance Controls

```python
# Advanced users can modify:
index.query(
    vector=embedding,
    top_k=5,  # Balance precision/recall
    filter={"section": "appendix"},  # Metadata filtering
    include_values=True
)
```

---

## 🔧 Troubleshooting Guide

| Issue                   | Solution                                       |
|------------------------|------------------------------------------------|
| "API Error"            | Verify key permissions + region                |
| "No text extracted"    | Check PDF text selectability                   |
| "Irrelevant answers"   | Increase `top_k` + verify chunk quality        |
| "Slow responses"       | Check Groq API status @ [status.groq.com](https://status.groq.com) |

---

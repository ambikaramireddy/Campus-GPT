# 🎓 CampusGPT

### AI-Powered College Management Assistant using Retrieval-Augmented Generation (RAG)

<p align="center">
  <b>Ask questions. Retrieve relevant college information. Get grounded AI answers.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/Streamlit-Frontend-red?style=for-the-badge&logo=streamlit">
  <img src="https://img.shields.io/badge/FastAPI-Backend-green?style=for-the-badge&logo=fastapi">
  <img src="https://img.shields.io/badge/LangChain-RAG-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/FAISS-VectorDB-yellow?style=for-the-badge">
  <img src="https://img.shields.io/badge/HuggingFace-LLM-yellow?style=for-the-badge&logo=huggingface">
</p>

## 📌 1. Business Objective

The business objective of CampusGPT is to make institutional information **faster and easier to access** for students.

College information is often distributed across multiple documents such as admission details, fee structures, academic regulations, hostel information, placement information, and notices. CampusGPT provides a conversational interface that allows students to access this information by simply asking questions.

The system can help reduce the effort involved in manually searching through documents and provide a more convenient way to interact with institutional information.

---

## ❗ 2. Problem Statement

College information is commonly distributed across:

* PDFs
* Notices
* Brochures
* Websites
* Academic documents
* Regulations and policies

Students may need to manually search these sources to find information related to:

* Admissions
* Courses
* Fee structure
* Hostel facilities
* Placements
* Academic information
* Campus facilities
* College policies

Traditional document-search methods can be time-consuming, especially when students do not know which document contains the required information.

### Proposed Solution

CampusGPT provides a conversational interface where students can ask questions in natural language.

The system understands the query, searches the college knowledge base using semantic similarity, retrieves relevant document chunks, and passes the retrieved information to an LLM to generate a contextual response.

---

## 🎯 3. Objective of the Project

The main objective of CampusGPT is to develop a **document-grounded AI assistant** for college-related queries using RAG.

### Key Objectives

* Allow students to ask college-related questions using natural language.
* Extract information from college PDF documents.
* Split documents into smaller searchable chunks.
* Convert text chunks into vector embeddings.
* Store and search embeddings using FAISS.
* Retrieve relevant information using semantic similarity.
* Provide retrieved information as context to an LLM.
* Generate contextual responses based on the retrieved information.
* Reduce the effort required to manually search through college documents.

---

## 🧠 4. Core Idea

The core workflow of CampusGPT is:

**College Documents → Text Extraction → Chunking → Embeddings → FAISS → Semantic Retrieval → LLM → Final Answer**

---

## 🔄 5. Project Approach

CampusGPT follows a Retrieval-Augmented Generation pipeline.

### Step 1: Document Collection

College-related PDF documents are used as the knowledge source.

These documents contain information such as rules, regulations, academic information, and other institutional details.

### Step 2: Text Extraction

The text is extracted from PDF documents using **PyPDF**.

This converts the document content into text that can be processed by the RAG pipeline.

### Step 3: Text Chunking

The extracted text is divided into smaller chunks.

A chunk overlap is also used so that important information is not lost between two consecutive chunks.

Chunking makes the documents easier to process and improves the retrieval process.

### Step 4: Generate Embeddings

Each text chunk is converted into a numerical vector using a **Hugging Face embedding model**.

These vectors represent the semantic meaning of the corresponding text.

### Step 5: Store Embeddings in FAISS

The generated embeddings are stored in **FAISS**.

FAISS is used to perform efficient vector similarity search.

### Step 6: Process User Query

When a student asks a question, the query is converted into an embedding using the same embedding model.

### Step 7: Semantic Retrieval

The query embedding is compared with the stored document embeddings.

FAISS retrieves the most relevant chunks based on semantic similarity.

### Step 8: Provide Context to LLM

The retrieved document chunks are combined with the user's question and provided as context to the Large Language Model.

### Step 9: Generate Final Answer

The LLM generates a contextual response using the retrieved information.

The final answer is displayed to the user through the application interface.

---

## 🏗️ 6. System Architecture

```text
                    COLLEGE PDF DOCUMENTS
                             │
                             ▼
                     Document Loading
                          (PyPDF)
                             │
                             ▼
                         Chunking
                    + Chunk Overlap
                             │
                             ▼
                    Hugging Face Embeddings
                         Text → Vector
                             │
                             ▼
                         FAISS Index
                    Store & Search Vectors
                             │
                             │
                       USER QUERY
                             │
                             ▼
                      Query Embedding
                       Question → Vector
                             │
                             ▼
                    FAISS Similarity Search
                          Top-K Chunks
                             │
                             ▼
                     Retrieved Context
                             │
                             ▼
                    Prompt Construction
                      Query + Context
                             │
                             ▼
                            LLM
                    Generate Answer
                             │
                             ▼
                      FINAL RESPONSE
```

---

## 🛠️ 7. Technology Stack

| Technology            | Role                                   |
| --------------------- | -------------------------------------- |
| Python                | Core application development           |
| PyPDF                 | PDF text extraction                    |
| Python Text Splitters | Document chunking                      |
| Hugging Face          | Embedding and LLM integration          |
| FAISS                 | Vector similarity search               |
| LangChain             | RAG workflow and LLM orchestration     |
| FastAPI               | Backend REST API                       |
| Streamlit             | Interactive frontend                   |
| NumPy                 | Numerical/vector operations            |
| LangSmith             | LLM application monitoring and tracing |

---

## 📂 8. Project Structure

```text
CampusGPT/
│
├── app.py
├── api.py
├── requirements.txt
├── .env
├── README.md
│
├── data/
│   └── college.pdf
│
└── src/
    ├── router.py
    ├── prompts.py
    ├── pdf_rag.py
    ├── hf_embeddings.py
    ├── llm_client.py
    └── ...
```

---

## ⚙️ 9. How the System Works

The system has two major phases:

### Phase 1: Knowledge Base Creation

```text
PDF
 ↓
Text Extraction
 ↓
Text Cleaning/Processing
 ↓
Chunking
 ↓
Embeddings
 ↓
FAISS
```

The documents are processed and converted into searchable vector representations.

### Phase 2: Question Answering

```text
User Question
 ↓
Query Embedding
 ↓
FAISS Similarity Search
 ↓
Top-K Relevant Chunks
 ↓
Context + Query
 ↓
LLM
 ↓
Final Answer
```

This allows the LLM to generate answers using information retrieved from the college knowledge base.

---

## 🚧 10. Challenge and Solution

### Challenge

One of the main challenges was improving the **relevance of retrieved information**.

Initially, some user queries returned partially relevant document chunks.

### Solution

I improved retrieval by:

* Optimizing chunk size.
* Using chunk overlap.
* Tuning the Top-K retrieval parameter.
* Using semantic similarity search.
* Using Hugging Face embeddings with FAISS.
* Grounding the LLM response using retrieved document context.

This improved the relevance of the retrieved information and helped produce more context-aware responses.

---

## 📊 11. Result

The project resulted in a functional AI-powered college management assistant.

CampusGPT can:

* Accept college-related questions in natural language.
* Search information from PDF documents.
* Perform semantic document retrieval.
* Retrieve relevant document chunks.
* Generate contextual AI responses.
* Provide information through a conversational interface.

The project also provided practical experience in building an end-to-end RAG application.

---

## 💡 12. Key Learning

Through this project, I gained practical experience in:

* Retrieval-Augmented Generation
* Text extraction
* Document chunking
* Text embeddings
* Vector databases
* Semantic similarity search
* FAISS
* LangChain
* Large Language Models
* Prompt construction
* FastAPI
* Streamlit
* LLM application monitoring

---

## 🔮 13. Future Enhancements

### 🌐 Multilingual Support

Allow students to interact with the assistant in multiple Indian languages.

### 🎤 Voice Assistant

Add speech-to-text and text-to-speech capabilities.

### 📱 Mobile Application

Develop an Android and iOS application.

### 🔐 Student Authentication

Add authentication to provide personalized responses for students.

### 🔔 Notification System

Provide important announcements and deadline reminders.

### ☁️ Scalable Cloud Deployment

Deploy the complete system using scalable cloud infrastructure.

---

## 🎯 14. Conclusion

CampusGPT demonstrates how **Retrieval-Augmented Generation** can be used to build a practical document-based college assistant.

The system combines PDF processing, text chunking, embeddings, FAISS-based semantic search, LangChain, and LLMs to retrieve relevant institutional information and generate contextual responses.

The project helped me understand the complete RAG pipeline, from **document ingestion and vector creation to information retrieval and final answer generation**.

It also provides a foundation for future improvements such as multilingual interaction, voice assistance, authentication, notifications, and scalable deployment.

---

## 👨‍💻 Developer

### Ambika Ramireddy

**B.Tech – Computer Science & Engineering (Data Science)**



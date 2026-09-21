# Research-paper-QA-project
# Research Paper Question-Answering System using RAG

## 📌 Project Overview

This project implements a **Retrieval-Augmented Generation (RAG)** system that allows users to upload research papers in PDF format and ask questions about their contents.

The system retrieves the most relevant sections from the uploaded research paper and uses a Large Language Model (LLM) to generate an answer based only on the retrieved context. Each answer is also associated with the source paper and page range.

## 🎯 Objectives

* Allow users to upload one or more research papers.
* Extract text from PDF documents.
* Divide documents into manageable overlapping chunks.
* Convert chunks into semantic embeddings.
* Retrieve relevant chunks using FAISS similarity search.
* Generate context-grounded answers using an LLM.
* Provide source/page citations for generated answers.
* Reduce hallucination by instructing the LLM to answer only from retrieved content.

## 🏗️ System Architecture

**PDF Upload → Text Extraction → Chunking → Embeddings → FAISS Vector Search → Relevant Context → LLM → Answer with Citations**

## 🔧 Technologies Used

* Python
* Google Colab
* PyMuPDF
* Sentence Transformers
* FAISS
* Gemini API / OpenAI API
* NumPy
* Tiktoken

## 🤖 Models Used

### Embedding Model

`all-MiniLM-L6-v2`

* Produces 384-dimensional embeddings.
* Used for semantic similarity search.

### Language Model

The notebook supports:

* Google Gemini
* OpenAI

The default configuration uses Gemini.

## ⚙️ Configuration

| Parameter       |            Value |
| --------------- | ---------------: |
| Chunk Size      |        300 words |
| Chunk Overlap   |         50 words |
| Top-K Retrieval |                4 |
| Embedding Model | all-MiniLM-L6-v2 |
| LLM Provider    |           Gemini |

## 🔄 Methodology

### 1. PDF Ingestion

Users can upload one or more research papers in PDF format.

### 2. Text Extraction

PyMuPDF extracts text page by page so that the system can preserve page information for citations.

### 3. Text Chunking

The extracted text is divided into chunks of approximately 300 words with 50 words of overlap.

The overlap helps prevent important information from being lost when a sentence or concept occurs near a chunk boundary.

### 4. Embedding Generation

Each text chunk is converted into a numerical vector using the `all-MiniLM-L6-v2` Sentence Transformer model.

### 5. Vector Database / Retrieval

FAISS is used to store the embeddings and perform similarity search.

Normalized embeddings with FAISS inner-product search are used to perform cosine-similarity-based retrieval.

### 6. Context-Grounded Generation

The top 4 relevant chunks are passed to the LLM.

The prompt instructs the LLM to:

* Use only the retrieved context.
* Avoid using outside knowledge.
* State that the paper does not address the question when sufficient information is unavailable.
* Include source citations with the generated answer.

### 7. Question Answering

The system supports predefined questions such as:

* What is the objective of the paper?
* What methodology was used?
* What datasets were used?
* What are the major findings?
* What are the limitations?

Users can also enter their own questions interactively.

## 📊 Evaluation

The current notebook implements retrieval and context-grounded generation, but it does **not automatically calculate numerical Precision, Recall, or Faithfulness scores**.

Therefore, these metrics should be reported only after performing a separate evaluation using a labelled question-answer dataset or an appropriate RAG evaluation framework.

## ✨ Key Features

* 📄 Multiple PDF upload support
* 🔍 Semantic search
* 🧠 Retrieval-Augmented Generation
* 📚 Research-paper-specific question answering
* 📌 Source and page citations
* 🛡️ Context-grounded responses
* 🔄 Interactive question answering
* ⚙️ Adjustable chunk size, overlap and Top-K
* 📊 Retrieval experimentation

## 🚀 How to Run

1. Open the notebook in Google Colab.
2. Install the required dependencies.
3. Select Gemini or OpenAI as the LLM provider.
4. Enter the required API key when prompted.
5. Upload one or more research papers.
6. Run the notebook cells sequentially.
7. Ask questions about the uploaded papers.
8. Review the generated answer and source citations.

## 📁 Project Structure

```text
Research-Paper-QA-RAG/
│
├── Research_Paper_QA_RAG.ipynb
├── README.md
└── Documentation.pdf
```

## 🔮 Future Enhancements

* Add automated Precision, Recall and Faithfulness evaluation.
* Add a web-based interface using Streamlit or Gradio.
* Add persistent vector storage.
* Support larger research-paper collections.
* Add hybrid BM25 + semantic retrieval.
* Add metadata filtering by paper, author or topic.
* Add conversational memory for follow-up questions.

## 👩‍💻 Author

**Tejaswini Talla**

B.Tech – Data Science
Vignan University

# -Retrieval-Augmented-Generation-RAG-pipeline
to run this project 
this is the image id of docker:: sha256:7104ed26e6fd3eb3fcce862e1754d7881bb9aa7b23d6401ea2fad1d3494b7d85
this is thee name of docker container ::   adarshsha/rag


go on github:

step 1:
create a empty folder in desktop
step 2:
copy link of URL 
step 3:
open powershell and write 
"git clone <url>"
step 4:
write "code ."
step 5:
open 2 seperate terminal 
write this command
Terminal 1:
"python -m uvicorn main:app --reload --port 8000"
Terminal 2:
"python -m streamlit run streamlit_app.py"

now upload pdf and ask queries to it 



Introduction
In this comprehensive guide, we'll walk you through the process of building a Retrieval-Augmented Generation (RAG) system using LangChain.

Build a production-ready RAG chatbot that can answer questions based on your own documents using Langchain. This comprehensive tutorial guides you through creating a multi-user chatbot with FastAPI backend and Streamlit frontend, covering both theory and hands-on implementation.

What You'll Learn

Introduction to RAG: Learn the fundamentals of Retrieval-Augmented Generation (RAG) and understand its significance in modern AI applications.

Working with LangChain: Get hands-on experience with LangChain, exploring its core components such as large language models (LLMs), prompts, and retrievers.

Document Processing: Master the process of splitting, embedding, and storing documents in vector databases to enable efficient retrieval.

Building RAG Chains: Develop your first RAG chain capable of answering document-based questions, and advance to creating conversational AI systems that manage complex interactions.

Contextualizing and refining queries: Learn how to refine queries using conversation history, making your AI system more accurate and responsive.

Conversational RAG: Implement a chatbot to apply these concepts practically and manage conversation history using databases.

Moving to Production: Integrate your RAG system into a FastAPI application, modularize your code, and create essential API endpoints for file management.

Building a Streamlit App: Develop a user-friendly Streamlit app that interacts with your FastAPI backend, allowing real-time data management and interaction.

# 🧠 Retrieval-Augmented Generation (RAG) Chatbot System

This project is a complete **RAG-based question-answering system** that allows users to upload documents and ask natural language questions based on their content. It combines **vector search**, **LLM-based reasoning**, and **REST APIs** for an interactive, production-ready application.

---

## 📌 Project Objectives

- Build a **Retrieval-Augmented Generation (RAG)** pipeline.
- Support **multi-format document ingestion** (PDF, DOCX, HTML).
- Use a **vector database** (e.g., Chroma) for semantic search.
- Use **LLMs** like OpenAI or Gemini for generating contextual answers.
- Serve the app using a **REST API (FastAPI)**.
- Provide a user-friendly **Streamlit UI**.
- Enable easy deployment using **Docker Compose**.

---

## 🚀 Key Features

- ✅ Upload and process up to 20 documents (max 1000 pages each)
- ✅ Split documents into chunks for embedding
- ✅ Store embeddings in **Chroma vector DB**
- ✅ Ask natural language queries referencing uploaded content
- ✅ View and manage uploaded documents
- ✅ Use **Google Generative AI** (`text-embedding-004` and Gemini models)
- ✅ Containerized with Docker for **local or cloud deployment**
- ✅ Includes RESTful APIs and frontend UI
- ✅ Modular, scalable, and easy to extend

---

## 🏗️ System Architecture

```text
            +--------------------+         +---------------------+
            |   Streamlit UI     | <-----> |    FastAPI Backend  |
            +--------------------+         +----------+----------+
                                                     |
                                  +------------------+------------------+
                                  |                                     |
                       +----------v---------+               +-----------v-----------+
                       |   Chroma VectorDB  |               |   Google Gemini LLM   |
                       +--------------------+               +-----------------------+





project-root/
│
├── main.py                  # FastAPI application
├── app.py                   # Streamlit frontend
├── api_utils.py             # Handles API interactions
├── db_utils.py              # SQLite storage for metadata & chat history
├── chroma_utils.py          # Chroma vector DB functions
├── langchain_utils.py       # RAG chains and prompt templates
├── pydantic_models.py       # Pydantic data models
├── chat_interface.py        # Streamlit chat UI
├── sidebar.py               # Streamlit sidebar
├── requirements.txt         # Python dependencies
├── Dockerfile               # Unified Docker build
├── docker-compose.yml       # Compose for backend and frontend
├── .env                     # Contains your GOOGLE_API_KEY
└── README.md                # This file



⚙️ Setup Instructions
🐳 Dockerized Setup (Recommended)
1. Clone the repo
bash
Copy
Edit
git clone https://github.com/your-username/rag-chatbot.git
cd rag-chatbot
2. Create a .env file
env
Copy
Edit
GOOGLE_API_KEY=your-google-api-key
3. Build and run the app
bash
Copy
Edit
docker build -t rag-chatbot .
docker run -p 8000:8000 -p 8501:8501 rag-chatbot
OR using Docker Compose:

bash
Copy
Edit
docker-compose up --build
🖥️ Access the App
FastAPI Backend: http://localhost:8000

Streamlit Frontend: http://localhost:8501

🧪 Running Locally (Without Docker)
Create a virtual environment:

bash
Copy
Edit
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
Install dependencies:

bash
Copy
Edit
pip install -r requirements.txt
Start FastAPI:

bash
Copy
Edit
uvicorn main:app --reload --port 8000
In a new terminal, start Streamlit:

bash
Copy
Edit
streamlit run app.py --server.port 8501
🔌 API Endpoints (FastAPI)
Method	Endpoint	Description
POST	/upload-doc	Upload and index a document
GET	/list-docs	List uploaded documents
POST	/delete-doc	Delete a document from DB & Chroma
POST	/chat	Ask a question to the RAG pipeline

API base URL: http://localhost:8000

📤 Streamlit UI
Upload PDF/DOCX/HTML files

See the document metadata

Ask questions in the chat interface

See which model was used and which session ID the query belongs to

📦 Configuration Details
LLM Provider: Gemini (via langchain-google-genai)

Embedding Model: text-embedding-004

Vector Store: ChromaDB

Environment Vars: Configurable via .env

Session History: Stored using SQLite

Document metadata: Tracked via document_store table

✅ Testing
Unit tests can be added for:

Document loading

Chunk splitting

Embedding generation

API responses

✅ Optionally provide a postman_collection.json for easy testing.

🧪 Example API Payloads
Upload Document
http
Copy
Edit
POST /upload-doc
Content-Type: multipart/form-data
file: sample.pdf
Query Chatbot
json
Copy
Edit
POST /chat
{
  "question": "What is this paper about?",
  "session_id": "abcd-1234",
  "model": "gemini-2.5-pro"
}
🧠 Technologies Used
LangChain

Google Generative AI

Chroma VectorDB

FastAPI

Streamlit

Docker

🔍 Evaluation Criteria (Assignment Guidelines)
Criteria	✅ This Project
Document ingestion & chunking	✅ Yes
Vector DB + embeddings	✅ Yes
REST API (upload, query, meta)	✅ Yes
Dockerized architecture	✅ Yes
Multi-model LLM support	✅ Yes
Streamlit frontend	✅ Yes
Clean modular code	✅ Yes
Configurable .env + models	✅ Yes

📬 Deliverables
✅ GitHub Repo with Full Code

✅ Docker Setup

✅ .env Config for LLM Keys

✅ API Docs (this README)

✅ Optional Postman Collection

👨‍💻 Author
Adarsh Sharma
GitHub • LinkedIn

📄 License
MIT License — free to use, fork, and modify.

yaml
Copy
Edit



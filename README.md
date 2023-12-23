# RAG Chat
A web application that allows users to upload documents to be added to a knowledge base which is used by a LLM to generate relevant responses. When a document is uploaded to the application, the text is extracted and split into concise documents. These documents are stored in a vector store indexed by their embeddings generated by an embedding model. Upon receiving a query in the chat, the vector store will retrieve the documents which are the most similar by comparing the embeddings of the documents with the query. This document is then incorporated into the prompt to the LLM as context for answering the query.
The chat model also has a memory feature and keeps track of the chat history of the ongoing chat and uses it as context for generating the next response.

![RAGChat screenshot](https://github.com/wwaihoe/RAG-Chat/assets/91514179/209895fe-e0f9-4fb5-80f2-c3540131f44b)

## How to run
1. Update Docker Compose file with HuggingFace API Token or OpenAI API key (requires switching to OpenAI llm in chatModel.py).
2. Run command `docker compose up --build` to build and run containers.
3. Upon completion, RAG Chat will run on localhost:8000

## Microservices Architecture
The web application consists of 3 Docker containers which are run together using Docker Compose. Each of the services run on each container are loosely coupled and modular, with each service having a well-defined and focused scope and function. This ensures that the application is less prone to complete failure and allows updates to the application in the future to be more seamless.

### Docker Services (Containers)
front-end
- User interface
\
chat-model
- Generates text response using LLM and document retrieved from retrieval-model
\
retrieval-model
- Builds vector store from user documents
- Retrieves relevant documents for knowledge augmented generation by chat-model

### Frameworks and Models
Web Frameworks:
front-end
- Next.js, React
\
chat-model
- HuggingFace, LangChain, FastAPI, Uvicorn
\
retrieval-model
- ChromaDB, PyPDF2, FastAPI, Uvicorn
\
LLM APIs:
OpenAI API - gpt 3.5 (Paid)
HuggingFace Inference API - openchat/openchat_3.5 (Free)

## Flow of Events
![Term Project System Workflow Diagram](https://github.com/wwaihoe/RAG-Chat/assets/91514179/ac92fe05-2b28-4e42-b64c-905cd0abfbba)


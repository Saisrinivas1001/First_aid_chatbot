# first-aid-chatbot

A Retrieval-Augmented Generation (RAG) chatbot for first-aid and medical Q&A, leveraging Redis for document search, Serper API for web search, and Groq LLM for response generation.

---

## Features

- **Document Search:** Retrieves relevant medical facts from a curated CSV knowledge base using vector search in Redis.
- **Web Search:** Uses Serper API to fetch up-to-date information from the web.
- **LLM Integration:** Uses Groq's Qwen model for natural language understanding and response generation.
- **API Server:** FastAPI-based HTTP server for chat interaction.

---

## Setup Instructions

### 1. Clone the Repository

```sh
git clone <your-repo-url>
cd rag_application_using_mcp_server_redis
```

### 2. Python Environment

- Python 3.12 is required (see [.python-version](.python-version)).
- Create and activate a virtual environment:

```sh
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 3. Install Dependencies

```sh
pip install -r requirements.txt
```
Or, using `pyproject.toml`:
```sh
pip install .
```

### 4. Environment Variables

Create a `.env` file in the project root with the following keys:

```
GROQ_API_KEY=your_groq_api_key
SERPER_API_KEY=your_serper_api_key
```

### 5. Redis Setup

- Install and start Redis server (default: `localhost:6379`).
- Populate Redis with document embeddings:
    1. Open `src/first_aid_chatbot/embedings_store.ipynb` in Jupyter.
    2. Run all cells to create the vector index and upload the CSV data.

### 6. Running the Application

Start the FastAPI server:

```sh
python app.py
```

The API will be available at [http://127.0.0.1:8080](http://127.0.0.1:8080).

---

## API Usage

### POST `/chat`

**Request:**
```json
{
  "message": "What is first aid for hypoglycaemia?"
}
```

**Response:**
```json
{
  "response": "First-aid for mild hypoglycaemia: give 15 g of fast-acting carbohydrate such as glucose tablets. For severe cases, give intramuscular glucagon if available."
}
```

---

## Project Structure

- [`app.py`](app.py): FastAPI server entry point.
- [`src/first_aid_chatbot/client.py`](src/first_aid_chatbot/client.py): Orchestrates LLM, document, and web search tools.
- [`src/first_aid_chatbot/documentSearch.py`](src/first_aid_chatbot/documentSearch.py): Redis vector search tool.
- [`src/first_aid_chatbot/webSearch.py`](src/first_aid_chatbot/webSearch.py): Serper API web search tool.
- [`src/first_aid_chatbot/embedings_store.ipynb`](src/first_aid_chatbot/embedings_store.ipynb): Embedding and Redis index setup.
- [`src/first_aid_chatbot/Assignment_Data_Base.csv`](src/first_aid_chatbot/Assignment_Data_Base.csv): Knowledge base.

---

## Known Limitations

- **Redis Required:** The chatbot will not function without a running Redis server and pre-populated vector index.
- **API Keys:** Requires valid Serper and Groq API keys.
- **No User Authentication:** The API is open and unsecured by default.
- **Limited Knowledge Base:** The CSV covers only a subset of first-aid/medical facts.
- **Performance:** First request may be slow due to model loading; subsequent requests are faster.
- **Concurrency:** The current setup is not optimized for high-concurrency production use.
- **Error Handling:** Minimal error handling; failures in Redis or external APIs may cause errors.

---

## Performance Report

- **Startup Time:** ~10-20 seconds (model and index loading).
- **Average Response Time:** 
    - Document search: < 1 second (after warmup)
    - Web search: 1-2 seconds (depends on Serper API latency)
    - LLM response: 2-5 seconds (depends on Groq API)
- **Memory Usage:** 
    - Embedding model: ~1GB RAM
    - Redis: ~50MB for 60 documents
- **Throughput:** Suitable for low to moderate traffic (1-5 concurrent users).

---

## Troubleshooting

- **Redis Connection Error:** Ensure Redis is running on `localhost:6379`.
- **API Key Errors:** Double-check `.env` file for correct keys.
- **Module Not Found:** Activate your virtual environment and install dependencies.

---

## License

MIT License

---

## Author

saiSrinivas
"# First_aid_chatbot" 
#   F i r s t _ a i d _ c h a t b o t 
 
 # First_aid_chatbot
# First_aid_chatbot
# First_aid_chatbot

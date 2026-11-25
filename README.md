# LangGraph Chatbot

A Streamlit chatbot built with LangGraph and LangChain. The main threaded chatbot uses the local TinyLlama 1.1B Chat model through Hugging Face Transformers to generate responses.

## Features

- Chat UI built with Streamlit.
- LangGraph manages the conversation flow and message state.
- The threaded frontend can switch between conversations.
- The tool backend checkpoints conversation state in a local SQLite database (`chatbot.db`).
- The repository also contains alternate frontends and backends for streaming, database, MCP, tools, and PDF/RAG experiments.

## Requirements

- Python 3.10 or later
- Internet access on first run to download TinyLlama and its model files from Hugging Face
- Enough memory and compute to run a 1.1B-parameter model locally

## Setup on Windows

Run these commands from the project root:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell prevents environment activation, you can invoke the environment's Python directly instead:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

## Run the threaded chatbot

From the project root, make the backend importable and start Streamlit:

```powershell
$env:PYTHONPATH = "$PWD\backend"
python -m streamlit run frontend\streamlit_frontend_threading.py
```

Streamlit prints a local URL (usually `http://localhost:8501`) when the app is ready. The first run may take longer while the model is downloaded and loaded.

To run the simpler streaming frontend instead:

```powershell
$env:PYTHONPATH = "$PWD\backend"
python -m streamlit run frontend\streamlit_frontend_streaming.py
```

## Conversation storage

The threaded frontend uses the SQLite checkpointer in `backend/langgraph_tool_backend.py`, which stores checkpoints in `chatbot.db`. The simpler backend in `backend/langgraph_backend.py` uses an in-memory checkpointer, so its checkpointed conversations do not persist after the process exits.

## Security

Do not commit `.env` files, API keys, or local database files. Before publishing this repository, remove any credentials embedded in backend source code and rotate them if they have already been exposed.

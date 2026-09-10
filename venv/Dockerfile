FROM python:3.11-slim

WORKDIR /app

# Install dependencies first (cached layer — only rebuilds if requirements.txt changes)
COPY venv/requirements.txt .
RUN pip install --no-cache-dir -r venv/requirements.txt

# Copy all app files
COPY venv/streamlit_app.py .
COPY venv/streamlit_app_tfidf.py .
COPY venv/main.py .

# Copy the company documents the RAG system searches through
COPY venv/_data/ ./_data/

# TF-IDF version — no model download, starts in under 2 seconds
# Switch back to streamlit_app.py to use the ChromaDB version locally
CMD ["streamlit", "run", "streamlit_app_tfidf.py", "--server.port=10000", "--server.address=0.0.0.0"]

# RAG Chatbot for ML/AI

This project is a **Streamlit-based Retrieval-Augmented Generation (RAG) chatbot** built for answering questions about Machine Learning and Artificial Intelligence.

It uses:

- **Streamlit** for the web UI
- **Google Gemini** for response generation
- **LangChain** for document processing
- **FAISS** for vector search
- **Sentence Transformers** for embeddings

The chatbot reads content from `mlbookcontent.txt`, splits it into chunks, creates or loads a FAISS index, and then uses that context to answer user queries.

## Features

- Clean Streamlit chat interface
- Context-aware responses from the provided ML/AI document
- General knowledge responses when the query is not document-specific
- Local FAISS index storage for faster startup
- Modern dark-themed UI

## Project Structure

```text
ragml/
|-- app.py
|-- mlbookcontent.txt
|-- requirements.txt
|-- ml.faiss_index/
|   |-- index.faiss
|   `-- index.pkl
`-- .env
```

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/CodeWithRuhani/ragml.git
cd ragml
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add your Gemini API key

Create a `.env` file in the project folder:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

Important:

- Do **not** commit `.env` to GitHub.
- If you are deploying on Streamlit Cloud, add the key in **Streamlit Secrets** instead of `.env`.

### 5. Run the app

```bash
streamlit run app.py
```

## How It Works

1. The app loads the Gemini API key from `.env`.
2. `mlbookcontent.txt` is loaded and split into chunks.
3. A FAISS vector store is created or loaded from `ml.faiss_index`.
4. When the user sends a query, the app checks whether it matches ML/AI keywords.
5. If relevant, the app retrieves similar chunks and answers using that context.
6. Otherwise, Gemini answers using general knowledge.

## Deployment on Streamlit Cloud

1. Push the project to GitHub.
2. Go to [Streamlit Community Cloud](https://streamlit.io/cloud).
3. Create a new app from your GitHub repo.
4. Set the main file path to:

```text
app.py
```

5. Add your API key in **Secrets**:

```toml
GEMINI_API_KEY = "your_gemini_api_key_here"
```

6. Deploy the app.

## Notes

- The FAISS index is stored locally in `ml.faiss_index/`.
- If the FAISS index is missing, the app will rebuild it from `mlbookcontent.txt`.
- If you replace your Gemini key, restart the app so it reloads the new value.

## Requirements

The project currently depends on:

- `streamlit`
- `langchain-community`
- `google-generativeai`
- `sentence-transformers`
- `faiss-cpu`

## License

Add a license here if you plan to share or publish the project publicly.

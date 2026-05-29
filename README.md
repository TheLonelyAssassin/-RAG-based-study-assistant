# RAG-based-study-assistant
A local RAG-based study assistant built from scratch without LangChain. Users upload any PDF and ask questions via a chat interface — answers are grounded strictly in the uploaded document. Built with SentenceTransformers (all-MiniLM-L6-v2) for embeddings, FAISS for instant similarity retrieval, and Mistral via Ollama for generation. Chunk size was tuned through experimentation, settling on 10 sentences with 2 sentences of overlap. Includes a built-in faithfulness evaluator scoring each answer 0-10 using a second LLM call.
##Architecture diagram:

![Architecture Diagram](architecture.png)

The flow reads as:
•	Left side -> document processing path (upload -> chunk -> embed -> cache)
•	Right side -> query answering path (question -> retrieve -> generate)
•	Both paths meet at the chat window output, with the evaluator scoring every answer

## Requirements

- Python 3.10+
- [Ollama](https://ollama.com) installed and running locally
- Mistral model pulled via Ollama

## Installation

### 1. Clone the repository
git clone https://github.com/your-username/rag-study-assistant.git
cd rag-study-assistant

### 2. Install dependencies
pip install streamlit sentence-transformers faiss-cpu \
            pymupdf nltk torch numpy requests

### 3. Install and run Ollama
# Download from https://ollama.com
ollama pull mistral
ollama serve

### 4. Download NLTK tokenizer (first run only)
python -c "import nltk; nltk.download('punkt')"

### 5. Run the app
streamlit run app.py

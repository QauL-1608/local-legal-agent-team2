# WAKILI M-SMART Local AI Legal Agent

A local AI-powered legal document analysis system that uses both local and cloud-based AI models to analyze legal documents, contracts, and provide comprehensive legal insights.

## Features

- **Document Analysis**: Upload and analyze legal documents (PDF format)
- **Multiple Analysis Types**: Contract review, legal research, risk assessment, compliance checks
- **AI-Powered Team**: Multiple specialized AI agents working together
- **Hybrid Operation**: Works with both local models (Ollama) and cloud models (OpenAI)

## Requirements

- Python 3.11+
- Qdrant server (local vector database)
- Ollama server (optional for local models)
- OpenAI API key (optional for cloud models)

## Installation

This project uses `uv` for dependency management. If you don't have `uv` installed, you can install it with:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd local-legal-agent-team2
   ```

2. Install dependencies:
   ```bash
   uv sync
   ```

3. Set up environment variables:
   - Create a `.env` file in the project root (or use the existing `.env.py` file)
   - Add your OpenAI API key:
     ```
     OPENAI_API_KEY="your-api-key-here"
     ```

4. Start Qdrant server:
   ```bash
   docker run -p 6333:6333 qdrant/qdrant
   ```

5. (Optional) Start Ollama server:
   ```bash
   ollama serve
   ```
   
   And pull the required models:
   ```bash
   ollama pull llama3.1
   ollama pull nomic-embed-text
   ```

## Usage

1. Start the application:
   ```bash
   uv run streamlit run local_legal_agent.py
   ```

2. Open your browser at http://localhost:8501

3. Upload a legal document (PDF format)

4. Select an analysis type and enter any specific queries

5. Review the detailed analysis, key points, and recommendations

## Model Selection

The application automatically selects which models to use:

- If an OpenAI API key is provided, it will use:
  - GPT-4o for text generation
  - text-embedding-3-small for embeddings

- Otherwise, it will fall back to local models:
  - llama3.1 for text generation
  - nomic-embed-text for embeddings

## Troubleshooting

### Common Issues

1. **Dimension mismatch errors**: This occurs when switching between different embedding models. Delete the Qdrant collection and restart:
   ```bash
   curl -X DELETE http://localhost:6333/collections/legal_docs_local
   ```

2. **OpenAI API key issues**: Ensure your API key is correctly set in the `.env.py` file and that it has not expired.

3. **Ollama model not found**: Make sure you've pulled the required models:
   ```bash
   ollama pull llama3.1
   ollama pull nomic-embed-text
   ```

## License

[Specify license information]
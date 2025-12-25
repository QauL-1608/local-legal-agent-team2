# WAKILI M-SMART Local AI Legal Agent

A local AI-powered legal document analysis system that uses both local and cloud-based AI models to analyze legal documents, contracts, and provide comprehensive legal insights.

**Quick Start:**
```bash
# Install dependencies
uv sync

# Run the application
source $HOME/.local/bin/env
uv run streamlit run local_legal_agent.py
```

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
   - Copy the sample environment file to create your own:
     ```bash
     cp .env.sample .env
     ```
   - Edit the `.env` file and add your OpenAI API key:
     ```
     OPENAI_API_KEY="your-api-key-here"
     ```

4. Install and start Qdrant server:
   - Follow the instructions at https://qdrant.tech/documentation/install/
   - Ensure it's running on port 6333

5. (Optional) Start Ollama server:
   ```bash
   ollama serve
   ```
   
   And pull the required models:
   ```bash
   ollama pull llama3.1
   ollama pull nomic-embed-text
   ```

## Running the Application

1. Make sure your environment is set up correctly:
   - `.env` file with your OpenAI API key
   - Qdrant server running on port 6333
   - Ollama server running (if using local models)

2. Start the application:
   ```bash
   source $HOME/.local/bin/env  # Add uv to your PATH
   uv run streamlit run local_legal_agent.py
   ```

3. Open your browser at the URL shown in the terminal (typically http://localhost:8501)

4. Using the application:
   - Upload a legal document (PDF format)
   - Select an analysis type (Contract Review, Legal Research, etc.)
   - Enter any specific queries or questions
   - Review the detailed analysis, key points, and recommendations

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

1. **Dimension mismatch errors**: This occurs when switching between different embedding models. Delete the Qdrant collection using the Qdrant API:
   ```bash
   curl -X DELETE http://localhost:6333/collections/legal_docs_local
   ```
   Then restart the application.

2. **OpenAI API key issues**: Ensure your API key is correctly set in the `.env` file and that it has not expired.

3. **Ollama model not found**: Make sure you've pulled the required models:
   ```bash
   ollama pull llama3.1
   ollama pull nomic-embed-text
   ```

4. **Import errors**: If you encounter import errors, run `uv sync` to ensure all dependencies are installed correctly.

5. **Connection refused errors**: Make sure Qdrant is running and accessible on port 6333.

## License

[Specify license information]
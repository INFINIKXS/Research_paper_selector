

# Document Intelligence Agent

A modular, extensible agent for intelligent document processing, research filtering, and automated file renaming. Supports TXT, PDF, and DOCX files, leverages Gemini 2.5 Pro LLM for content analysis, and provides robust workflows for research and file management.

---

## Features

- **Rename Mode:** Batch rename documents using LLM-generated, context-aware filenames.
- **Research Filter Mode:** Filter and copy relevant PDFs based on LLM-powered research queries.
- **Modular File Handlers:** Unified interface for TXT, PDF, and DOCX files (easily extensible).
- **LLM Client:** Gemini 2.5 Pro integration with prompt templating and document chunking.
- **Prompt Templating:** Named templates for 'rename' and 'research' tasks.
- **Comprehensive Testing:** Unit and integration tests for all major components.

---

## Installation

1. **Clone the repository:**
   ```sh
   git clone https://github.com/INFINIKXS/Pdf_read_rename_Agent.git
   cd Pdf_read_rename_Agent
   ```
2. **Create and activate a virtual environment:**
   ```sh
   python -m venv .venv
   .venv\Scripts\activate  # On Windows
   # On macOS/Linux:
   source .venv/bin/activate
   ```
3. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```
4. **Set up environment variables:**
   - Create a `.env` file in the project root with your API keys:
     ```env
     GEMINI_API_KEY=your_gemini_api_key
     EXA_API_KEY=your_exa_api_key
     ```

---

## Usage

### CLI

The main entry point is `main.py`, which provides two subcommands: `rename` and `research`.

```sh
python main.py rename   # Run Rename Mode
python main.py research # Run Research Filter Mode
```

#### Rename Mode
Scans for TXT, PDF, and DOCX files, extracts text, and uses the LLM to generate descriptive filenames.

**Example:**
```sh
python main.py rename
```
*Options can be added by editing `rename_mode` in `src/agent_core/rename_workflow.py`.*

#### Research Filter Mode
Scans a directory for PDFs, uses the LLM to score/filter them, and copies relevant files to a target directory.

**Example:**
```sh
python main.py research
```
*Options can be added by editing `research_filter_mode` in `src/agent_core/research_workflow.py`.*

---

## Usage in Python

### 1. Research Filter Workflow

Filter and copy relevant PDFs from a source directory to a destination directory using LLM-based scoring.

```python
from src.agent_core.research_workflow import ResearchWorkflow

source = "./pdfs"
dest = "./relevant_pdfs"
workflow = ResearchWorkflow()
copied = workflow.copy_relevant_pdfs(source, dest)
print("Copied relevant PDFs:", copied)
```

### 2. Rename Workflow

Automatically rename files based on LLM-generated context.

```python
from src.agent_core.rename_workflow import RenameWorkflow

source_dir = "./pdfs"
workflow = RenameWorkflow()
workflow.rename_files(source_dir)
```

---

## Architecture

```
src/
  handlers/
    base_handler.py   # Abstract base class for file handlers
    pdf_handler.py    # PDF file handler
    docx_handler.py   # DOCX file handler
    txt_handler.py    # TXT file handler
  services/
    llm_client.py     # LLM client (Gemini 2.5 Pro, prompt templating, chunking)
  agent_core/
    rename_workflow.py    # Rename workflow logic
    research_workflow.py  # Research filter workflow logic
main.py                  # Entry point
tests/                   # Unit and integration tests
requirements.txt
README.md
```

- **File Handlers:** Each handler implements a unified interface for extracting text.
- **LLM Client:** Handles prompt templating, chunking, and communication with Gemini 2.5 Pro.
- **Workflows:** Orchestrate file processing, LLM scoring, and file operations.

---

## Testing

Run all tests with:

```sh
pytest
```
Or run a specific test file:
```sh
pytest tests/test_handlers.py
pytest tests/test_llm_client.py
pytest tests/test_rename_workflow.py
pytest tests/test_research_workflow.py
```

Tests cover:
- File handlers (TXT, PDF, DOCX)
- LLM client logic
- Rename workflow
- Research filter workflow

---

## Extending the Agent

- **Add a new file handler:** Subclass `BaseHandler` and implement `extract_text`.
- **Add a new workflow:** Create a new class in `agent_core/` and use existing handlers and LLM client.
- **Swap LLM provider:** Update or extend `LLMClient` in `services/llm_client.py`.

---

## Requirements

- Python 3.8+
- See `requirements.txt` for dependencies (`fpdf`, `python-docx`, `pypdf`, etc.)

---

## Contributing

1. Fork the repo and create your branch.
2. Add tests for new features.
3. Ensure all tests pass and code is PEP 8 compliant.
4. Submit a pull request.

---

## License

[MIT License](LICENSE)

---

## Acknowledgments

- Gemini 2.5 Pro (Google)
- Python community libraries: `fpdf`, `python-docx`, `pypdf`

---

For more details, see the code-level documentation and inline docstrings.

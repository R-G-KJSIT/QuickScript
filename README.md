# FastWrite
Python Module for AI-Assisted Documentation

## Overview
This module provides functionality to:
- **Process Code Files**: Extract and list Python files from a ZIP archive.
- **Generate Data Flow Diagrams**: Create a data flow chart (in Graphviz format) by analyzing Python code using the AST module.
- **Generate Documentation**: Produce detailed documentation for Python code using multiple AI models:
  - Groq-based models (remote)
  - Gemini-based models (remote)
  - OpenAI-based models (remote)
  - Ollama-based models (local)
- **Evaluate Documentation Quality**: Compute BLEU scores to compare generated documentation against a reference document.


## Installation

### Requirements
- Python 3.11
- [groq](https://pypi.org/project/groq/)
- [google-generativeai](https://pypi.org/project/google-generativeai/)
- [openai](https://pypi.org/project/openai/)
- [requests](https://pypi.org/project/requests/)
- [nltk](https://pypi.org/project/nltk/)

### Install Dependencies
```bash
pip install groq google-generativeai requests nltk python-dotenv openai
```

## Usage

### Processing Files:
```
from FastWrite import extract_zip, list_python_files, read_file
import tempfile
import os

# Specify the path to your ZIP file containing Python code
zip_file_path = "path/to/your/code.zip"

with tempfile.TemporaryDirectory() as tmp_dir:
    # Extract the ZIP file
    extract_zip(zip_file_path, tmp_dir)
    
    # List Python files in the extracted directory
    py_files = list_python_files(tmp_dir)
    
    if py_files:
        # For example, choose the first Python file as the main file
        main_file_path = os.path.join(tmp_dir, py_files[0])
        code_content = read_file(main_file_path)

```

### Generating Data Flow Diagrams:

```
from FastWrite import generate_data_flow

# Generate Graphviz code for the data flow diagram
graphviz_code = generate_data_flow(code_content)
print(graphviz_code)

```

### Generating Documentation (Groq):

```
from FastWrite import generate_documentation_groq

custom_prompt = """
Objective:
Generate detailed and structured documentation for Python code. Include inline comments, function descriptions, module overviews, and best practices.
"""

groq_api_key = "your_groq_api_key"
groq_model = "deepseek-r1-distill-llama-70b"  # Replace with your desired model

doc_groq = generate_documentation_groq(code_content, custom_prompt, groq_api_key, groq_model)
print(doc_groq)

```

### Generating Documentation (Gemini):

```
from FastWrite import generate_documentation_gemini

custom_prompt = """
Objective:
Generate detailed and structured documentation for Python code. Include inline comments, function descriptions, module overviews, and best practices.
"""

gemini_api_key = "your_gemini_api_key"
gemini_model = "gemini-2.0-flash"  # Replace with your desired model

doc_gemini = generate_documentation_gemini(code_content, custom_prompt, gemini_api_key, gemini_model)
print(doc_gemini)

```

### Generating Documentation (OpenAI):

```
from FastWrite import generate_documentation_openai

custom_prompt = """
Objective:
Generate detailed documentation for Python code. Include inline comments, function descriptions, module overviews, and best practices.
"""
doc_openai = generate_documentation_openai(code_content, custom_prompt)
print(doc_openai)

```

### Generating Documentation (Ollama):

```
from FastWrite import generate_documentation_ollama

custom_prompt = """
Objective:
Generate detailed and structured documentation for Python code. Include inline comments, function descriptions, module overviews, and best practices.
"""

# Replace with your local Ollama model name (e.g., "ollama-llama-70b")
ollama_model = "ollama-llama-70b"

doc_ollama = generate_documentation_ollama(code_content, custom_prompt, ollama_model)
print(doc_ollama)

```

### Calculating Bleu Score:

```
from FastWrite import calculate_bleu

# Provide a reference documentation string for comparison
reference_doc = "Your reference documentation text here..."

bleu_score = calculate_bleu(doc_llm-host, reference_doc) ##LLM host may include Groq,Gemini,OpenAI or Ollama
print("BLEU Score:", bleu_score)

```
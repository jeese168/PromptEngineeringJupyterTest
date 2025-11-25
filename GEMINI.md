# Project Overview

This project is a collection of Jupyter notebooks designed for prompt engineering and Large Language Model (LLM) evaluation. The primary focus is on experimenting with various models from the Qwen3 series using `ollama`, as well as other models like Kimi through their respective APIs.

The notebooks are structured as hands-on experiments to test and compare different aspects of LLMs, including:
- Core prompt engineering principles.
- Context retention and "context rot" (long-term memory).
- Comparative intelligence benchmarks across different model sizes (e.g., 0.6B vs 8B vs 14B) on tasks involving logic, math, creativity, and coding.

# Technologies

- **Language:** Python
- **Environment:** Jupyter Notebooks (intended for Google Colab with GPU acceleration)
- **LLM Orchestration:** `ollama` for local model execution
- **Core Models:** Qwen3 series (0.6B, 1.7B, 8B, 14B, etc.)
- **APIs:** Moonshot AI (for the Kimi model)
- **Key Python Libraries:** `requests`, `openai`, `python-dotenv`

# Building and Running

There is no central build process or `requirements.txt` file. The project is intended to be used by running the Jupyter notebooks (`.ipynb` files) individually, preferably in a Google Colab environment.

## Setup

1.  **Environment:** Open the desired `.ipynb` file in Google Colab or a local Jupyter environment.
2.  **Dependencies:** The notebooks are self-contained and will install necessary tools like `ollama` and download the required models using shell commands within the code cells.
3.  **API Keys:** For notebooks that use external APIs (e.g., `temptest/kimi_prompt01.ipynb`), you will need to create a `.env` file in the project root and add the necessary API keys:
    ```
    MOONSHOT_API_KEY="your_api_key_here"
    ```

## Running Experiments

- Execute the cells in the notebooks sequentially. The initial cells typically handle environment setup and model downloads.
- Subsequent cells contain the specific experiments and will output the results directly in the notebook.

# Development Conventions

- **Modular Notebooks:** Each notebook is a self-contained experiment focused on a specific model or concept.
- **In-Notebook Setup:** All necessary setup, including package installation and model downloading, is performed directly within the notebooks using `!pip` or `!curl` commands. This ensures reproducibility within the target Colab environment.
- **Local and Remote Execution:** The primary workflow involves running models locally via `ollama`, but the structure allows for easy extension to other model APIs.
- **Experiment-Driven:** The code is structured around running specific, documented experiments with clear goals and expected outcomes.

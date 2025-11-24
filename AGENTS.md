# Prompt Engineering Jupyter Test Project

## Project Overview

This is a Jupyter Notebook-based project focused on prompt engineering experimentation and AI model testing. The project serves as a testing ground for various AI models including Qwen3 series models via Ollama integration and Moonshot AI's Kimi models via API. The primary language is Chinese, with documentation and code comments predominantly in Chinese.

## Technology Stack

- **Runtime Environment**: Python 3.11.14 with Jupyter ecosystem
- **Primary Interface**: Jupyter Notebooks (.ipynb files)
- **AI Model Integration**: 
  - Ollama for local model deployment (Qwen3 series)
  - OpenAI-compatible API for cloud models (Moonshot AI Kimi)
- **Development Environment**: PyCharm with Jupyter support
- **Virtual Environment**: Python venv (.venv/)

## Project Structure

```
/Users/jeese/Projects/PromptEngineeringJupyterTest/
├── README.md                           # Qwen3 Colab deployment guide (Chinese)
├── requirements.txt                    # Empty requirements file
├── .env                                # API key configuration (MOONSHOT_API_KEY)
├── sample.ipynb                        # Basic PyCharm Jupyter example
├── prompt_engineering_principles.ipynb # Main prompt engineering experiments
├── temptest/                           # Additional experiment notebooks
│   ├── kimi_prompt01.ipynb            # Kimi API testing
│   ├── local_models_experiment.ipynb  # Local model experiments
│   └── qwen3_intelligence_benchmark.ipynb # Qwen3 intelligence benchmarks
├── .venv/                             # Python virtual environment
├── .claude/                           # Claude AI configuration
└── .idea/                             # PyCharm project settings
```

## Key Components

### 1. Prompt Engineering Core (`prompt_engineering_principles.ipynb`)
- Based on Andrew Ng x OpenAI prompt engineering course
- Implements two core principles with 6 strategies total
- Uses Qwen3 8B model (Q4_K_M quantization) for experiments
- Features carefully designed positive/negative examples
- Includes automated Ollama installation and model downloading

### 2. Model Testing Suite (`temptest/`)
- **kimi_prompt01.ipynb**: Basic Kimi API integration tests
- **local_models_experiment.ipynb**: Local model deployment experiments
- **qwen3_intelligence_benchmark.ipynb**: Intelligence benchmarking for Qwen3 models

### 3. Documentation
- **README.md**: Comprehensive Qwen3 deployment guide for Google Colab
- Covers model specifications, hardware requirements, quantization options
- Includes performance benchmarks and Colab-specific configurations

## Development Setup

### Environment Configuration
```bash
# Virtual environment is already set up at .venv/
source .venv/bin/activate  # Activate on Unix/macOS
# .venv\Scripts\activate    # Activate on Windows
```

### API Keys
- Moonshot AI API key configured in `.env` file
- Ollama runs locally without API keys

### Dependencies
Key packages installed in virtual environment:
- jupyterlab (4.4.10)
- notebook (7.4.7)
- openai (2.8.0)
- python-dotenv (1.2.1)
- requests (2.32.5)

## Running the Project

### Jupyter Notebook Server
```bash
jupyter lab        # Start JupyterLab
jupyter notebook   # Start classic Jupyter Notebook
```

### Ollama Integration
The project includes automated Ollama setup for local model deployment:
```python
# Install Ollama (automated in notebooks)
!curl -fsSL https://ollama.com/install.sh | sh
!nohup ollama serve &

# Download Qwen3 models
!ollama pull qwen3:8b
```

### Model Recommendations
- **T4 GPU (16GB VRAM)**: Qwen3-8B recommended
- **L4 GPU (24GB VRAM)**: Qwen3-32B or 30B-A3B (MoE)
- **A100-40GB**: Qwen3-32B with higher quantization
- **A100-80GB**: Qwen3-235B-A22B (flagship model)

## Code Style Guidelines

### Language Preferences
- Primary documentation and comments in Chinese
- Code follows standard Python conventions
- Notebook cells include clear markdown explanations

### Notebook Structure
1. **Setup Cells**: Environment preparation and imports
2. **Experiment Cells**: Core functionality with clear outputs
3. **Analysis Cells**: Results interpretation and conclusions
4. **Cleanup Cells**: Resource management

### Model Interaction Pattern
```python
# Standard pattern for Ollama integration
import subprocess
import time

# Start Ollama service
subprocess.Popen(["ollama", "serve"])
time.sleep(5)

# Run model
result = subprocess.run(
    ["ollama", "run", "qwen3:8b", "prompt here"],
    capture_output=True, text=True
)
```

## Testing Strategies

### Automated Testing
- Notebooks include self-contained test cases
- Positive/negative example pairs for prompt engineering principles
- Automated model deployment verification

### Performance Benchmarking
- Token generation speed measurements
- Memory usage monitoring for different model sizes
- Quality assessment through structured prompts

### Model Comparison
- Side-by-side outputs from different model sizes
- Quantization impact analysis
- Hardware requirement validation

## Security Considerations

### API Key Management
- API keys stored in `.env` file (git-ignored)
- Environment variables used for sensitive configuration
- No hardcoded credentials in notebooks

### Model Deployment
- Local Ollama deployment reduces external dependencies
- Colab-specific security considerations documented
- Resource usage monitoring to prevent abuse

### Data Privacy
- No persistent data storage in project
- Temporary files cleaned up after experiments
- Clear documentation of data handling practices

## Deployment Process

### Google Colab Deployment
1. Upload notebooks to Colab environment
2. Configure GPU runtime (T4/L4/A100 based on requirements)
3. Run automated Ollama installation cells
4. Download appropriate model based on available hardware
5. Execute experiments with proper resource monitoring

### Local Development
1. Ensure Python 3.11+ environment
2. Activate virtual environment
3. Start Jupyter server
4. Run notebooks with local Ollama installation

## Troubleshooting

### Common Issues
- **Ollama Installation**: Network connectivity for download
- **Model Download**: Sufficient disk space (5-20GB per model)
- **GPU Memory**: Monitor VRAM usage during experiments
- **Colab Timeout**: 12-hour limit for free tier

### Performance Optimization
- Use appropriate quantization levels for hardware
- Monitor system resources during experiments
- Clean up unused models to free disk space

## Future Enhancements

### Planned Features
- Additional model integrations (GPT, Claude, etc.)
- Automated benchmark generation
- Web interface for experiment management
- Results visualization and comparison tools

### Research Directions
- Advanced prompt engineering techniques
- Multi-modal model integration
- Fine-tuning experiments
- Domain-specific prompt optimization
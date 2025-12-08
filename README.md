# Model Deployment Project

This project provides multiple methods to deploy and inference AI models, including PyTorch, vLLM, and Triton Inference Server.

## Table of Contents

- [Overview](#overview)
- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Deployment Methods](#deployment-methods)
  - [Method 1: PyTorch HuggingFace](#method-1-pytorch-huggingface)
  - [Method 2: vLLM Server](#method-2-vllm-server)
  - [Method 3: Triton Inference Server](#method-3-triton-inference-server)
- [Running the API](#running-the-api)
- [Running Gradio Interface](#running-gradio-interface)
- [Project Structure](#project-structure)
- [Complete Workflow](#complete-workflow)

## Overview

This project supports 3 model deployment methods:

1. PyTorch Standard - Traditional approach using PyTorch and HuggingFace
2. vLLM - Optimized inference speed for Large Language Models
3. Triton Server - Production-ready inference server with Docker

## System Requirements

- Python 3.8 or higher
- CUDA-compatible GPU
- Docker and Docker Compose for Triton Server
- Required libraries: PyTorch, HuggingFace Transformers, vLLM, FastAPI, Gradio

## Installation

```bash
git clone https://github.com/yourusername/yourproject.git
cd yourproject
pip install -r requirements.txt
```

## Deployment Methods

### Method 1: PyTorch HuggingFace

Basic method using PyTorch and HuggingFace to load and inference models.

File location: `Deploy/pytorch/model_infer.py`

Usage:
```bash
python Deploy/pytorch/model_infer.py
```

Features:
- Easy to change models
- Suitable for development and testing
- Direct inference execution

### Method 2: vLLM Server

vLLM provides high-speed inference for Large Language Models.

Starting the server:
```bash
CUDA_VISIBLE_DEVICES=1 vllm serve <model-name> --port 8006
```

Example:
```bash
CUDA_VISIBLE_DEVICES=1 vllm serve meta-llama/Llama-2-7b-hf --port 8006
```

Features:
- Fast inference speed
- Automatic batching support
- Optimized for production

### Method 3: Triton Inference Server

Deploy models using Triton Server with Docker.

Steps:
```bash
cd Deploy/work-directory
docker-compose up
```

Configuration file: `Deploy/work-directory/docker-compose.yml`

Features:
- Production-ready
- Multiple model support
- Scalable and robust

## Running the API

After loading the model using one of the three methods above, start the API server:

```bash
cd src/app_vllm
uvicorn api:app --host 0.0.0.0 --port 8000 --reload
```

The API will be available at: http://localhost:8000

API endpoints:
- Documentation: http://localhost:8000/docs
- Health check: http://localhost:8000/health

## Running Gradio Interface

After the API is running successfully, you can start the Gradio interface:

```bash
cd src/app_vllm
CUDA_VISIBLE_DEVICES=1 python gradio_app.py
```

The Gradio interface will start and the URL will be displayed in the terminal.

## Project Structure

```
.
├── Deploy/
│   ├── pytorch/
│   │   └── model_infer.py
│   └── work-directory/
│       └── docker-compose.yml
├── src/
│   └── app_vllm/
│       ├── api.py
│       └── gradio_app.py
└── README.md
```

## Complete Workflow

1. Choose a deployment method: PyTorch, vLLM, or Triton
2. Load the model following the corresponding instructions
3. Start the API server
4. Run the Gradio interface (optional)
5. Use the model via API or Gradio UI

## Notes

- Ensure GPU has sufficient VRAM for the model
- For vLLM and Gradio, specify GPU using CUDA_VISIBLE_DEVICES
- Triton Server requires Docker and Docker Compose installed
- Check logs if errors occur when starting services

## Contributing

Contributions are welcome! Please create an issue or pull request.

## License

MIT License

## Contact

For questions or support, please open an issue on GitHub.

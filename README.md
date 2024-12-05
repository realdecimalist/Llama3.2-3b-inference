# Llama3 Docker Inference Setup

This repository contains the Docker setup for running inference with the Llama3.2-3B-Instruct model.

## Prerequisites

1. **Hardware Requirements**
   - NVIDIA GPU with CUDA support
   - Sufficient RAM (at least 16GB recommended)
   - At least 20GB free disk space

2. **Software Requirements**
   - Docker installed
   - NVIDIA Container Toolkit installed
   - NVIDIA drivers installed

## Model Access

1. Request access to Llama 3.2 models from Meta:
   - Visit [llama.meta.com](https://llama.meta.com)
   - Fill out the form and request access to Llama 3.2 models
   - Download the Llama3.2-3B-Instruct model

2. Place the model files in:
   ```
   /root/.llama/checkpoints/Llama3.2-3B-Instruct/
   ```

   Required files:
   - tokenizer.model
   - params.json
   - consolidated.00.pth
   - checklist.chk

## Installation & Setup

1. Install Docker:
   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   ```

2. Install NVIDIA Container Toolkit:
   ```bash
   distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
   curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
   curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
   sudo apt-get update
   sudo apt-get install -y nvidia-container-toolkit
   sudo systemctl restart docker
   ```

3. Pull the Docker image:
   ```bash
   docker pull decimalist/llama3-inference:latest
   ```

## Running the Model

1. Run the container:
   ```bash
   docker run --gpus all \
       -v /root/.llama/checkpoints/Llama3.2-3B-Instruct:/root/.llama/checkpoints/Llama3.2-3B-Instruct \
       --rm -it decimalist/llama3-inference:latest
   ```

2. Inside the container, run the test script:
   ```bash
   python3 /app/test_model.py
   ```

## Troubleshooting

1. If you see "docker: Error response from daemon: could not select device driver", install nvidia-container-toolkit
2. If you get CUDA errors, ensure your NVIDIA drivers are properly installed
3. If the model fails to load, verify all model files are in the correct location

## Support

If you encounter any issues, please check:
1. All prerequisite software is installed
2. Model files are correctly placed
3. You have sufficient system resources

## License

The Docker setup is provided under MIT license. The Llama3 model is subject to Meta's license terms.

Note: This setup is for inference only and is not intended for training or fine-tuning.

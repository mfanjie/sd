# Start from the NVIDIA CUDA base image with CUDA 12.0 and cuDNN
FROM nvidia/cuda:12.0.0-devel-ubuntu22.04

# Install necessary system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-pip \
    python3-dev \
    git \
    curl \
    libffi-dev \
    libssl-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    && rm -rf /var/lib/apt/lists/*

# Upgrade pip and install Jupyter Notebook
RUN pip3 install --no-cache-dir --upgrade pip && \
    pip3 install --no-cache-dir \
    notebook

# Install popular ML packages including transformers, numpy, pandas
RUN pip3 install --no-cache-dir \
    transformers \
    numpy \
    pandas \
    scikit-learn \
    matplotlib \
    seaborn \
    tensorflow \
    torch \
    torchvision \
    torchaudio \
    jupyterlab

# Install nvidia-smi to monitor GPU usage
RUN apt-get update && apt-get install -y --no-install-recommends \
    nvidia-utils-525 \
    && rm -rf /var/lib/apt/lists/*

# Set up working directory
WORKDIR /workspace

# Expose the port Jupyter Notebook will use
EXPOSE 8888

# Set the entrypoint to start Jupyter Notebook without password or token
ENTRYPOINT ["python3.10", "/usr/local/bin/jupyter-notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
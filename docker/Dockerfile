FROM nvcr.io/nvidia/cuda:12.8.1-cudnn-devel-ubuntu22.04

# Install necessary dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    python3 \
    python3-pip \
    python3-dev \
    python3-venv \
    git \
    vim \
    build-essential \
    libcairo2 \
    libaio-dev \
    && rm -rf /var/lib/apt/lists/*


# Install Jupyter Notebook and install star-vector from local directory
RUN pip install --upgrade pip setuptools wheel packaging

# Copy and install star-vector
COPY . /tmp/star-vector
RUN pip install /tmp/star-vector

# Install flash-attn with build dependencies
RUN pip install flash-attn --no-build-isolation

# Cleanup unneeded packages
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*
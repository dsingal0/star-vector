FROM nvcr.io/nvidia/cuda:12.8.1-cudnn-devel-ubuntu22.04

# Install necessary dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    python3 \
    python3-pip \
    python3-venv \
    git \
    vim \
    build-essential \
    libcairo2 \
    libaio-dev \
    && rm -rf /var/lib/apt/lists/*


# Install Jupyter Notebook, clone and install star-vector and dependencies
#RUN pip install --upgrade pip && pip install jupyter deepspeed \
#    && git clone https://github.com/dsingal0/star-vector.git /tmp/star-vector \
#    && pip install /tmp/star-vector \
#    && rm -rf /tmp/star-vector

COPY . /tmp/star-vector
RUN pip install /tmp/star-vector

# Cleanup unneeded packages
RUN apt-get purge -y --auto-remove \
    git \
    build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Expose Jupyter Notebook port
EXPOSE 8888

WORKDIR /workspace

# Launch Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]

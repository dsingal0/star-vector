#FROM pytorch/pytorch:2.5.1-cuda12.4-cudnn9-devel
# docker build -f docker/Dockerfile -t star . && docker run --gpus all -it --rm --network host --ipc host -v /home/dsingal/.cache:/root/.cache -v $PWD/test:/app/test star
FROM nvcr.io/nvidia/cuda:12.6.0-cudnn-devel-ubuntu22.04
#FROM nvcr.io/nvidia/pytorch:25.04-py3
# Install necessary dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    vim \
    tmux \
    nload \
    python3 \
    python3-dev \
    python3-venv \
    python-is-python3 \
    python3-pip \
    build-essential \
    libcairo2 \
    libaio-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp/requirements.txt
RUN pip install --upgrade pip && pip install -r /tmp/requirements.txt
COPY . /tmp/star-vector
RUN pip install /tmp/star-vector
WORKDIR /app
CMD ["python", "test/test.py"]
# # Install Jupyter Notebook, clone and install star-vector and dependencies
# RUN pip install --upgrade pip && pip install jupyter deepspeed \
#     && git clone https://github.com/joanrod/star-vector.git /tmp/star-vector \
#     && pip install /tmp/star-vector \
#     && rm -rf /tmp/star-vector

#COPY . /tmp/star-vector

#RUN pip install /tmp/star-vector
# Base NVidia CUDA Ubuntu image
FROM pytorch/pytorch:latest as build
ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /app
ARG CUDA_DOCKER_ARCH=all

RUN apt-get update -y && \
    apt-get install -y build-essential cmake wget && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb && \
    dpkg -i cuda-keyring_1.1-1_all.deb && \
    apt-get update && \
    apt-get -y install cuda 
    
RUN apt-get install -y python3 python3-pip python-is-python3 && \
    python3 -m pip install --upgrade pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*   

ENV TORCH_CUDA_ARCH_LIST="8.0;8.6+PTX;8.9;9.0" 

# Install AutoGPTQ
ARG AUTOGPTQ="0.2.2"
ENV CUDA_VERSION=""
ENV GITHUB_ACTIONS=true
ENV TORCH_CUDA_ARCH_LIST="8.0;8.6+PTX;8.9;9.0" 

RUN pip install --force-reinstall torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

COPY req.txt ./req.txt

RUN pip3 install -r req.txt

RUN mkdir /root/dev
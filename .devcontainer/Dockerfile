# Base image – Python 3.11 (small, includes pip)
FROM mcr.microsoft.com/devcontainers/python:3.11

# System deps for PDF, FAISS, Neo4j driver, etc.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
        gcc \
        g++ \
        make \
        libfaiss-dev \
        libssl-dev \
        default-jre-headless \
        poppler-utils \
        tesseract-ocr && \
    rm -rf /var/lib/apt/lists/*

# Python libs – keep them in one layer for caching
COPY requirements.txt /tmp/
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Create a non‑root user (codespaces already does this)
ENV HOME /workspaces/paper-kg-assistant
WORKDIR $HOME

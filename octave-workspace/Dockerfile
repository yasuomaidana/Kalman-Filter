FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y \
    octave \
    liboctave-dev \
    octave-control \
    octave-signal \
    python3 \
    python3-pip \
    curl \
    git \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

# Install Language Server
RUN npm install -g matlab-language-server

# Install UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh \
    && mv /root/.local/bin/uv /usr/local/bin/

# Install JupyterLab, the Octave Kernel, and Jupytext using uv
RUN uv pip install --system --no-cache jupyterlab octave_kernel jupytext jupyterlab-lsp && \
    python3 -m octave_kernel install

# Create a non-root user for security
RUN useradd -m -s /bin/bash jovyan
USER jovyan

# Set the working directory
WORKDIR /home/jovyan/work

EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--ServerApp.token=", "--ServerApp.password="]

FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies (including texinfo for docs and gnuplot for plotting)
RUN apt-get update && apt-get install -y \
    octave \
    liboctave-dev \
    octave-control \
    octave-signal \
    python3 \
    python3-pip \
    python3-sympy \
    curl \
    git \
    build-essential \
    texinfo \
    gnuplot \
    && rm -rf /var/lib/apt/lists/*

# Install UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh \
    && mv /root/.local/bin/uv /usr/local/bin/

# Install JupyterLab, the Octave Kernel, and Jupytext using uv
RUN uv pip install --system --no-cache jupyterlab octave_kernel jupytext && \
    python3 -m octave_kernel install

# Enable "As-You-Type" Autocompletion by default (Continuous Hinting)
# This overrides the default JupyterLab settings system-wide.
RUN mkdir -p /usr/local/share/jupyter/lab/settings && \
    echo '{"@jupyterlab/completer-extension:manager": {"continuousHinting": true}}' > /usr/local/share/jupyter/lab/settings/overrides.json

# Create a non-root user for security
RUN useradd -m -s /bin/bash jovyan
USER jovyan

# Set the working directory
WORKDIR /home/jovyan/work

EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--ServerApp.token=", "--ServerApp.password="]

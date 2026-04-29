FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# 1. Install system dependencies
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

# 2. Install UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh \
    && mv /root/.local/bin/uv /usr/local/bin/

# 3. Install Jupyter, Octave Kernel, and Jupytext
RUN uv pip install --system --no-cache jupyterlab octave_kernel jupytext && \
    python3 -m octave_kernel install

# 4. Create user with UID 1000 (Standard for Host-to-Container mapping)
# RUN useradd -m -u 1000 -s /bin/bash jovyan

# 5. Global Settings (Autocompletion + DARK THEME)
RUN mkdir -p /usr/local/share/jupyter/lab/settings && \
    echo '{ \
        "@jupyterlab/completer-extension:manager": {"continuousHinting": true}, \
        "@jupyterlab/apputils-extension:themes": {"theme": "JupyterLab Dark"} \
    }' > /usr/local/share/jupyter/lab/settings/overrides.json

# 6. Install Symbolic Package as Root (Global)
# This prevents permission issues in the user's home directory
RUN octave --eval "pkg install -forge -global symbolic; pkg load symbolic; syms x; diff(x^2, x);"

# 7. Configure .octaverc
# RUN echo "setenv('PYTHON', '/usr/bin/python3');" >> /home/jovyan/.octaverc && \
#    echo "pkg load control;" >> /home/jovyan/.octaverc && \
#    echo "pkg load signal;" >> /home/jovyan/.octaverc && \
#    echo "pkg load symbolic;" >> /home/jovyan/.octaverc && \
#    chown -R jovyan:jovyan /home/jovyan

RUN useradd -m -s /bin/bash jovyan
USER jovyan
WORKDIR /home/jovyan/work

EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--ServerApp.token=", "--ServerApp.password="]

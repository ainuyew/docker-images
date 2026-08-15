# 1. Start from Ubuntu LTS (24.04 Noble or 22.04 Jammy)
FROM ubuntu:24.04

# 2. Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# 3. Install system dependencies and set up the user
RUN apt-get update && apt-get install -y --no-install-recommends \
      git \
      ca-certificates \
      curl \
      bash \
      python3 \
      python3-pip \
      python3-dev \
      python3-venv \
      build-essential \
      less \
      ripgrep \ 
      vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
  

# 4. Create a non-root user for better security
ARG USERNAME=ubuntu
#ARG UID=1001
#ARG GID=1001
#RUN groupadd -g ${GID} ${USERNAME} && \
#    useradd -m -u ${UID} -g ${GID} -s /bin/bash ${USERNAME}

# 5. Create configuration directories
RUN mkdir -p /home/${USERNAME}/.config/opencode && \
    mkdir -p /home/${USERNAME}/.local/share/opencode && \
    chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}

# 6. Add OpenCode to PATH
ENV PATH="/home/${USERNAME}/.opencode/bin:${PATH}"

# 7. Switch to the non-root user for subsequent commands
USER ${USERNAME}
WORKDIR /home/${USERNAME}

# 8. Install OpenCode via the official installer
RUN curl -fsSL https://opencode.ai/install | bash

# 9. create virtual environment
RUN python3 -m venv .venv
ENV PATH="/home/${USERNAME}/.venv/bin:$PATH"

# 10. Install Python packages for venv
RUN python3 -m pip install numpy \
                           matplotlib \
                           seaborn \
                           pandas \
                           pytest \
                           streamlit \
                           altair

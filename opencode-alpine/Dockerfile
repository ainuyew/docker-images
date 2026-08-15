# 1. Start from the official minimal Arch Linux image
FROM alpine:latest

# 2. Install system dependencies and set up the user
RUN apk add --no-cache \
      git \
      ca-certificates \
      curl \
      bash \
      python3 \
      py3-pip \
      sudo \
      less \
      vim

# 3. Set the root password non-interactively
#RUN echo 'root:sbegy2pt' | chpasswd

# 4. Create a non-root user for better security
ARG USERNAME=opencode
ARG UID=1000
ARG GID=1000

RUN addgroup -g ${GID} ${USERNAME} && \
    adduser -D -u ${UID} -G ${USERNAME} -s /bin/bash ${USERNAME}

# 5. Create configuration directories
RUN mkdir -p /home/${USERNAME}/.config/opencode && \
    mkdir -p /home/${USERNAME}/.local/share/opencode && \
    chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}

# 6. Switch to the non-root user for subsequent commands
USER ${USERNAME}
WORKDIR /home/${USERNAME}

# 7. Install OpenCode via the official installer
RUN curl -fsSL https://opencode.ai/install | bash
ENV PATH="/home/${USERNAME}/.opencode/bin:$PATH"

# 8. create virtual environment
RUN python3 -m venv .venv
ENV PATH="/home/${USERNAME}/.venv/bin:$PATH"

# 9. Install Python packages for venv
RUN python3 -m pip install numpy \
                           matplotlib \
                           seaborn \
                           pandas \
                           pytest 
                          


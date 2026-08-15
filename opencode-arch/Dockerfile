# 1. Start from the official minimal Arch Linux image
FROM archlinux:base

# 2. Install system dependencies and set up the user
#    -Syu updates the package list and upgrades all packages
#    --noconfirm automatically answers 'yes' to prompts
#    -Scc cleans the package cache to keep the image small
RUN pacman -Syu --noconfirm \
      git \
      ca-certificates \
      curl \
      bash \
      opencode \
      python \
      python-pip \
      sudo \
      less \
      ripgrep \
      vi \
  && pacman -Scc --noconfirm


# 3. Create a non-root user for better security
ARG USERNAME=opencode
ARG UID=1000
ARG GID=1000
RUN groupadd -g ${GID} ${USERNAME} && \
    useradd -m -u ${UID} -g ${GID} -s /bin/bash ${USERNAME}

# 4. Change ownership of non-root user directory
RUN mkdir -p /home/opencode/.config/opencode
RUN mkdir -p /home/opencode/.local/share/opencode
RUN chown -R opencode:opencode /home/opencode

# 5. Switch to the non-root user for subsequent commands
USER ${USERNAME}
WORKDIR /home/${USERNAME}

# 6. create virtual environment
RUN python3 -m venv .venv
ENV PATH="/home/${USERNAME}/.venv/bin:$PATH"

# 7. Install Python packages for venv
RUN python3 -m pip install numpy \
                           matplotlib \
                           seaborn \
                           pandas \
                           pytest \
                           streamlit \
                           altair


# Use the official minimal Arch Linux image
FROM archlinux:base

# Update the system, install tools, and delete the cache to save space
RUN pacman -Syu --noconfirm \
    && pacman -Scc --noconfirm

# Set your entrypoint
CMD ["/bin/bash"]


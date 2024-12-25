# Use Ubuntu image base
FROM ubuntu:latest

# Environment variables for versions
ARG GO_VERSION=1.21.5
ARG NODE_VERSION=22.12.0

# Update package list, install dependencies, and clean up
RUN apt-get update && apt-get install -y \
    git \
    gnupg2 \
    wget \
    curl \
    nano \
    unzip \
    lsb-release \
    ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install oh-my-posh
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh \
    && chmod +x /usr/local/bin/oh-my-posh

# Install oh-my-posh themes
RUN mkdir -p /etc/skel/.poshthemes \
    && wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip \
    && unzip themes.zip -d /etc/skel/.poshthemes \
    && rm themes.zip

# Configure oh-my-posh
RUN echo 'eval "$(oh-my-posh init bash --config /etc/skel/.poshthemes/paradox.omp.json)"' >> /etc/skel/.bashrc

# Install Go
RUN curl -fsSL https://golang.org/dl/go${GO_VERSION}.linux-amd64.tar.gz -o /tmp/go.tar.gz && \
    tar -C /usr/local -xzf /tmp/go.tar.gz && \
    rm /tmp/go.tar.gz

# Add Go to PATH
ENV PATH=$PATH:/usr/local/go/bin

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - && \
    apt-get install -y nodejs

# Check versions
RUN go version && node -v && npm -v

# Set default shell
SHELL ["/bin/bash", "-c"]

# Default command
CMD ["bash"]

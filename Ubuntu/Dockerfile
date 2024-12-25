# Use Ubuntu image base
FROM ubuntu:latest

# Update package list and install dependencies must have
RUN apt-get update && apt-get install -y \
    git \
    gpg \
    wget \
    curl \
    nano \
    unzip \
    gnupg2 \
    lsb-release \
    ca-certificates

# Install oh-my-posh
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh \
    && chmod +x /usr/local/bin/oh-my-posh

# Install oh-my-posh theme
RUN mkdir -p ~/.poshthemes \
    && wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip \
    && unzip themes.zip -d ~/.poshthemes \
    && rm themes.zip

# Create oh-my-posh config file
RUN echo 'eval "$(oh-my-posh init bash --config ~/.poshthemes/paradox.omp.json)"' >> ~/.bashrc

# Download and install Go
RUN curl -fsSL https://golang.org/dl/go1.23.4.linux-amd64.tar.gz -o /tmp/go.tar.gz && \
    tar -C /usr/local -xzf /tmp/go.tar.gz && \
    rm /tmp/go.tar.gz

# Config Go path
ENV PATH=$PATH:/usr/local/go/bin

# Add NodeSource repository for Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -

# Install Node.js and npm
RUN apt-get install -y nodejs

# Check installed version
RUN go version
RUN node -v
RUN npm -v

# Default command
CMD ["bash"]
# Use Ubuntu image base
FROM ubuntu:latest

# Update package list and install dependencies must have
RUN apt-get update && apt-get install -y \
    git \
    gpg \
    wget \
    curl \
    gnupg2 \
    lsb-release \
    ca-certificates

# Download and install Go
RUN curl -fsSL https://golang.org/dl/go1.23.4.linux-amd64.tar.gz -o /tmp/go.tar.gz && \
    tar -C /usr/local -xzf /tmp/go.tar.gz && \
    rm /tmp/go.tar.gz

# Config Go path
ENV PATH=$PATH:/usr/local/go/bin

# Check Go version
RUN go version

# Add NodeSource repository for Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -

# Install Node.js and npm
RUN apt-get install -y nodejs

# Check version Node.js and npm
RUN node -v
RUN npm -v

# Default command
CMD ["bash"]
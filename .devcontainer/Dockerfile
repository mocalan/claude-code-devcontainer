# Use official DevContainer base image
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Install system dependencies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        curl wget git make build-essential ca-certificates \
        postgresql-client \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install Node.js (required for Claude Code)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs

# Install Go
ENV GO_VERSION=1.24.2
ENV GOPATH=/go
ENV GOROOT=/usr/local/go
ENV PATH=$GOROOT/bin:$GOPATH/bin:$PATH
RUN ARCH=$(case $(uname -m) in x86_64) echo amd64 ;; aarch64) echo arm64 ;; *) echo amd64 ;; esac) && \
    curl -fsSL https://go.dev/dl/go${GO_VERSION}.linux-${ARCH}.tar.gz | tar -xzC /usr/local

# Set up vscode user environment
ARG USERNAME=vscode
USER root

# Create directories and set ownership
RUN mkdir -p /go /workspace \
    && mkdir -p /home/$USERNAME/.vscode-server/data \
    && chown -R $USERNAME:$USERNAME /go /workspace /home/$USERNAME \
    && chmod -R 755 /go

# Install Claude Code globally
RUN npm install -g @anthropic-ai/claude-code

# Configure shell and environment for vscode user
USER $USERNAME
RUN echo 'export GOPATH=/go' >> ~/.bashrc \
    && echo 'export GOROOT=/usr/local/go' >> ~/.bashrc \
    && echo 'export PATH=$GOROOT/bin:$GOPATH/bin:$PATH' >> ~/.bashrc \
    && git config --global init.defaultBranch main \
    && git config --global pull.rebase false

WORKDIR /workspace

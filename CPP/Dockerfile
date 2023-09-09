# Use the clangd/clangd:latest image as the base image
# FROM clangd/clangd:latest
FROM registry.gitlab.com/mmoelle1/docker-clang:16ubuntu20.04

# RUN apt-get update && apt-get install -y clangd
# Install Python3 and necessary Python packages
RUN apt-get update && apt-get install -y python3 python3-pip locales && \
    rm -rf /var/lib/apt/lists/* && \
    sed -in '/# en_US.UTF-8 UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8 && \
    pip3 install 'requests[security]' && \
    apt-get update && apt-get install -y clangd gcc

# Install additional C++ development tools if needed
# For example, you can install GCC for C++ development:
# RUN apt-get update && apt-get install -y gcc

# Set the working directory to /workspace
WORKDIR /workspace

# Expose the language server's port (default is 5000)
# EXPOSE 5000

# Optionally, you can specify the entry point for your language server.
# If you have a script to start your language server, you can use it here.
# For example, if your server script is named "start_server.sh":
# ENTRYPOINT ["/bin/bash", "start_server.sh"]

# Alternatively, you can specify the command to start your language server.
# For example, if you want to start clangd directly:
CMD ["clangd"]

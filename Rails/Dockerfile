# Use the official Rails 7 image as the base image
FROM bitnami/rails:7.0.8

# Set the working directory
WORKDIR /app

# Install additional dependencies for your language server, if needed
# For example, if you're using Solargraph as the language server:
RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    zlib1g-dev

# Install your language server (e.g., Solargraph)
RUN gem install solargraph -v 0.49.0

# Copy your Rails application code into the container
COPY . /app

# Set any environment variables needed for your Rails application

# Expose any necessary ports

# Start your Rails application or language server process
CMD [ "rails", "server" ]

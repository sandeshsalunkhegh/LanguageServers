# Use an official Node.js runtime as the base image
FROM node:20

# Set the working directory inside the container
WORKDIR /app
COPY ./file.js /app

# Install quick-lint-js globally
RUN npm install -g quick-lint-js

# Expose the language server's port (if applicable)
# Replace 2089 with the port number that quick-lint-js uses
EXPOSE 2089

# Specify the command to run when the container starts
CMD ["quick-lint-js", "file.js"]

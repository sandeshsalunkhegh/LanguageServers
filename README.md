# LanguageServers - Language Server Docker Implementations Repository

This repository contains Docker implementations of Language Servers for various programming languages. Language Servers provide language-specific code analysis and rich language features for code editors and Integrated Development Environments (IDEs). By containerizing these Language Servers, you can easily integrate them into your development environment.

## Table of Contents

- [Supported Language Servers](#supported-language-servers)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Usage](#usage)

## Supported Language Servers

- [Language Server for C++](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/CPP)
- [Language Server for C# - .NET](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/CSharp)
- [Language Server for Go](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/Go)
- [Language Server for Java](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/Java)
- [Language Server for JavaScript/NodeJS](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/JavaScript)
- [Language Server for Python3](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/Python3)
- [Language Server for Rails](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/Rails)
- [Language Server for Ruby](https://github.com/sandeshsalunkhegh/LanguageServers/tree/main/Ruby)

## Getting Started

Follow these steps to get started with the Language Servers in Docker:

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your system.

## Usage

### For all Language Servers other than C# - .NET

To use this language server, build it first with below command
```bash
docker build -t javascript . # For AMD-64 / Linux-64 based OS
```
Note: Add `linux/x86_64` at the end if you want to run the same in AMD-64 / Linux-64 OS based enironment.

Adjust the port mapping (-p) as needed based on the Language Server's port if you want to expose the language server to a certain port.
Make sure you expose the port using `EXPOSE <port-number>` in the Dockerfile before the `CMD ['your-iniatiator-command-here']`.

### For C# - .NET Language Server

To use this language server, build it first with below command
```bash
docker build -t javascript . # For AMD-64 / Linux-64 based OS
```
Note: Add `linux/x86_64` at the end if you want to run the same in AMD-64 / Linux-64 OS based enironment.
Make sure the other files are also added appropriately such as `file.csproj` which might vary depending upon your use-case.
Here `fle.csproj` is the project file for which you want to run the language server.


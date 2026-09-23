README START

# Cyber Assistant

> A self-hosted AI assistant project focused on cybersecurity learning, Linux administration, technical documentation, and AI infrastructure experimentation.

![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-blue)
![Docker](https://img.shields.io/badge/platform-Docker-2496ED)
![Linux](https://img.shields.io/badge/platform-Linux-black)

## Overview

Cyber Assistant is a self-hosted AI environment built as a hands-on cybersecurity and infrastructure project.

The current implementation focuses on deploying and managing local AI services with Docker, integrating Ollama with Open WebUI, maintaining persistent model storage, and documenting the operational and hardware limitations encountered during development.

The project is primarily intended to demonstrate practical skills in:

- Linux administration
- Docker and Docker Compose
- Self-hosted AI infrastructure
- Git and GitHub workflows
- System troubleshooting
- Infrastructure documentation
- Cybersecurity-focused experimentation

## Current Implementation

The current version provides:

- Dockerized Ollama deployment
- Open WebUI interface
- Persistent Docker volumes
- Local LLM execution
- Dedicated Docker networking
- Linux-based deployment
- Git version control
- Reproducible container configuration

### Models Tested

The following models were tested during development:

- `qwen3:4b`
- `qwen3:8b`

Local inference performance was evaluated on the development laptop.

The results showed that local AI execution is technically possible, but the available hardware is not suitable for comfortable day-to-day local LLM inference.

## Architecture

    User
      |
      | HTTP :3000
      v
    Open WebUI
    cyber-open-webui
      |
      | Docker network
      | HTTP :11434
      v
    Ollama
    cyber-ollama
      |
      v
    Persistent Models
    docker_ollama_data

See the detailed documentation:

- [Architecture](docs/architecture.md)
- [Deployment Guide](docs/deployment.md)
- [Hardware & Performance Environment](docs/hardware.md)
- [Performance Evaluation](docs/performance.md)
- [Troubleshooting Case Studies](docs/troubleshooting.md)

## Technology Stack

### Implemented

- Linux
- Docker
- Docker Compose
- Ollama
- Open WebUI
- Git
- GitHub

### Planned

The following components are part of the future roadmap:

- FastAPI
- PostgreSQL
- Redis
- Retrieval-Augmented Generation (RAG)
- Model Context Protocol (MCP)
- CVE lookup
- IOC analysis
- Log analysis
- Threat intelligence integrations
- Automated security reporting

Planned components are intentionally separated from the current implementation.

## Hardware and Performance

Development and testing were performed on a Linux laptop with:

- Intel Core i5-1035G1
- 4 cores / 8 threads
- 32 GB RAM
- Integrated Intel graphics
- NVMe SSD
- Zorin OS 18.1

An Intel integrated GPU/Vulkan acceleration experiment was also performed.

The experiment successfully exposed the Intel GPU to the Ollama container, but the end-to-end workload did not provide sufficient performance improvement to justify making GPU acceleration a project requirement.

The final baseline configuration therefore remains hardware-independent.

Detailed results are documented in:

[Performance Evaluation](docs/performance.md)

## Deployment

### Requirements

- Linux
- Docker Engine
- Docker Compose
- Git

### Start the Environment

    docker compose -f docker/compose.yml up -d

### Check Services

    docker compose -f docker/compose.yml ps

### Stop Services

    docker compose -f docker/compose.yml down

Open WebUI:

    http://localhost:3000

Ollama:

    http://localhost:11434

For detailed deployment instructions, see:

[Deployment Guide](docs/deployment.md)

## Persistent Storage

The project uses external Docker volumes for persistent application data:

- `docker_ollama_data`
- `docker_openwebui_data`

These volumes allow containers to be recreated without losing downloaded models or Open WebUI application data.

## Engineering Lessons

The project is also used to document real infrastructure problems encountered during development, including:

- Docker Compose configuration errors
- Container name conflicts
- Persistent volume migration
- GitHub SSH authentication
- Local LLM performance limitations
- Intel integrated GPU experimentation
- Linux and infrastructure troubleshooting

The objective is not only to make the system work, but also to document the engineering reasoning behind the decisions.

See:

[Troubleshooting Case Studies](docs/troubleshooting.md)

## Project Structure

    cyber-assistant/
    |
    +-- docs/
    |   +-- architecture.md
    |   +-- deployment.md
    |   +-- hardware.md
    |   +-- performance.md
    |   +-- troubleshooting.md
    |
    +-- docker/
    |   +-- compose.yml
    |
    +-- prompts/
    +-- scripts/
    +-- data/
    +-- app/
    |
    +-- README.md
    +-- CHANGELOG.md
    +-- CONTRIBUTING.md
    +-- SECURITY.md
    +-- ROADMAP.md
    +-- TODO.md
    +-- LICENSE

## Roadmap

### Phase 1 - Infrastructure

- [x] GitHub repository
- [x] Docker environment
- [x] Docker Compose
- [x] Ollama
- [x] Open WebUI
- [x] Persistent model storage
- [x] Linux deployment

### Phase 2 - Documentation

- [x] Architecture documentation
- [x] Deployment guide
- [x] Hardware documentation
- [x] Performance evaluation
- [x] Troubleshooting case studies
- [ ] Screenshots

### Phase 3 - Application Layer

- [ ] FastAPI backend
- [ ] PostgreSQL
- [ ] Redis
- [ ] RAG pipeline
- [ ] MCP integration

### Phase 4 - Security Features

- [ ] CVE lookup
- [ ] IOC analysis
- [ ] Log analysis
- [ ] Threat intelligence integration
- [ ] Automated security report generation

## Author

**Danilo Manoel**

IT Support Technician transitioning into Cybersecurity.

Hands-on interests:

- Linux
- Docker
- Cybersecurity
- AI infrastructure
- Networking
- Infrastructure automation

## License

This project is licensed under the MIT License.

README END

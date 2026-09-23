# Deployment Guide

## Overview

Cyber Assistant runs as a Docker Compose application on a Linux host.

The current deployment consists of two services:

- Ollama
- Open WebUI

Persistent application data is stored in external Docker volumes.

## Requirements

The current deployment requires:

- Linux
- Docker Engine
- Docker Compose
- Git
- Internet access for pulling container images and downloading models

No dedicated GPU is required for the baseline configuration.

## Clone the Repository

```bash
git clone git@github.com:Dmanoel/cyber-assistant.git
cd cyber-assistant

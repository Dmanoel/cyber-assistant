# Architecture

## Overview

Cyber Assistant currently uses a lightweight self-hosted architecture based on Docker, Ollama, and Open WebUI.

The current implementation is intentionally small and focused on local AI infrastructure rather than a full application backend.

## Current Architecture

```text
+-----------------------------+
|          User               |
|      Web Browser            |
+-------------+---------------+
              |
              | HTTP :3000
              v
+-----------------------------+
|         Open WebUI          |
|      cyber-open-webui       |
+-------------+---------------+
              |
              | Docker network
              | HTTP :11434
              v
+-----------------------------+
|           Ollama            |
|        cyber-ollama         |
+-------------+---------------+
              |
              v
+-----------------------------+
|      Persistent Models      |
|     docker_ollama_data      |
+-----------------------------+

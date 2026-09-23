# Troubleshooting Case Studies

## Overview

Cyber Assistant was developed as a hands-on infrastructure project. During development, several real-world issues were encountered involving Docker Compose, persistent storage, GitHub authentication, and local AI performance.

This document records selected problems, root causes, resolutions, and engineering lessons.

---

## Case Study 1 — Docker Compose Configuration Error

### Symptom

Docker Compose failed to parse the configuration and reported a YAML parser error:

did not find expected document start

### Investigation

The Compose file was inspected with:

docker compose -f docker/compose.yml config

The error was traced to malformed YAML structure and incorrect indentation.

### Resolution

The Compose file was rebuilt with a clean structure and validated with:

docker compose -f docker/compose.yml config --quiet

The configuration was then deployed successfully.

### Lesson Learned

Configuration should be validated before starting containers.

Recommended workflow:

Edit → Validate → Deploy → Check health

---

## Case Study 2 — Docker Container Name Conflict

### Symptom

Docker reported that the container name cyber-ollama was already in use.

### Investigation

Existing containers were inspected with:

docker ps -a

The containers cyber-ollama and cyber-open-webui were still present.

### Root Cause

The Compose configuration had changed while containers using the same explicit names still existed.

### Resolution

The existing containers were stopped and removed with:

docker stop cyber-ollama cyber-open-webui

docker rm cyber-ollama cyber-open-webui

Persistent volumes were preserved.

### Lesson Learned

Container lifecycle and persistent storage must be treated separately.

Removing a container does not mean removing its data.

---

## Case Study 3 — Persistent Volume Migration

### Symptom

After changing the Compose project name, Docker created new volumes named:

cyber-assistant_ollama_data

cyber-assistant_openwebui_data

The existing data was stored in:

docker_ollama_data

docker_openwebui_data

### Risk

Using the new volumes could have caused duplicate model storage and a fresh Open WebUI data directory.

### Investigation

Existing mounts were inspected with:

docker inspect cyber-ollama

docker inspect cyber-open-webui

The stored Ollama models were verified with:

docker exec cyber-ollama ollama list

The existing models included qwen3:4b and qwen3:8b.

### Resolution

The Compose configuration was updated to use the existing external volumes:

ollama_data → docker_ollama_data

openwebui_data → docker_openwebui_data

The temporary volumes were removed only after the correct volumes had been verified.

### Lesson Learned

Before changing infrastructure, identify the relationship between:

Container → Mount → Volume → Data

---

## Case Study 4 — GitHub SSH Authentication

### Symptom

Git operations failed with:

Permission denied (publickey).

### Investigation

The SSH configuration was checked with:

ls -la ~/.ssh

ssh-add -l

No identities were loaded in the SSH agent.

### Resolution

An ED25519 key was created with:

ssh-keygen -t ed25519 -C "danilo.aems@gmail.com"

The key was added to the SSH agent with:

ssh-add ~/.ssh/id_ed25519

The public key was registered in GitHub.

Authentication was verified with:

ssh -T git@github.com

### Lesson Learned

GitHub authentication depends on both local SSH configuration and GitHub-side public key registration.

---

## Case Study 5 — Local LLM Performance

### Symptom

The local AI stack worked, but interactive inference was too slow for practical daily usage.

### Investigation

The following configurations were tested:

- qwen3:4b
- qwen3:8b
- CPU inference
- reasoning enabled
- reasoning disabled
- Open WebUI
- direct Ollama CLI

Observed qwen3:8b CPU throughput was approximately 3.6–3.9 tokens per second.

The smaller qwen3:4b model became substantially more responsive when reasoning was disabled.

### Resolution

The hardware limitation was documented rather than hidden.

The project retained a portable infrastructure configuration.

### Lesson Learned

A service can be available and functional while still being impractical for interactive use.

---

## Case Study 6 — Intel Integrated GPU Experiment

### Symptom

An attempt was made to improve Ollama performance using Intel integrated graphics.

### Experiment

The container was configured to expose /dev/dri and Intel/Vulkan-related environment variables were enabled.

The Intel integrated GPU was successfully detected.

### Result

GPU detection was successful, but the end-to-end workload did not justify making GPU acceleration a project requirement.

### Resolution

The experimental GPU configuration was removed from the baseline Compose file.

The final deployment does not require:

- /dev/dri
- Vulkan
- CUDA
- vendor-specific GPU settings

### Lesson Learned

Hardware detection alone does not prove that acceleration improves real application performance.

---

## Troubleshooting Philosophy

The project follows this workflow:

Observe → Reproduce → Inspect → Identify root cause → Apply the smallest safe change → Validate → Document

The objective is not only to restore functionality, but also to understand the failure and preserve the solution as reusable technical knowledge.

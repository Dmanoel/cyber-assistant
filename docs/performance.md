# Performance Evaluation

## Purpose

This document records the local AI performance tests performed during the development of Cyber Assistant.

The purpose of the evaluation was not to determine the fastest configuration, but to understand the practical limits of running local language models on the available development hardware.

## Test Environment

The tests were performed on the project's development laptop:

- Intel Core i5-1035G1
- 4 cores / 8 threads
- 32 GB RAM
- Integrated Intel graphics
- NVMe SSD
- Zorin OS 18.1
- Docker
- Ollama
- Open WebUI

## Models Tested

The main models evaluated were:

| Model | Size | Notes |
|---|---:|---|
| `qwen3:4b` | ~2.5 GB | Small local model |
| `qwen3:8b` | ~5.2 GB | Larger local model |

## CPU Inference Results

The `qwen3:8b` model was tested using CPU-based inference.

Observed throughput was approximately:

```text
3.6 - 3.9 tokens/second

# Hardware and Performance Environment

## Development System

The Cyber Assistant project was developed and tested on a Linux laptop with the following hardware:

| Component | Specification |
|---|---|
| CPU | Intel Core i5-1035G1 |
| CPU topology | 4 cores / 8 threads |
| RAM | 32 GB DDR4 |
| GPU | Integrated Intel graphics |
| Storage | NVMe SSD |
| Operating System | Zorin OS 18.1 |
| Container Runtime | Docker Engine |
| Orchestration | Docker Compose |

## Why Hardware Matters

Local LLM inference is strongly influenced by available CPU, memory bandwidth, GPU acceleration, model size, and inference configuration.

The project therefore treats hardware performance as an explicit engineering consideration rather than assuming that local AI inference will perform equally well on every system.

## Models Tested

The following models were tested during development:

- `qwen3:4b`
- `qwen3:8b`

The models were stored persistently using Docker volumes so that containers could be recreated without downloading the models again.

## CPU Inference

CPU-based inference was tested on the integrated-graphics development laptop.

The results showed that local inference was technically functional but could become too slow for practical day-to-day usage, particularly with larger models and reasoning-enabled configurations.

The project therefore does not depend on high local inference performance to demonstrate its infrastructure architecture.

## Intel iGPU / Vulkan Experiment

An Intel integrated GPU acceleration experiment was performed using the Ollama Docker container.

The experiment exposed:

```text
/dev/dri

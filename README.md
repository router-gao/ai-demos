# AI Demos — My VMware Demo Portfolio

**Hands-on AI demonstrations I delivered during my time at VMware: from GPU infrastructure and Kubernetes to generative AI, model fine-tuning and shared notebook environments.**

**English** | [简体中文](README.zh-CN.md)

This repository preserves my demo guides, lab configurations, embedded code examples, troubleshooting notes and recording links. The collection connects the infrastructure needed to run AI with the applications people can see and use: video analytics, image generation, local language models and model fine-tuning.

The original material largely records work from **2023–2024**. It includes practical VMware vSphere / ESXi and Tanzu Kubernetes Grid (TKGm) labs, alongside Google Colab experiments. It is intended for engineers, architects and technical audiences who want to understand the complete path from provisioning GPU resources to demonstrating an AI workload.

## Start here

- **Explore the portfolio:** use the demo map below, then open the linked guides for commands, configuration and recorded outputs.
- **Watch the demos:** open the [recording index](99-videos/demo-list.md).
- **Build a GPU application lab:** begin with [the tinykube GPU demo](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>), then add [GPU monitoring](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>).
- **Explore generative AI:** follow [Stable Diffusion on vGPU](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>) or [local Llama 2](<06-LLM-DEMO/12 - Llama 2 quick demo.md>).
- **Learn fine-tuning:** start with [GPT-2](<01-fine-tuning/32 - GPT2 fine-tuning in WDC T4 GPU.md>) or [BERT](<01-fine-tuning/33 - BERT fine-tuning in WDC T4 GPU.md>), then work through [Llama 2 with LoRA on Colab](<01-fine-tuning/21.2 - Lllama 2 Fine-tuning Demo - Colab, Fine-tuning ipynb file Go Through.md>).

## Demo map

| Area | What the material demonstrates | Entry point |
| --- | --- | --- |
| GPU infrastructure and computer vision | ESXi GPU passthrough, Ubuntu drivers, tinykube, NVIDIA GPU Operator and DeepStream-based video analytics; RTSP sources connect the application to live or prerecorded streams. | [GPU video analytics](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>) |
| GPU observability | DCGM exporter metrics collected by Prometheus and presented in Grafana, with GPU temperature, power, clocks and workload labels in the recorded output. | [Monitoring walkthrough](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>) |
| vGPU and image generation | ESXi and guest configuration, vGPU profiles and licensing, followed by Stable Diffusion through AUTOMATIC1111. | [Stable Diffusion demo](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>) |
| Local LLM inference | Conda / Anaconda, text-generation-webui and Llama 2 model loading in a GPU-enabled VM. | [Llama 2 quick demo](<06-LLM-DEMO/12 - Llama 2 quick demo.md>) |
| Model fine-tuning | GPT-2 on AG News; BERT cased/uncased models on GLUE/CoLA; Llama 2 7B with SAMSum, PEFT/LoRA and quantization on Colab. Includes training and inference examples. | [Fine-tuning guides](01-fine-tuning/) |
| Private AI platforms | Kubeflow deployment approaches using MicroK8s / Juju and Minikube / manifests. | [Kubeflow overview](<02-kubeflow-and-private-ai/01 - kubeflow deployment 101.md>) |
| Tanzu and shared notebooks | TKGm workload clusters, node pools, GPU passthrough and JupyterHub profiles that select CPU or GPU nodes, with NFS storage and MetalLB. | [JupyterHub on TKGm](<07-TKGm-GPU/TKGm GPU Cluster with JupyterHub (Jupyter Notebook).md>) |
| Supporting infrastructure experiments | A Redis 7.0.8 multi-instance testbed with memtier workload generation, stored in the DPU section. | [Redis testbed](<03-NVIDIA-DPU/redis-testbed-setup.md>) |

The collection covers several connected engineering responsibilities: preparing the platform, deploying applications, validating behavior, observing resource usage and documenting how to repeat a demonstration.

## What is in the repository

The original collection contains **42 Markdown files across eight directories**, plus a Git text-normalization configuration. Python training and inference examples, shell automation, Kubernetes YAML, Helm values and configuration snippets are embedded in the Markdown documents. There are no standalone Python scripts, shell scripts or Jupyter notebook files checked into this snapshot.

A useful way to read the material is:

```text
GPU and virtualization
  ESXi / vSphere + NVIDIA passthrough or vGPU
                 |
Guest operating system and GPU software
  Ubuntu / Windows + drivers + CUDA-related tooling
                 |
Application environment
  Kubernetes / TKGm / Kubeflow / JupyterHub / Conda
                 |
AI demonstrations
  Video analytics | Stable Diffusion | Llama 2 | Fine-tuning

Observability alongside the workflow
  nvidia-smi | DCGM + Prometheus + Grafana | Weights & Biases
```

These are alternative and complementary lab paths; an individual demo does not require every component.

## Documentation catalog

The links below cover every original topic document. The existing directory-level READMEs are short labels or empty placeholders; the substantive guides are linked directly here. Original filenames are retained.

### 01-fine-tuning — Model fine-tuning

- [Lessons learned: infrastructure, operations and model selection](<01-fine-tuning/01 - Lessons Learned during fine-tuning.md>)
- [Conda, Jupyter Notebook and a CPU-capable BERT example](<01-fine-tuning/02 - Conda and Jupyter notebook installation.md>)
- [Llama 2 on Colab: workflow, prerequisites and SAMSum](<01-fine-tuning/21.1 - Lllama 2 Fine-tuning Demo - Colab, Introduction and Pre-config.md>)
- [Llama 2 notebook walkthrough: conversion, LoRA and before/after inference](<01-fine-tuning/21.2 - Lllama 2 Fine-tuning Demo - Colab, Fine-tuning ipynb file Go Through.md>)
- [Manual text-generation-webui environment setup](<01-fine-tuning/30 - text-generation-webui manully installation.md>)
- [Weights & Biases setup and training charts](<01-fine-tuning/31 - wandb registration and sample charts.md>)
- [GPT-2 fine-tuning on a T4 with AG News](<01-fine-tuning/32 - GPT2 fine-tuning in WDC T4 GPU.md>)
- [BERT cased/uncased fine-tuning with GLUE/CoLA](<01-fine-tuning/33 - BERT fine-tuning in WDC T4 GPU.md>)

### 02-kubeflow-and-private-ai — Kubeflow and private AI

- [Kubeflow deployment options](<02-kubeflow-and-private-ai/01 - kubeflow deployment 101.md>)
- [MicroK8s and Juju lab notes](<02-kubeflow-and-private-ai/02 - microk8s kubeflow deployment.md>)
- [Minikube and Kubeflow manifests walkthrough](<02-kubeflow-and-private-ai/03 - minikube kubeflow deployment.md>)

### 03-NVIDIA-DPU — DPU-related testbed

- [Redis multi-instance testbed and memtier workload scripts](<03-NVIDIA-DPU/redis-testbed-setup.md>)

### 04-NVIDIA-GPU — GPU infrastructure, video analytics and monitoring

- [NVIDIA ecosystem and GPU FAQ](<04-NVIDIA-GPU/00 - NVIDIA FAQ.md>)
- [GPU on Kubernetes: drivers, Operator and resource allocation](<04-NVIDIA-GPU/01 - NVIDIA GPU on Kubernetes 101.md>)
- [GPU passthrough and video analytics on tinykube](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>)
- [Shell automation: tinykube, Helm, Harbor and network configuration](<04-NVIDIA-GPU/03 - tinykube configuration automation.md>)
- [DCGM, Prometheus and Grafana monitoring](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>)
- [Ubuntu GPU driver and CUDA installation notes](<04-NVIDIA-GPU/11 - NVIDIA GPU Driver and CUDA install on Ubuntu - Advanced.md>)
- [VLC as an RTSP monitoring client](<04-NVIDIA-GPU/21 - RTSP Client.md>)
- [RTSP sources and multi-stream video analytics integration](<04-NVIDIA-GPU/22 - RTSP Source Configuratrion and Demo Integration.md>)
- [GPU application onboarding checklist](<04-NVIDIA-GPU/90 - GPU Apps Onboarding Process.md>)

### 05-NVIDIA-vGPU — Virtual GPU and generative AI

- [vGPU concepts, profiles and software components](<05-NVIDIA-vGPU/00 - vGPU 101.md>)
- [Cloud License Service setup and guest activation](<05-NVIDIA-vGPU/01 - GPU License Service installation - Cloud License Service (CLS) instance.md>)
- [ESXi vGPU preparation checklist](<05-NVIDIA-vGPU/02 - vGPU Set up on ESXi.md>)
- [ESXi 8 vGPU software installation outline](<05-NVIDIA-vGPU/03 - vGPU Software Installation on ESXi 8.md>)
- [Ubuntu guest driver, licensing and video analytics](<05-NVIDIA-vGPU/04 - vGPU driver installation on GuestOS Ubuntu 22.04 Server LTS.md>)
- [Stable Diffusion with AUTOMATIC1111 on vGPU](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>)

### 06-LLM-DEMO — LLM deployment and tools

- [LLM tools and ecosystem notes](<06-LLM-DEMO/00 - Open Source Tools for LLM.md>)
- [Conda and Anaconda on Ubuntu and Windows](<06-LLM-DEMO/01 - Conda and Anaconda.md>)
- [text-generation-webui setup](<06-LLM-DEMO/02 - text-generation-webui.md>)
- [ChatGPT API note — brief pointer, no implementation](<06-LLM-DEMO/11 - ChatGPT API Demo.md>)
- [Local Llama 2 deployment and model loading](<06-LLM-DEMO/12 - Llama 2 quick demo.md>)
- [LangChain and ChatGPT — empty work-in-progress placeholder](<06-LLM-DEMO/13 - Langchain and Chatgpt quick demo (ongoing).md>)

### 07-TKGm-GPU — Tanzu GPU clusters and JupyterHub

- [JupyterHub: storage, load balancing and CPU/GPU profiles](<07-TKGm-GPU/TKGm GPU Cluster with JupyterHub (Jupyter Notebook).md>)
- [TKGm cluster bootstrap, node pools and GPU passthrough](<07-TKGm-GPU/TKGm GPU Workload Cluster Bootstrapping Demo.md>)

### 99-videos — Demo recordings

- [Recording index: deployment, applications, fine-tuning and notebooks](<99-videos/demo-list.md>)

## Demo recordings

The [video index](99-videos/demo-list.md) retains the original sequence:

| Series | Subject |
| --- | --- |
| Demo 1 | GPU passthrough, OS installation, tinykube application deployment and monitoring |
| Demo 2 | vGPU licensing, guest drivers and Stable Diffusion |
| Demo 3 | vGPU, Ubuntu, Conda / text-generation-webui and Llama 2 model loading |
| Demo 4 | Local fine-tuning setup, training and validation |
| Demo 5 | Colab fine-tuning and a Google Vertex AI recording |
| Demo 6 | Kubeflow installation; the listed recording is marked as raw footage without audio |
| Demo 7 | VCD / CSE heading only; no recording link is currently listed |
| Demo 8 | GPU cluster bootstrapping, JupyterHub deployment and its user interface |

Recordings are linked from Google Drive rather than stored in Git. Access depends on the sharing permissions of each file. The index has been reviewed; the external recordings have not been replayed or access-tested for this README.

## Reading and reusing the labs

Browse the Markdown directly on GitHub, or download the repository:

```bash
git clone https://github.com/router-gao/ai-demos.git
cd ai-demos
```

Choose one guide and review its environment before extracting its code blocks. There is no repository-wide installer or single application to launch.

The recorded environments include NVIDIA T4 GPUs, an A100 40 GB Colab runtime, ESXi / vCenter 8.x, Ubuntu 20.04 / 22.04 and Windows 10. Examples also reference tinykube Kubernetes 1.25.7, TKG 2.4 with Kubernetes 1.27.5, and JupyterHub Helm chart 3.1.0. These describe the original labs, not a current compatibility matrix or universal sizing recommendation.

The original guides preserve historical package versions, commands, screenshots and observations. Some dependencies are unpinned, some images refer to local paths or old Confluence exports, and some lab packages or registries require separate access. Reproducing a demo today may require adapting the instructions. This README update does not represent a fresh execution of the labs.

Use a disposable lab when trying the configuration examples: some shell blocks reset clusters or alter host networking, and some examples use lab credentials or relaxed access settings. Replace environment-specific values before use.

## Scope and completeness

- The **GPT-2 and BERT** examples simplify training for demonstration. The BERT sample compares predictions on a small set of sentences; it is not a general accuracy benchmark.
- The **Llama 2 fine-tuning** walkthrough records a before/after summarization example. Reported training time and memory usage belong to that particular lab run.
- The **DPU directory** currently contains Redis / memtier setup instructions. It does not document a completed DPU-offload implementation or performance comparison.
- The **ChatGPT API** file is a short note, and the **LangChain / ChatGPT** file is an empty work-in-progress entry.
- The **TKGm guide** includes populated cluster examples and a manual hybrid-node-pool procedure, alongside unfinished multiple-GPU and hybrid configuration headings.
- Some guides link to upstream projects or other teams' material; those references retain their original attribution.

## Author and context

Maintained by [router-gao](https://github.com/router-gao). This is my personal archive of AI demo work delivered during my VMware tenure, with supporting lab notes and references. Product names identify the technologies used in the demonstrations; upstream software and models remain subject to their respective licenses.


# AI Demos — 我在 VMware 期间的 AI 演示项目集

**记录我在 VMware 工作期间交付的 AI 技术演示：从 GPU 基础设施与 Kubernetes，到生成式 AI、模型微调和共享 Notebook 环境。**

[English](README.md) | **简体中文**

本仓库保存了我的演示指南、实验配置、文档内嵌代码、故障排查记录和录像链接。内容将 AI 运行所需的基础设施与可直接体验的应用连接起来，涵盖视频分析、图像生成、本地大语言模型和模型微调。

原始材料主要记录 **2023–2024 年**的工作，包括 VMware vSphere / ESXi、Tanzu Kubernetes Grid（TKGm）实验，以及 Google Colab 上的模型实验。适合希望理解从 GPU 资源准备到 AI 应用演示完整过程的工程师、架构师和技术交流参与者阅读。

## 从这里开始

- **了解项目全貌：**先看下方演示概览，再通过链接查看操作命令、配置和当时的运行输出。
- **观看演示：**打开[录像索引](99-videos/demo-list.md)。
- **搭建 GPU 应用实验：**从[tinykube GPU 演示](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>)开始，再加入[GPU 监控](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>)。
- **体验生成式 AI：**阅读[vGPU 上的 Stable Diffusion](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>)或[本地 Llama 2 演示](<06-LLM-DEMO/12 - Llama 2 quick demo.md>)。
- **学习模型微调：**先看[GPT-2](<01-fine-tuning/32 - GPT2 fine-tuning in WDC T4 GPU.md>)或[BERT](<01-fine-tuning/33 - BERT fine-tuning in WDC T4 GPU.md>)，再阅读[Colab 上的 Llama 2 LoRA 微调](<01-fine-tuning/21.2 - Lllama 2 Fine-tuning Demo - Colab, Fine-tuning ipynb file Go Through.md>)。

## 演示概览

| 方向 | 材料展示的内容 | 阅读入口 |
| --- | --- | --- |
| GPU 基础设施与计算机视觉 | ESXi GPU 直通、Ubuntu 驱动、tinykube、NVIDIA GPU Operator 与基于 DeepStream 的视频分析；通过 RTSP 接入实时或预录视频流。 | [GPU 视频分析](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>) |
| GPU 可观测性 | 通过 DCGM Exporter 采集指标，接入 Prometheus 并在 Grafana 展示；记录中包含 GPU 温度、功耗、频率与工作负载标签。 | [监控部署流程](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>) |
| vGPU 与图像生成 | ESXi 和虚拟机配置、vGPU 规格与许可证，再通过 AUTOMATIC1111 运行 Stable Diffusion。 | [Stable Diffusion 演示](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>) |
| 本地大模型推理 | Conda / Anaconda、text-generation-webui，以及 GPU 虚拟机中的 Llama 2 模型加载。 | [Llama 2 快速演示](<06-LLM-DEMO/12 - Llama 2 quick demo.md>) |
| 模型微调 | GPT-2 与 AG News；BERT 大小写模型与 GLUE/CoLA；Colab 上使用 SAMSum、PEFT/LoRA 和量化进行 Llama 2 7B 微调。包含训练与推理示例。 | [模型微调目录](01-fine-tuning/) |
| 私有 AI 平台 | 使用 MicroK8s / Juju，以及 Minikube / Manifests 部署 Kubeflow。 | [Kubeflow 概览](<02-kubeflow-and-private-ai/01 - kubeflow deployment 101.md>) |
| Tanzu 与共享 Notebook | TKGm 工作负载集群、节点池、GPU 直通，以及按配置选择 CPU / GPU 节点的 JupyterHub 环境，配合 NFS 存储与 MetalLB。 | [TKGm 上的 JupyterHub](<07-TKGm-GPU/TKGm GPU Cluster with JupyterHub (Jupyter Notebook).md>) |
| 配套基础设施实验 | DPU 目录中的 Redis 7.0.8 多实例测试环境与 memtier 负载生成脚本。 | [Redis 测试环境](<03-NVIDIA-DPU/redis-testbed-setup.md>) |

这些材料覆盖了相互衔接的工程工作：准备平台、部署应用、验证行为、观察资源使用情况，并记录可供再次演示的操作过程。

## 仓库内容

原始资料包括 **八个目录中的 42 个 Markdown 文件**，以及一个 Git 文本换行规范配置文件。Python 训练与推理示例、Shell 自动化脚本、Kubernetes YAML、Helm Values 和配置片段均内嵌在 Markdown 文档中。当前快照未单独收录 Python 脚本、Shell 脚本或 Jupyter Notebook 文件。

可以沿着下面的技术层次阅读：

```text
GPU 与虚拟化
  ESXi / vSphere + NVIDIA GPU 直通或 vGPU
                 |
虚拟机操作系统与 GPU 软件
  Ubuntu / Windows + 驱动 + CUDA 相关工具
                 |
应用运行环境
  Kubernetes / TKGm / Kubeflow / JupyterHub / Conda
                 |
AI 演示
  视频分析 | Stable Diffusion | Llama 2 | 模型微调

贯穿实验过程的监控
  nvidia-smi | DCGM + Prometheus + Grafana | Weights & Biases
```

这些是可分别选择、也可相互配合的实验路径；单个演示不需要部署图中的全部组件。

## 文档目录

以下链接覆盖所有原始主题文档。现有子目录 README 多为简短标题或空白占位，因此这里直接链接到具体指南，并保留原有文件名。

### 01-fine-tuning — 模型微调

- [微调经验：基础设施、运维与模型选择](<01-fine-tuning/01 - Lessons Learned during fine-tuning.md>)
- [Conda、Jupyter Notebook 与可在 CPU 上运行的 BERT 示例](<01-fine-tuning/02 - Conda and Jupyter notebook installation.md>)
- [Colab 上的 Llama 2：流程、准备工作与 SAMSum 数据集](<01-fine-tuning/21.1 - Lllama 2 Fine-tuning Demo - Colab, Introduction and Pre-config.md>)
- [Llama 2 Notebook 逐步解析：格式转换、LoRA 与微调前后推理](<01-fine-tuning/21.2 - Lllama 2 Fine-tuning Demo - Colab, Fine-tuning ipynb file Go Through.md>)
- [手动搭建 text-generation-webui 环境](<01-fine-tuning/30 - text-generation-webui manully installation.md>)
- [Weights & Biases 配置与训练图表](<01-fine-tuning/31 - wandb registration and sample charts.md>)
- [T4 上的 GPT-2 微调：AG News 数据集](<01-fine-tuning/32 - GPT2 fine-tuning in WDC T4 GPU.md>)
- [BERT 大小写模型微调：GLUE/CoLA 数据集](<01-fine-tuning/33 - BERT fine-tuning in WDC T4 GPU.md>)

### 02-kubeflow-and-private-ai — Kubeflow 与私有 AI

- [Kubeflow 部署方式概览](<02-kubeflow-and-private-ai/01 - kubeflow deployment 101.md>)
- [MicroK8s 与 Juju 实验记录](<02-kubeflow-and-private-ai/02 - microk8s kubeflow deployment.md>)
- [Minikube 与 Kubeflow Manifests 部署流程](<02-kubeflow-and-private-ai/03 - minikube kubeflow deployment.md>)

### 03-NVIDIA-DPU — DPU 相关测试环境

- [Redis 多实例测试环境与 memtier 负载脚本](<03-NVIDIA-DPU/redis-testbed-setup.md>)

### 04-NVIDIA-GPU — GPU 基础设施、视频分析与监控

- [NVIDIA 生态与 GPU 常见问题](<04-NVIDIA-GPU/00 - NVIDIA FAQ.md>)
- [Kubernetes GPU 基础：驱动、Operator 与资源分配](<04-NVIDIA-GPU/01 - NVIDIA GPU on Kubernetes 101.md>)
- [tinykube 上的 GPU 直通与视频分析](<04-NVIDIA-GPU/02 - GPU Quick Demo on tinykube.md>)
- [Shell 自动化：tinykube、Helm、Harbor 与网络配置](<04-NVIDIA-GPU/03 - tinykube configuration automation.md>)
- [DCGM、Prometheus 与 Grafana 监控](<04-NVIDIA-GPU/04 - NVIDIA monitoring in Prometheus and Grafana.md>)
- [Ubuntu GPU 驱动与 CUDA 安装记录](<04-NVIDIA-GPU/11 - NVIDIA GPU Driver and CUDA install on Ubuntu - Advanced.md>)
- [使用 VLC 作为 RTSP 监控客户端](<04-NVIDIA-GPU/21 - RTSP Client.md>)
- [RTSP 视频源与多路视频分析集成](<04-NVIDIA-GPU/22 - RTSP Source Configuratrion and Demo Integration.md>)
- [GPU 应用上线准备清单](<04-NVIDIA-GPU/90 - GPU Apps Onboarding Process.md>)

### 05-NVIDIA-vGPU — 虚拟 GPU 与生成式 AI

- [vGPU 概念、配置规格与软件组件](<05-NVIDIA-vGPU/00 - vGPU 101.md>)
- [云许可证服务 CLS 配置与虚拟机激活](<05-NVIDIA-vGPU/01 - GPU License Service installation - Cloud License Service (CLS) instance.md>)
- [ESXi vGPU 环境准备清单](<05-NVIDIA-vGPU/02 - vGPU Set up on ESXi.md>)
- [ESXi 8 vGPU 软件安装提纲](<05-NVIDIA-vGPU/03 - vGPU Software Installation on ESXi 8.md>)
- [Ubuntu 虚拟机驱动、许可证与视频分析](<05-NVIDIA-vGPU/04 - vGPU driver installation on GuestOS Ubuntu 22.04 Server LTS.md>)
- [vGPU 上的 Stable Diffusion 与 AUTOMATIC1111](<05-NVIDIA-vGPU/10 - vGPU Demo - Stable Diffusion.md>)

### 06-LLM-DEMO — LLM 部署与工具

- [LLM 工具与生态记录](<06-LLM-DEMO/00 - Open Source Tools for LLM.md>)
- [Ubuntu 与 Windows 上的 Conda / Anaconda](<06-LLM-DEMO/01 - Conda and Anaconda.md>)
- [text-generation-webui 安装配置](<06-LLM-DEMO/02 - text-generation-webui.md>)
- [ChatGPT API 简短提示——未包含实现代码](<06-LLM-DEMO/11 - ChatGPT API Demo.md>)
- [本地 Llama 2 部署与模型加载](<06-LLM-DEMO/12 - Llama 2 quick demo.md>)
- [LangChain 与 ChatGPT——尚无正文的待完善条目](<06-LLM-DEMO/13 - Langchain and Chatgpt quick demo (ongoing).md>)

### 07-TKGm-GPU — Tanzu GPU 集群与 JupyterHub

- [JupyterHub：存储、负载均衡与 CPU / GPU 环境配置](<07-TKGm-GPU/TKGm GPU Cluster with JupyterHub (Jupyter Notebook).md>)
- [TKGm 集群初始化、节点池与 GPU 直通](<07-TKGm-GPU/TKGm GPU Workload Cluster Bootstrapping Demo.md>)

### 99-videos — 演示录像

- [录像索引：部署、应用、微调与 Notebook](<99-videos/demo-list.md>)

## 演示录像

[录像索引](99-videos/demo-list.md)保留了原来的演示编号：

| 系列 | 主题 |
| --- | --- |
| Demo 1 | GPU 直通、操作系统安装、tinykube 应用部署与监控 |
| Demo 2 | vGPU 许可证、虚拟机驱动与 Stable Diffusion |
| Demo 3 | vGPU、Ubuntu、Conda / text-generation-webui 与 Llama 2 模型加载 |
| Demo 4 | 本地微调环境、训练与验证 |
| Demo 5 | Colab 微调，以及一段 Google Vertex AI 录像 |
| Demo 6 | Kubeflow 安装；索引注明该录像为无音频的原始录屏 |
| Demo 7 | 目前仅有 VCD / CSE 标题，未列出录像链接 |
| Demo 8 | GPU 集群初始化、JupyterHub 部署与用户界面 |

录像通过 Google Drive 链接提供，未保存在 Git 仓库中，访问取决于各文件的分享权限。本次 README 编写已核对录像索引，未逐个播放外部视频或测试其访问权限。

## 阅读与复现实验

可以直接在 GitHub 阅读 Markdown，也可以下载仓库：

```bash
git clone https://github.com/router-gao/ai-demos.git
cd ai-demos
```

选择一篇指南，先阅读其环境说明，再按步骤提取文档中的代码块使用。仓库没有统一安装程序，也没有一个覆盖全部演示的应用启动命令。

材料记录的环境包括 NVIDIA T4、Colab A100 40 GB、ESXi / vCenter 8.x、Ubuntu 20.04 / 22.04 和 Windows 10；部分示例还使用 tinykube Kubernetes 1.25.7、TKG 2.4 与 Kubernetes 1.27.5，以及 JupyterHub Helm Chart 3.1.0。这些版本描述的是当时的实验环境，并非当前兼容性清单或通用容量建议。

原始指南保留了当时的软件版本、命令、截图和观察结果。部分依赖未固定版本，部分图片仍指向本地路径或旧 Confluence 导出目录，一些实验安装包和镜像仓库需要另行获得访问权限。今天重新部署时，可能需要调整操作步骤。本次 README 更新不代表重新运行并验证了全部实验。

建议在可重建的实验环境中尝试配置示例：部分 Shell 代码会重置集群或修改主机网络，部分配置使用实验账号或较宽松的访问设置。使用前请替换环境相关参数。

## 内容范围与完成情况

- **GPT-2 与 BERT** 示例为便于演示而简化了训练过程。BERT 示例仅比较少量句子的预测结果，不构成通用准确率基准。
- **Llama 2 微调**指南记录了对话摘要任务的微调前后示例；其中训练耗时和显存用量仅对应当次实验。
- **DPU 目录**目前提供 Redis / memtier 测试环境配置，未包含已完成的 DPU 卸载实现或性能对比。
- **ChatGPT API** 文件是简短提示；**LangChain / ChatGPT** 文件仍为空白的待完善条目。
- **TKGm 指南**包含具体集群配置和混合节点池的手动操作流程，同时保留了尚未补全的多 GPU 节点池及混合配置标题。
- 部分指南引用上游项目或其他团队的资料，相关内容保留其原有来源归属。

## 作者与背景

由 [router-gao](https://github.com/router-gao) 维护。本仓库是我在 VMware 工作期间交付的 AI 演示项目个人档案，并收录配套实验记录与参考资料。文中的产品名称用于说明演示所采用的技术；上游软件和模型遵循各自的许可证。


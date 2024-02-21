### Financial reports

all financial reports,

https://investor.nvidia.com/financial-info/financial-reports/

fiscal 2023,

https://s201.q4cdn.com/141608511/files/doc_financials/2023/ar/2023-Annual-Report-1.pdf 

Q1 of fiscal 2024,

https://s201.q4cdn.com/141608511/files/doc_presentations/2023/06/nvda-f1q24-investor-presentation-final.pdf

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-22_9-46-34.png)

(from its FY2023 report)

### NVIDIA Expanding Accelerated Computing Ecosystem

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-22_9-49-45.png)

(from its fiscal 2024 Q1 report)

### NVIDIA Data Center Product Portfolio

https://www.nvidia.com/en-us/data-center/

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-22_10-56-6.png)

**NVIDIA Data Center GPU Dirver Document （Release Notes，User Guide， Quick Start Guide, etc）**

https://docs.nvidia.com/datacenter/tesla/index.html#nvidia-driver-documentation

The following GPUs are supported for device passthrough for virtualization

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-26_6-35-13.png)

### NVIDIA Ecosystem

### NVIDIA Edge Computing Solution

https://www.nvidia.com/en-us/edge-computing/

https://www.nvidia.com/en-us/edge-computing/5g/

### NVIDIA Document Center

https://docs.nvidia.com/

### NVIDIA Cloud Native Technologies Docs

https://docs.nvidia.com/datacenter/cloud-native/#overview

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-22_21-50-12.png)

### NVIDIA NGC and NGC Catalog

#### What is NGC

NVIDIA NGC™ is the portal of enterprise services, software, management tools, and support for end-to-end AI and digital twin workflows. Bring your solutions to market faster with fully managed services, or take advantage of performance-optimized software to build and deploy solutions on your preferred cloud, on-prem, and edge systems.

#### NGC Catalog

https://catalog.ngc.nvidia.com/

### NVIDIA Hands on labs

https://www.nvidia.com/en-us/launchpad

NVIDIA Launchpad Docs

https://docs.nvidia.com/launchpad/index.html

### Is Kubernetes important to NVIDIA GPU?

NVIDIA GPUs are widely used for accelerating various types of workloads, including machine learning, deep learning, data analytics, and high-performance computing.

Kubernetes allows you to define and manage GPU resources as part of your cluster, ensuring that applications requiring GPU acceleration can be efficiently scheduled and run on appropriate nodes that have the necessary NVIDIA GPU hardware.

Kubernetes also integrates with NVIDIA's GPU device plugin, which provides the necessary interfaces for Kubernetes to discover and utilize GPUs within the cluster. This plugin allows you to allocate GPUs to specific containers or pods, ensuring that the workload can access and utilize the GPU resources effectively.

Additionally, Kubernetes provides features such as auto-scaling, load balancing, and fault tolerance, which are beneficial for running GPU-accelerated workloads at scale. It enables you to dynamically scale the number of GPU-enabled instances based on demand, distribute the workload across multiple nodes, and ensure high availability of the applications utilizing NVIDIA GPUs.

In summary, Kubernetes plays a vital role in managing and orchestrating NVIDIA GPU resources within a cluster, enabling efficient deployment and scaling of GPU-accelerated applications.

### What is CUDA?

https://docs.nvidia.com/cuda/

https://developer.nvidia.com/cuda-toolkit

https://developer.nvidia.com/cuda-gpus

### How to try GPU and Kubernetes?

Currently I'm using ESXi 8, with Ubuntu 22.04 server OS, and tinykube 1.25 to try GPU features.

Or any desktop/laptop with a GPU, install OS (Ubuntu desktop 22.04 is user friendly), and then install GPU driver and tinykube to try GPU in Kubernetes.

### GPU on Public Cloud

There are lots of document from NVIDIA website with tag 'AWS' and 'google'.

https://developer.nvidia.com/blog/tag/aws/

https://developer.nvidia.com/blog/tag/google/

### VMware GPU Compatibility Guide

![img](./00 - NVIDIA FAQ - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-26_6-29-50.png)

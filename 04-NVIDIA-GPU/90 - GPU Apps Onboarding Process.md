The document is a check list for customer, GPU App vendor and platform vendor when we are preparing on-boarding some GPU Apps.

# Hardware resource

- VPN, jumphost information
- Internet and proxy information
- NTP, DNS, DHCP information
- number of hosts
- minimum CPU/Memory/Storage resource of each host
- Is NFS and vSAN mandatory? If yes, please provide the information.
- Is HTTP/HTTPS/FTP server mandatory? If yes, please provide the information.

# GPU Resource

- GPU model
  - Data Center GPU (A100, T4, etc)
  - or desktop GPU (RTX3000/4000, etc)
- GPU Capacity/Sizing (for example, IVS, Resolution, Algorithms, Number of Video Streams, etc)
- How many GPU cards need to be allocated for each Pod?
- Is MIG supported?

# VM resource

- Guest OS version, kernel version (Ubuntu 20.04/22.04 Server LTS is recommended)
- CPU/Memory/Storage resource of each VM
- number of port groups for each VM
- number of GPUs for each VM
- GPU driver/CUDA version

# Kubernetes platform resource

- Kubernetes version
- login information (user/password/token, etc)

# NVIDIA Software List

- GPU driver version
- CUDA version

# GPU App Information

- Pod login information (user/password/token, etc)
- service type, (NodePort, ClusterIP, Loadbalancer, etc)
- Pod management login information (http/https, user/password, etc)

# Helm or Docker Files

- The deployment is by Helm Chars or Docker?
- If it's Helm Chart, what is the Helm information (FQDN, user/password if any)
- Can the Docker file be pulled from Internet?

# Harbor Information

- Harbor version
- Harbor FQDN information
- Harbor user/password and CA

# User Document List

- App deployment Guide
- App User Guide
- App Helm Charts modification description

# Functional Test Cases

- GPU App Test Cases

# Monitoring Request

- Prometheus login in information (FQDN, user/password)

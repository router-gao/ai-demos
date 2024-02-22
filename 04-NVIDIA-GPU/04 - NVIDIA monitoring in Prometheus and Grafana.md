# Hardware

Ubuntu 22.04, NVIDIA Tesla T4 GPU, DirectPath IO to Ubuntu VM.

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_17-14-30.png)

**lspci output**

```shell
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# lspci | grep -i nvidia
03:00.0 3D controller: NVIDIA Corporation TU104GL [Tesla T4] (rev a1)
root@ubuntu-vm:/home/ubuntu#
```



# Software Versions

ESXi/vCenter 8.0.1

Ubuntu 22.04/20.04 LTS with Tinykube for fast deployment & demo

**tinykube and kubernetes version**

```shell
root@ubuntu-vm:/home/ubuntu# tinykube version
Client Version: v0.0.1
Kubernetes Version: v1.25.7+tinykube.2
Etcd Version: v3.5.6_tinykube.1
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# kubectl get node -o wide
NAME        STATUS   ROLES           AGE   VERSION              INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
ubuntu-vm   Ready    control-plane   4d    v1.25.7+tinykube.2   10.252.80.20   <none>        Ubuntu 22.04.2 LTS   5.15.0-73-generic   containerd://1.6.18
root@ubuntu-vm:/home/ubuntu#
```



The NVIDIA driver is 470, it supports higher version.

**nvidia-smi output**

```shell
root@ubuntu-vm:/home/ubuntu# nvidia-smi
Mon Jun 19 02:16:57 2023
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.182.03   Driver Version: 470.182.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:03:00.0 Off |                    0 |
| N/A   54C    P0    30W /  70W |   1215MiB / 15109MiB |     11%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
 
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1345      G   /usr/lib/xorg/Xorg                  4MiB |
|    0   N/A  N/A   3286409      C   deepstream-app                   1079MiB |
+-----------------------------------------------------------------------------+
root@ubuntu-vm:/home/ubuntu#
```



# General steps

## Pre-config, which is covered from the document here.

[02 - GPU Quick Demo on tinykube](https://confluence.eng.vmware.com/display/HTP/02+-+GPU+Quick+Demo+on+tinykube)

- install tinykube deb, as well as some other tools packages
- deploy Kubernetes from tinykube CLI (see the document of tinykube deployment here)
- install Nvidia GPU driver (see the document here. It's a few mouse clicking only)
- deploy Nvidia GPU Operator by helm chart
- deploy test Streaming analysis App by helm chart

## Deploy Prometheus and Grafana

**deploy Prometheus**

```shell
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
kubectl create ns prom
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace prom
```

Edit the service ’kube-prometheus-stack-grafana‘ service type from 'ClusterIP' to 'NodePort'

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_19-13-44.png)

Check the output and login to Grafana GUI.

**check the output**

```shell
root@ubuntu-vm:/home/ubuntu# kubectl get pod -n prom
NAME                                                        READY   STATUS    RESTARTS   AGE
alertmanager-kube-prometheus-stack-alertmanager-0           2/2     Running   0          6h1m
kube-prometheus-stack-grafana-6c848ccc84-c44wq              3/3     Running   0          6h1m
kube-prometheus-stack-kube-state-metrics-669bd5c594-2zzpt   1/1     Running   0          6h1m
kube-prometheus-stack-operator-6cc94cc988-gbvs4             1/1     Running   0          6h1m
kube-prometheus-stack-prometheus-node-exporter-vdbzn        1/1     Running   0          6h1m
prometheus-kube-prometheus-stack-prometheus-0               2/2     Running   0          6h1m
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# kubectl get svc -n prom
NAME                                             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
alertmanager-operated                            ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP   6h1m
kube-prometheus-stack-alertmanager               ClusterIP   10.106.201.175   <none>        9093/TCP                     6h1m
kube-prometheus-stack-grafana                    NodePort    10.106.243.10    <none>        80:31945/TCP                 6h1m
kube-prometheus-stack-kube-state-metrics         ClusterIP   10.104.64.250    <none>        8080/TCP                     6h1m
kube-prometheus-stack-operator                   ClusterIP   10.107.146.236   <none>        443/TCP                      6h1m
kube-prometheus-stack-prometheus                 ClusterIP   10.109.146.118   <none>        9090/TCP                     6h1m
kube-prometheus-stack-prometheus-node-exporter   ClusterIP   10.111.19.208    <none>        9100/TCP                     6h1m
prometheus-operated                              ClusterIP   None             <none>        9090/TCP                     6h1m
root@ubuntu-vm:/home/ubuntu#
```



login to Grafana GUI (**user/pwd: admin/prom-operator**) to get familiar with Prometheus/Grafana menus.

Because we modify the service type to NodePort, so

- login IP is VM IP address
- port number can be checked as below

**get port number**

```shell
root@ubuntu-vm:/home/ubuntu# kubectl get svc -n prom | grep grafana
kube-prometheus-stack-grafana                    NodePort    10.106.243.10    <none>        80:31945/TCP                 6h3m
root@ubuntu-vm:/home/ubuntu#
```



![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_17-38-1.png)

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_17-40-18.png)



## Integration of Nvidia Exporter with Prometheus

The general process of integration,

- check the Nvidia Exporter status, and modify Nvidia exporter service type from 'ClusterIP' to 'NodePort'
- get the Prometheus Helm Chart default values.yaml file
- modify the values.yaml to add Nvidia exporter information
- use command 'helm upgrade' to update the Prometheus
- modify the Grafana service from 'ClusterIP' to 'NodePort' again
- add Nvidia official template from web GUI
- validate the output

More Prometheus configuration and Nvidia Prometheus integration introduction is here.

## Check the Nvidia Exporter status.

Use CLI 'curl <cluster-ip>:<port>/metrics' to check the output. The example below shows service 'nvidia-dcgm-exporter' type=ClusterIP, ClusterIP=10.97.173.76, port=32297

**check Nvidia exporter status**

```shell
root@ubuntu-vm:/home/ubuntu# kubectl get svc -n gpu-operator
NAME                                                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
gpu-operator                                            ClusterIP   10.104.228.193   <none>        8080/TCP         9h
gpu-operator-1687144677-node-feature-discovery-master   ClusterIP   10.101.160.110   <none>        8080/TCP         9h
nvidia-dcgm-exporter                                    ClusterIP   10.97.173.76     <none>        9400:32297/TCP   9h
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# kubectl get pod -n gpu-operator
NAME                                                              READY   STATUS      RESTARTS   AGE
gpu-feature-discovery-n6jbd                                       1/1     Running     0          9h
gpu-operator-1687144677-node-feature-discovery-master-7cb62kz5q   1/1     Running     0          9h
gpu-operator-1687144677-node-feature-discovery-worker-dspfx       1/1     Running     0          9h
gpu-operator-f488d5956-l2gnk                                      1/1     Running     0          9h
nvidia-container-toolkit-daemonset-7vz46                          1/1     Running     0          9h
nvidia-cuda-validator-h6lmm                                       0/1     Completed   0          9h
nvidia-dcgm-exporter-xpn6b                                        1/1     Running     0          9h
nvidia-device-plugin-daemonset-t92cr                              1/1     Running     0          9h
nvidia-device-plugin-validator-qqdwt                              0/1     Completed   0          9h
nvidia-operator-validator-qgxxx                                   1/1     Running     0          9h
root@ubuntu-vm:/home/ubuntu#
```

**curl Nvidia exporter**

```shell
root@ubuntu-vm:/home/ubuntu# curl http://10.97.173.76:32297/metrics
...
DCGM_FI_DEV_SM_CLOCK{gpu="0",UUID="GPU-916b8073-39e4-200a-f89a-45fa79439232",device="nvidia0",modelName="Tesla T4",Hostname="nvidia-dcgm-exporter-xpn6b",DCGM_FI_DRIVER_VERSION="470.182.03",container="video-analytics-demo-1",namespace="default",pod="video-analytics-demo-0-1687144945-54d
8d5c67d-4g4b4"} 585
# HELP DCGM_FI_DEV_MEM_CLOCK Memory clock frequency (in MHz).
# TYPE DCGM_FI_DEV_MEM_CLOCK gauge
DCGM_FI_DEV_MEM_CLOCK{gpu="0",UUID="GPU-916b8073-39e4-200a-f89a-45fa79439232",device="nvidia0",modelName="Tesla T4",Hostname="nvidia-dcgm-exporter-xpn6b",DCGM_FI_DRIVER_VERSION="470.182.03",container="video-analytics-demo-1",namespace="default",pod="video-analytics-demo-0-1687144945-54
d8d5c67d-4g4b4"} 5000
# HELP DCGM_FI_DEV_GPU_TEMP GPU temperature (in C).
# TYPE DCGM_FI_DEV_GPU_TEMP gauge
DCGM_FI_DEV_GPU_TEMP{gpu="0",UUID="GPU-916b8073-39e4-200a-f89a-45fa79439232",device="nvidia0",modelName="Tesla T4",Hostname="nvidia-dcgm-exporter-xpn6b",DCGM_FI_DRIVER_VERSION="470.182.03",container="video-analytics-demo-1",namespace="default",pod="video-analytics-demo-0-1687144945-54d
8d5c67d-4g4b4"} 54
# HELP DCGM_FI_DEV_POWER_USAGE Power draw (in W).
# TYPE DCGM_FI_DEV_POWER_USAGE gauge
DCGM_FI_DEV_POWER_USAGE{gpu="0",UUID="GPU-916b8073-39e4-200a-f89a-45fa79439232",device="nvidia0",modelName="Tesla T4",Hostname="nvidia-dcgm-exporter-xpn6b",DCGM_FI_DRIVER_VERSION="470.182.03",container="video-analytics-demo-1",namespace="default",pod="video-analytics-demo-0-1687144945-
54d8d5c67d-4g4b4"} 30.099000
..
```

Edit the Nvidia exporter service type from 'ClusterIP' to 'NodePort'

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_20-42-3.png)

The expected result is as below, IP 10.252.80.20 is the Ubuntu OS mgmt IP.

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_20-43-49.png)

## Modify Prometheus user defined values.yaml file

**That's the key step of the whole process.**

Download default vaules.yaml file and save it locally with name prometheus-values.yaml.

https://raw.githubusercontent.com/prometheus-community/helm-charts/main/charts/kube-prometheus-stack/values.yaml

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_20-55-25.png)

Search for 'additionalScrapeConfigs: []' between line 3200 - 3300, and add the Nvidia Exporter information.

Below is the default values.yaml file

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_20-25-6.png)

Modify it as below, which IP and port is already validated before by command 'curl http://<IP>:<port>/metrics'

- target IP is the Ubuntu OS mgmt IP
- target port is the Nvidia exporter port

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_20-28-35.png)

## Upgrade the helm deployment by the command as below

**Upgrade Prometheus deployment**

```shell
helm upgrade kube-prometheus-stack prometheus-community/kube-prometheus-stack -n prom -f prometheus-values.yaml
```

Edit the Grafana service type from 'ClusterIP' to 'NodePort' as below

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-5-24.png)

## Check the results

**check Prometheus status**

```shell
root@ubuntu-vm:/tmp# kubectl get pod -n prom
NAME                                                        READY   STATUS    RESTARTS   AGE
alertmanager-kube-prometheus-stack-alertmanager-0           2/2     Running   0          9h
kube-prometheus-stack-grafana-6c848ccc84-c44wq              3/3     Running   0          9h
kube-prometheus-stack-kube-state-metrics-669bd5c594-2zzpt   1/1     Running   0          9h
kube-prometheus-stack-operator-6cc94cc988-gbvs4             1/1     Running   0          9h
kube-prometheus-stack-prometheus-node-exporter-vdbzn        1/1     Running   0          9h
prometheus-kube-prometheus-stack-prometheus-0               2/2     Running   0          9h
root@ubuntu-vm:/tmp#
root@ubuntu-vm:/tmp# kubectl get svc -n prom
NAME                                             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
alertmanager-operated                            ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP   9h
kube-prometheus-stack-alertmanager               ClusterIP   10.106.201.175   <none>        9093/TCP                     9h
kube-prometheus-stack-grafana                    NodePort    10.106.243.10    <none>        80:31945/TCP                 9h
kube-prometheus-stack-kube-state-metrics         ClusterIP   10.104.64.250    <none>        8080/TCP                     9h
kube-prometheus-stack-operator                   ClusterIP   10.107.146.236   <none>        443/TCP                      9h
kube-prometheus-stack-prometheus                 ClusterIP   10.109.146.118   <none>        9090/TCP                     9h
kube-prometheus-stack-prometheus-node-exporter   ClusterIP   10.111.19.208    <none>        9100/TCP                     9h
prometheus-operated                              ClusterIP   None             <none>        9090/TCP                     9h
root@ubuntu-vm:/tmp#
```

## Create Dashboard for GPU

Login to Grafana Web GUI - Dashboards

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-30-17.png)

New - 'new folder' with the name 12239-offcial (or other names)

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-32-21.png)

New - 'Import'

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-33-29.png)

Input the ID '12239'. This is Nvidia official Dashboard template ID. Select the Data Source 'Prometheus', which is the default one.

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-39-25.png)

Check the Dashboard

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-43-41.png)![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-41-22.png)

# ********** the integration is done **********

# More Operations

## Search more Nvidia related templates from Grafana website

Go to website https://grafana.com/ and search the templates.

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-47-53.png) 

To import the template into Grafana, either input 'ID' or upload the 'JSON' file. NVDIA DCGM 12239 is the official Dashboard for Prometheus/Grafana.

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-52-0.png)

## Delete Dashboard

![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-35-40.png)



![img](./04 - NVIDIA monitoring in Prometheus_Grafana - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-19_21-36-29.png)

# Remove all 3 Helm Charts (clean up script)

In case the configuration is massed up, use the script to uninstall Video Analysis App, GPU Operator, as well as Prometheus.

**remove helm charts**

```shell
#!/bin/bash
 
# Get the Helm releases
helm_list_output=$(helm list -A)
 
# Loop through each line of the output
while IFS= read -r line; do
  # Extract the release name from the line
  release_name=$(echo "$line" | awk '{print $1}')
 
  # Check if the release name contains 'gpu', 'prom', or 'video'
  if [[ $release_name == *"gpu"* || $release_name == *"prom"* || $release_name == *"video"* ]]; then
    # Uninstall the release
    helm uninstall "$release_name" -n "$(echo "$line" | awk '{print $2}')"
  fi
done <<< "$helm_list_output"
```

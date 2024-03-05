# What is JupyterHub

https://jupyter.org/hub

https://z2jh.jupyter.org/en/stable/

# Demo Videos

JupyterHub Deployment

[jupyterhub-deployment.mp4](https://drive.google.com/open?id=1hFrguhNfjSDKqQQBxKU0aEsq6qLRhOMk&usp=drive_copy)

JupyterHub UI

[jupyterhub-ui.mp4](https://drive.google.com/open?id=1txubJo1vk9PycG-c6TSoQQ7K5T0dMKNO&usp=drive_copy)

# Deploy JupyterHub on TKGm

- create TKGm cluster, and set labels for node pools
- install GPU driver and GPU Operator

Please the document [here](https://github.com/router-gao/ai-demos/blob/main/07-TKGm-GPU/TKGm%20GPU%20Workload%20Cluster%20Bootstrapping%20Demo.md)

[TKGm GPU Workload Cluster Bootstrapping Demo](https://drive.google.com/open?id=1CxVNynGMMYgz0pig0o2hrbkY0geSSYaf&usp=drive_copy)

- create storageclass

Suppose that NFS server IP is 10.252.80.106, and NFS path is /home/ubuntu/nfs

**NFS stroageclass deployment**

```shell
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
helm repo update
helm install nfs-client-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner --set nfs.server=10.252.80.106 --set nfs.path=/home/ubuntu/nfs -n nfs-client --create-namespace
```

After helm deploy NFS client, modify the NFS client storageclass to be the default storageclass. Please refer the video above for details.

**helm deploy metallb**

**metallb config**

```yaml
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: example
  namespace: metallb-system
---
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 10.242.3.40 - 10.242.3.49
```

**helm deploy metallb**

```shell
helm repo add metallb https://metallb.github.io/metallb
helm install metallb metallb/metallb  --version 0.13.7 -n metallb-system --create-namespace
kubectl apply -f l2ad-ippool.yaml
```



**helm deploy JupyterHub**

**jupyterhub-config-gpu-test.yaml**

```yaml
proxy:
  service:
    type: LoadBalancer
singleuser:
  image:
    name: jupyter/datascience-notebook
    tag: latest
  profileList:
    - display_name: "Standard Environment"
      description: "Environment without GPU support"
      kubespawner_override:
        node_selector:
          hasGPU: "false"
        extra_resource_limits: {}
    - display_name: "GPU Environment"
      description: "Environment with GPU support"
      kubespawner_override:
        node_selector:
          hasGPU: "true"
        extra_resource_limits:
          nvidia.com/gpu: "1"
    - display_name: "Standard Environment on MD-0"
      description: "Environment without GPU support on MD-0"
      kubespawner_override:
        node_selector:
          md0: "true"
        extra_resource_limits: {}
    - display_name: "Standard Environment on MD-1"
      description: "Environment without GPU support on MD-1"
      kubespawner_override:
        node_selector:
          md1: "true"
        extra_resource_limits: {}
```

**helm deployment**

```yaml
helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/
helm search repo jupyterhub --versions --max-col-width 0
helm install jupyterhub jupyterhub/jupyterhub --namespace jhub --create-namespace --version=3.1.0 --values jupyterhub-config-gpu-test.yaml
```

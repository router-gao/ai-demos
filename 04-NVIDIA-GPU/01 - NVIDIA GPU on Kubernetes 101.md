### How to consume a GPU on ESXi?

The simple answer is Pass through GPU and vGPU (MIG, Multi-Instance GPU).

https://core.vmware.com/blog/virtual-gpus-and-passthrough-gpus-vmware-vsphere-can-they-be-used-together

![image-2023-6-25_0-28-3](https://github.com/router-gao/ai-demos/assets/144886373/e718b7bd-ff80-41c1-8d03-17616c275a50)


### How to consume a GPU on Kubernetes?
https://github.com/NVIDIA/gpu-operator
https://www.youtube.com/watch?v=KER0dbfmAqQ

[How_to_easily_use_GPUs_with_Kubernetes.pdf](https://github.com/router-gao/ai-demos/files/14359723/How_to_easily_use_GPUs_with_Kubernetes.pdf)


- Hardware ready - GPU
- OS ready - ESXi and OS (currently Ubnutu is more user friendly)
- GPU driver is intalled in the OS
- Kubernetes is up and running, GPU Opertator is successfully deployed on the Kubernetes cluster
- Monitoring is configed, if it's required

![image-2023-6-25_0-33-52](https://github.com/router-gao/ai-demos/assets/144886373/8ab3536d-c8ac-4eb8-ba2d-2b0b7e17a467)



### Linux OS that can be used to consume NVIDIA GPU in Kubernetes (container toolkit)

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

![image-2023-6-24_16-39-28](https://github.com/router-gao/ai-demos/assets/144886373/f7073165-681c-4436-af23-d7ff3071773b)



### What is GPU driver?

**NVIDIA Data Center GPU Dirver Document （Release Notes，User Guide， Quick Start Guide, etc）**

https://docs.nvidia.com/datacenter/tesla/index.html#nvidia-driver-documentation

The following GPUs are supported for device passthrough for virtualization (GPU Data Center driver 525.105.17, 2023-July)

![img](./01 - NVIDIA GPU on Kubernetes 101 - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-26_6-7-26.png)

![image-2023-6-26_6-7-26](https://github.com/router-gao/ai-demos/assets/144886373/425e458f-9e6b-47d5-868f-91028aba7590)


**Most of the time, user does not need to download and install the GPU driver!**

On Ubuntu, use the command 'apt-get install' for installation. And Ubuntu has the recommended & validated driver version.

In case, manually download and installation is required, this is the website to download the driver.

https://www.nvidia.com/download/index.aspx

### How to download specific version of GPU driver?

This is the link of all GPU Linux drivers

https://download.nvidia.com/XFree86/Linux-x86_64/

### How to install GPU driver?

Simplified process for Ubuntu 22.04 server.

Tips

- **install GPU driver first**, then **install GPU Operator.** After GPU operator pods are all running, start to deploy Apps.
- after GPU driver is installed, **reboot the VM**. Without rebooting, there will be error when execute command nvidia-smi. (Failed to initialize NVML: Driver/library version mismatch)
- If GPU operator is not running, there are some App pods consume GPU, GPU operator pod will have error msg as below
- for **Ubuntu 20.04** server version, need to install **ubuntu-drivers-common** first. (apt-get install ubuntu-drivers-common)

![img](./01 - NVIDIA GPU on Kubernetes 101 - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-23_17-53-10.png)

![image-2023-6-23_17-53-10](https://github.com/router-gao/ai-demos/assets/144886373/2194ba15-40f0-4c71-a2b3-d6a10d7414ee)


![img](./01 - NVIDIA GPU on Kubernetes 101 - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-23_17-52-39.png)
![image-2023-6-23_17-52-39](https://github.com/router-gao/ai-demos/assets/144886373/66f1a913-7457-413c-8880-be556ce6538c)



Steps to install GPU driver

**apt-get update**

```shell
apt-get update -y
```



**get the recommanded driver version, line 8 with 'recommended' tag**

```shell
root@ubuntu-2204-server:/home/ubuntu#
root@ubuntu-2204-server:/home/ubuntu# ubuntu-drivers devices
== /sys/devices/pci0000:02/0000:02:03.0 ==
modalias : pci:v000010DEd00001EB8sv000010DEsd000012A2bc03sc02i00
vendor   : NVIDIA Corporation
model    : TU104GL [Tesla T4]
driver   : nvidia-driver-515-server - distro non-free
driver   : nvidia-driver-530 - distro non-free recommended
driver   : nvidia-driver-525 - distro non-free
driver   : nvidia-driver-525-server - distro non-free
driver   : nvidia-driver-515 - distro non-free
driver   : nvidia-driver-418-server - distro non-free
driver   : nvidia-driver-510 - distro non-free
driver   : nvidia-driver-470 - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
 
== /sys/devices/pci0000:00/0000:00:0f.0 ==
modalias : pci:v000015ADd00000405sv000015ADsd00000405bc03sc00i00
vendor   : VMware
model    : SVGA II Adapter
manual_install: True
driver   : open-vm-tools-desktop - distro free
 
root@ubuntu-2204-server:/home/ubuntu#
```



**install the recommanded GPU driver**

```shell
root@ubuntu-2204-server:/home/ubuntu# apt-get install nvidia-driver-530 -y
Reading package lists... Done
Building dependency tree... Done
..
Processing triggers for initramfs-tools (0.140ubuntu13.1) ...
update-initramfs: Generating /boot/initrd.img-5.15.0-73-generic
Processing triggers for libgdk-pixbuf-2.0-0:amd64 (2.42.8+dfsg-1ubuntu0.2) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
Scanning processes...
Scanning linux images...
 
Running kernel seems to be up-to-date.
 
No services need to be restarted.
 
No containers need to be restarted.
 
No user sessions are running outdated binaries.
 
No VM guests are running outdated hypervisor (qemu) binaries on this host.
root@ubuntu-2204-server:/home/ubuntu#
root@ubuntu-2204-server:/home/ubuntu# reboot
```



**reboot and try command nvidia-smi**

```shell
root@ubuntu-2204-server:/home/ubuntu# nvidia-smi
Thu Jun 22 08:24:53 2023
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 530.41.03              Driver Version: 530.41.03    CUDA Version: 12.1     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                  Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf            Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  Tesla T4                        Off| 00000000:02:03.0 Off |                    0 |
| N/A   45C    P8               11W /  70W|      2MiB / 15360MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
 
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|  No running processes found                                                           |
+---------------------------------------------------------------------------------------+
root@ubuntu-2204-server:/home/ubuntu#
```



**lsmod**

```shell
root@ubuntu-2004-server:/home/ubuntu# lsmod | grep -i nvidia
nvidia_uvm           1265664  2
nvidia_drm             65536  2
nvidia_modeset       1273856  2 nvidia_drm
nvidia              55713792  505 nvidia_uvm,nvidia_modeset
drm_kms_helper        184320  2 vmwgfx,nvidia_drm
drm                   495616  10 vmwgfx,drm_kms_helper,nvidia,nvidia_drm,ttm
root@ubuntu-2004-server:/home/ubuntu#
```



### nvidia-smi command introduction

The NVIDIA System Management Interface (nvidia-smi) is a command line utility, based on top of the [NVIDIA Management Library (NVML)](https://developer.nvidia.com/nvidia-management-library-nvml), intended to aid in the management and monitoring of NVIDIA GPU devices. 

https://developer.nvidia.com/nvidia-system-management-interface



### What is gpu-operator?

These components include the NVIDIA drivers (to enable CUDA), Kubernetes device plugin for GPUs, the NVIDIA Container Runtime, automatic node labelling, [DCGM](https://developer.nvidia.com/dcgm) based monitoring and others.

https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html

https://github.com/NVIDIA/gpu-operator

NVIDIA Webinar of gpu-operator (videos and slides)

[https://info.nvidia.com/how-to-use-gpus-on-kubernetes-webinar.html?ondemandrgt=yes#](https://info.nvidia.com/how-to-use-gpus-on-kubernetes-webinar.html?ondemandrgt=yes)


![image-2023-6-24_15-39-47](https://github.com/router-gao/ai-demos/assets/144886373/fa1d063c-4eb5-4230-8107-0817e2a60e64)


During my Demo deployment, I found some pods are very important. There are plenty of document and videos to talk about GPU operator.

Some common functions of the pods

- pods with 'validator', they are validate the related function is working correctly or not. They are very helpful on trouble shooting. For example 'kubectl logs nvidia-operator-validator-t7b69 -n gpu-operator' as below
- dcgm-exporter pod is in charge of Prometheus/Granfana monitoring of the GPU resources. The GPU Prometheus/Grafana monitoring Demo is here. [04 - NVIDIA monitoring in Prometheus/Grafana](https://github.com/router-gao/ai-demos/blob/main/04-NVIDIA-GPU/04%20-%20NVIDIA%20monitoring%20in%20Prometheus%20and%20Grafana.md)
- container-tooltik is helping deploy the toolkit automatically
- feature discovery github https://gitlab.com/nvidia/kubernetes/gpu-feature-discovery



**gpu operator pods**

```shell
root@ubuntu-2004-server:/home/ubuntu# kubectl get pod -n gpu-operator
NAME                                                              READY   STATUS      RESTARTS   AGE
gpu-feature-discovery-66q9x                                       1/1     Running     0          22h
gpu-operator-1687511833-node-feature-discovery-master-57ccznptc   1/1     Running     0          22h
gpu-operator-1687511833-node-feature-discovery-worker-xsl58       1/1     Running     0          22h
gpu-operator-cd4b97cd8-wsczj                                      1/1     Running     0          22h
nvidia-container-toolkit-daemonset-qpnrd                          1/1     Running     0          22h
nvidia-cuda-validator-6tltk                                       0/1     Completed   0          22h
nvidia-dcgm-exporter-wzvwg                                        1/1     Running     0          22h
nvidia-device-plugin-daemonset-jjt7d                              1/1     Running     0          22h
nvidia-device-plugin-validator-s524l                              0/1     Completed   0          22h
nvidia-operator-validator-t7b69                                   1/1     Running     0          22h
root@ubuntu-2004-server:/home/ubuntu#
root@ubuntu-2004-server:/home/ubuntu# kubectl logs nvidia-operator-validator-t7b69 -n gpu-operator
Defaulted container "nvidia-operator-validator" out of: nvidia-operator-validator, driver-validation (init), toolkit-validation (init), cuda-validation (init), plugin-validation (init)
all validations are successful
root@ubuntu-2004-server:/home/ubuntu#
```



### How to install gpu-operator?

Very simple and direct.

**GPU operator deployment**

```shell
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
helm repo update
kubectl create ns gpu-operator
helm install --devel nvidia/gpu-operator -n gpu-operator --wait --generate-name  --set operator.defaultRuntime=containerd
```



### How to consume GPU resource?

After GPU operator is successfully deployment, the GPU resource could be checked from each node.

In the example below, section Capacity and section Allocatable



**GPU resource on node**

```shell
root@ubuntu-2004-server:/home/ubuntu# kubectl describe node ubuntu-2004-server
Name:               ubuntu-2004-server
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    feature.node.kubernetes.io/cpu-cpuid.ADX=true
                    feature.node.kubernetes.io/cpu-cpuid.AESNI=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX2=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512BW=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512CD=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512DQ=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512F=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512VL=true
                    feature.node.kubernetes.io/cpu-cpuid.AVX512VNNI=true
                    feature.node.kubernetes.io/cpu-cpuid.CMPXCHG8=true
                    feature.node.kubernetes.io/cpu-cpuid.FLUSH_L1D=true
                    feature.node.kubernetes.io/cpu-cpuid.FMA3=true
                    feature.node.kubernetes.io/cpu-cpuid.FXSR=true
                    feature.node.kubernetes.io/cpu-cpuid.FXSROPT=true
                    feature.node.kubernetes.io/cpu-cpuid.HYPERVISOR=true
                    feature.node.kubernetes.io/cpu-cpuid.IA32_ARCH_CAP=true
                    feature.node.kubernetes.io/cpu-cpuid.IBPB=true
                    feature.node.kubernetes.io/cpu-cpuid.LAHF=true
                    feature.node.kubernetes.io/cpu-cpuid.MD_CLEAR=true
                    feature.node.kubernetes.io/cpu-cpuid.MOVBE=true
                    feature.node.kubernetes.io/cpu-cpuid.OSXSAVE=true
                    feature.node.kubernetes.io/cpu-cpuid.SPEC_CTRL_SSBD=true
                    feature.node.kubernetes.io/cpu-cpuid.STIBP=true
                    feature.node.kubernetes.io/cpu-cpuid.SYSCALL=true
                    feature.node.kubernetes.io/cpu-cpuid.SYSEE=true
                    feature.node.kubernetes.io/cpu-cpuid.X87=true
                    feature.node.kubernetes.io/cpu-cpuid.XGETBV1=true
                    feature.node.kubernetes.io/cpu-cpuid.XSAVE=true
                    feature.node.kubernetes.io/cpu-cpuid.XSAVEC=true
                    feature.node.kubernetes.io/cpu-cpuid.XSAVEOPT=true
                    feature.node.kubernetes.io/cpu-cpuid.XSAVES=true
                    feature.node.kubernetes.io/cpu-hardware_multithreading=false
                    feature.node.kubernetes.io/cpu-model.family=6
                    feature.node.kubernetes.io/cpu-model.id=85
                    feature.node.kubernetes.io/cpu-model.vendor_id=Intel
                    feature.node.kubernetes.io/kernel-config.NO_HZ=true
                    feature.node.kubernetes.io/kernel-config.NO_HZ_IDLE=true
                    feature.node.kubernetes.io/kernel-version.full=5.4.0-150-generic
                    feature.node.kubernetes.io/kernel-version.major=5
                    feature.node.kubernetes.io/kernel-version.minor=4
                    feature.node.kubernetes.io/kernel-version.revision=0
                    feature.node.kubernetes.io/pci-10de.present=true
                    feature.node.kubernetes.io/pci-15ad.present=true
                    feature.node.kubernetes.io/storage-nonrotationaldisk=true
                    feature.node.kubernetes.io/system-os_release.ID=ubuntu
                    feature.node.kubernetes.io/system-os_release.VERSION_ID=20.04
                    feature.node.kubernetes.io/system-os_release.VERSION_ID.major=20
                    feature.node.kubernetes.io/system-os_release.VERSION_ID.minor=04
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=ubuntu-2004-server
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
                    nvidia.com/cuda.driver.major=530
                    nvidia.com/cuda.driver.minor=41
                    nvidia.com/cuda.driver.rev=03
                    nvidia.com/cuda.runtime.major=12
                    nvidia.com/cuda.runtime.minor=1
                    nvidia.com/gfd.timestamp=1687511884
                    nvidia.com/gpu-driver-upgrade-state=upgrade-done
                    nvidia.com/gpu.compute.major=7
                    nvidia.com/gpu.compute.minor=5
                    nvidia.com/gpu.count=1
                    nvidia.com/gpu.deploy.container-toolkit=true
                    nvidia.com/gpu.deploy.dcgm=true
                    nvidia.com/gpu.deploy.dcgm-exporter=true
                    nvidia.com/gpu.deploy.device-plugin=true
                    nvidia.com/gpu.deploy.driver=pre-installed
                    nvidia.com/gpu.deploy.gpu-feature-discovery=true
                    nvidia.com/gpu.deploy.node-status-exporter=true
                    nvidia.com/gpu.deploy.nvsm=
                    nvidia.com/gpu.deploy.operator-validator=true
                    nvidia.com/gpu.family=turing
                    nvidia.com/gpu.memory=15360
                    nvidia.com/gpu.present=true
                    nvidia.com/gpu.product=Tesla-T4
                    nvidia.com/gpu.replicas=1
                    nvidia.com/mig.capable=false
                    nvidia.com/mig.strategy=single
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: unix:///run/containerd/containerd.sock
                    nfd.node.kubernetes.io/extended-resources:
                    nfd.node.kubernetes.io/feature-labels:
                      cpu-cpuid.ADX,cpu-cpuid.AESNI,cpu-cpuid.AVX,cpu-cpuid.AVX2,cpu-cpuid.AVX512BW,cpu-cpuid.AVX512CD,cpu-cpuid.AVX512DQ,cpu-cpuid.AVX512F,cpu-...
                    nfd.node.kubernetes.io/master.version: v0.12.1
                    nfd.node.kubernetes.io/worker.version: v0.12.1
                    node.alpha.kubernetes.io/ttl: 0
                    nvidia.com/gpu-driver-upgrade-enabled: true
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Fri, 23 Jun 2023 06:57:16 +0000
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  ubuntu-2004-server
  AcquireTime:     <unset>
  RenewTime:       Sat, 24 Jun 2023 07:26:10 +0000
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Sat, 24 Jun 2023 07:24:54 +0000   Fri, 23 Jun 2023 06:57:13 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Sat, 24 Jun 2023 07:24:54 +0000   Fri, 23 Jun 2023 06:57:13 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Sat, 24 Jun 2023 07:24:54 +0000   Fri, 23 Jun 2023 06:57:13 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Sat, 24 Jun 2023 07:24:54 +0000   Fri, 23 Jun 2023 06:58:09 +0000   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:  10.0.72.102
  Hostname:    ubuntu-2004-server
Capacity:
  cpu:                10
  ephemeral-storage:  102626232Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16391500Ki
  nvidia.com/gpu:     1
  pods:               110
Allocatable:
  cpu:                10
  ephemeral-storage:  94580335255
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16289100Ki
  nvidia.com/gpu:     1
  pods:               110
System Info:
  Machine ID:                 1bc84b742a024f8f81eb08a17f84ed68
  System UUID:                857f3342-2cd9-06bd-8ab2-b642156d38ba
  Boot ID:                    e10e2090-b46a-4942-b97c-a22c40a87b37
  Kernel Version:             5.4.0-150-generic
  OS Image:                   Ubuntu 20.04.6 LTS
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  containerd://1.6.18
  Kubelet Version:            v1.25.7+tinykube.2
  Kube-Proxy Version:         v1.25.7+tinykube.2
PodCIDR:                      192.168.0.0/24
PodCIDRs:                     192.168.0.0/24
Non-terminated Pods:          (20 in total)
  Namespace                   Name                                                               CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                   ----                                                               ------------  ----------  ---------------  -------------  ---
  default                     ubuntu-pod                                                         0 (0%)        0 (0%)      0 (0%)           0 (0%)         24h
  default                     video-analytics-demo-0-1687512006-5b4bc84c4d-vzprt                 0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  default                     video-analytics-demo-0-1687512006-webui-855d45d68f-gqz7x           0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                gpu-feature-discovery-66q9x                                        0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                gpu-operator-1687511833-node-feature-discovery-master-57ccznptc    0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                gpu-operator-1687511833-node-feature-discovery-worker-xsl58        0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                gpu-operator-cd4b97cd8-wsczj                                       200m (2%)     500m (5%)   100Mi (0%)       350Mi (2%)     22h
  gpu-operator                nvidia-container-toolkit-daemonset-qpnrd                           0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                nvidia-dcgm-exporter-wzvwg                                         0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                nvidia-device-plugin-daemonset-jjt7d                               0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  gpu-operator                nvidia-operator-validator-t7b69                                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         22h
  kube-system                 antrea-agent-d7vd5                                                 400m (4%)     0 (0%)      0 (0%)           0 (0%)         24h
  kube-system                 antrea-controller-7df55b7dcb-wjmt6                                 200m (2%)     0 (0%)      0 (0%)           0 (0%)         24h
  kube-system                 coredns-565d847f94-6mbb9                                           100m (1%)     0 (0%)      70Mi (0%)        170Mi (1%)     24h
  kube-system                 coredns-565d847f94-wlrx6                                           100m (1%)     0 (0%)      70Mi (0%)        170Mi (1%)     24h
  kube-system                 etcd-ubuntu-2004-server                                            100m (1%)     0 (0%)      100Mi (0%)       0 (0%)         24h
  kube-system                 kube-apiserver-ubuntu-2004-server                                  250m (2%)     0 (0%)      0 (0%)           0 (0%)         24h
  kube-system                 kube-controller-manager-ubuntu-2004-server                         200m (2%)     0 (0%)      0 (0%)           0 (0%)         24h
  kube-system                 kube-proxy-flmwh                                                   0 (0%)        0 (0%)      0 (0%)           0 (0%)         24h
  kube-system                 kube-scheduler-ubuntu-2004-server                                  100m (1%)     0 (0%)      0 (0%)           0 (0%)         24h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests     Limits
  --------           --------     ------
  cpu                1650m (16%)  500m (5%)
  memory             340Mi (2%)   690Mi (4%)
  ephemeral-storage  0 (0%)       0 (0%)
  hugepages-1Gi      0 (0%)       0 (0%)
  hugepages-2Mi      0 (0%)       0 (0%)
  nvidia.com/gpu     1            1
Events:              <none>
root@ubuntu-2004-server:/home/ubuntu#
```



In the pod definition, 'resource' and 'request' definition are similar to SR-IOV pNIC definition.

**GPU resource**

```shell
root@ubuntu-2004-server:/home/ubuntu# kubectl get pod
NAME                                                       READY   STATUS    RESTARTS      AGE
ubuntu-pod                                                 1/1     Running   1 (24h ago)   24h
video-analytics-demo-0-1687512006-5b4bc84c4d-vzprt         1/1     Running   0             22h
video-analytics-demo-0-1687512006-webui-855d45d68f-gqz7x   2/2     Running   0             22h
root@ubuntu-2004-server:/home/ubuntu#
root@ubuntu-2004-server:/home/ubuntu# kubectl get pod video-analytics-demo-0-1687512006-5b4bc84c4d-vzprt -o yaml | grep gpu
        nvidia.com/gpu: "1"
        nvidia.com/gpu: "1"
root@ubuntu-2004-server:/home/ubuntu#
root@ubuntu-2004-server:/home/ubuntu#
root@ubuntu-2004-server:/home/ubuntu# kubectl get pod video-analytics-demo-0-1687512006-5b4bc84c4d-vzprt -o yaml | grep gpu -C 10
    name: video-analytics-demo-1
    ports:
    - containerPort: 8554
      name: http
      protocol: TCP
    - containerPort: 5080
      name: http1
      protocol: TCP
    resources:
      limits:
        nvidia.com/gpu: "1"
      requests:
        nvidia.com/gpu: "1"
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /etc/config
      name: ipmount
    - mountPath: /opt/nvidia/deepstream/create_config_a100.py
      name: create-config-a100
      subPath: create_config_a100.py
    - mountPath: /opt/nvidia/deepstream/create_config.py
      name: create-config
root@ubuntu-2004-server:/home/ubuntu#
```



### Container toolkit

The NVIDIA Container Toolkit allows users to build and run GPU accelerated containers. The toolkit includes a container runtime library and utilities to automatically configure containers to leverage NVIDIA GPUs.

https://github.com/NVIDIA/nvidia-container-toolkit

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/overview.html

![image-2023-6-24_16-35-34](https://github.com/router-gao/ai-demos/assets/144886373/d21fc8e6-2c4c-48bf-af57-f50a3cfb52d0)



### How to monitor NVIDIA GPU?

**NVIDIA Data Center GPU Manager (DCGM)** is a suite of tools for managing and monitoring NVIDIA datacenter GPUs in cluster environments. It includes active health monitoring, comprehensive diagnostics, system alerts and governance policies including power and clock management. It can be used standalone by infrastructure teams and easily integrates into cluster management tools, resource scheduling and monitoring products from NVIDIA partners.

It's included in the Kubernetes GPU Operator and it's deployed automatically. Without Kubernetes GPU Operator, users have to install it manually, for example in a Docker standalone environment.

The GPU Prometheus/Grafana monitoring Demo is here. [04 - NVIDIA monitoring in Prometheus/Grafana](https://github.com/router-gao/ai-demos/blob/main/04-NVIDIA-GPU/04%20-%20NVIDIA%20monitoring%20in%20Prometheus%20and%20Grafana.md)



![image-2023-6-24_16-6-28](https://github.com/router-gao/ai-demos/assets/144886373/056508b0-29f6-4340-af4f-c63ec4ba24e8)



This is the official document of NVIDIA DCGM

https://developer.nvidia.com/dcgm

https://docs.nvidia.com/datacenter/cloud-native/gpu-telemetry/latest/index.html

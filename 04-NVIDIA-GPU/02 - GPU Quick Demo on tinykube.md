To make the process as simple as possible, there are some optimizations.

- Use Ubuntu desktop version instead of Ubuntu server server. On Ubuntu desktop version, Nvidia driver can be installed from GUI by mouse clicking.
- Use 'dpkg' command to install tinykube. After converting the tinykube rpm package into deb, tinykube could be install through 1 command dpkg -i *.deb
- Use 'apt-get install' command to install golang.
- Use tinykube to deploy GPU Operator, and it save the process of plugin deployment and containerd configuration.
- Deploy a Nvidia Demo Helm Chart for better understanding of GPU.  

# 1 - Hardware & Software Requirement

- Any desktop/laptop/Server with Nvidia GPU 

- Ubuntu 22.04 Desktop version ISO

- tinykube 1.25 rpm package

  That's the link for tinykube rpm v1.25.7 (the latest one in June, 2023)

  https://gitlab.eng.vmware.com/core-build/tinykube-rpm/-/blob/main/RPMS/x86_64/tinykube-v1.25.7+tinykube.2-3.x86_64.rpm

  All tinykube RPMs could be found here.

  https://gitlab.eng.vmware.com/core-build/tinykube-rpm/-/tree/main/RPMS/x86_64

- Internet Connection

- VNC client (optional)

# 2 - Steps

- install Ubuntu 22.04 desktop
- install GPU passthrough (if it's ESXi VM based Ubuntu)
- install Nvidia driver
- install tinykube
- install Helm Chart
- install Nvidia GPU Operator
- install Nvidia demo

## install Ubuntu 22.04 desktop

In case you need VNC login, you can follow the steps below

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-55-26.png) ![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-56-8.png)

## install GPU passthrough (if it's ESXi VM based Ubuntu)

Add PCI Passthrough device

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-11-7.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_17-14-21.png)

## install Nvidia driver

Select Software & Updates - Additional Drivers - Select proper drivers. Most of the time, the first one with 'tested' label is preferred. 

Click 'Apply Changes', and system rebooting is required after driver is successfully installed.

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-17-50.png) ![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-19-24.png) 



After rebooting, check the status by command 'nvidia-smi', and Nvidia App will be installed automatically.

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_20-16-31.png)![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-53-28.png) ![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-54-10.png)

## install tinykube

Upload tinykube rpm into /root directory, and install tinykube by follow the commands below. 

**go to /root directory**

```shell
sudo su
cd /root
```



**install necessary packages**

```shell
apt-get update -y
apt-get install -y net-tools vim curl wget openssh-server
apt-get install -y zstd conntrack ethtool socat make build-essential libseccomp-dev pkg-config jq apparmor unzip btrfs-progs libbtrfs-dev
```



**swapoff**

```shell
sudo swapoff -a
sudo rm /swap.img
```



**install go and alien**

```shell
apt-get install -y golang alien
go version
alien --version
```



**convert rpm into deb and install tinykube**

```shell
alien -d tinykube-v1.25.7+tinykube.2-3.x86_64.rpm
dpkg -i tinykube_0v1.25.7+tinykube.2-4_amd64.deb
tinykube version
```



**install Kubernetes cluster (SNC)**

```shell
tinykube start --skip-phases=default-cni
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```



**deploy Antrea as the CNI**

```shell
cd /root
wget https://github.com/antrea-io/antrea/releases/download/v1.2.3/antrea.yml
sed -i 's/projects.registry.vmware.com\/antrea\/antrea-ubuntu\:v1.2.3/projects-stg.registry.vmware.com\/tkg\/antrea-advanced-debian\:v1.2.3_vmware.4/g' antrea.yml
kubectl apply -f antrea.yml
```



**dummy pod yaml**

```shell
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-pod
spec:
  containers:
    - name: ubuntu-container
      image: ubuntu:22.04
      command: ["/bin/bash", "-c"]
      args:
        - |
          apt-get update -y &&
          apt-get install -y net-tools vim iputils-ping &&
          echo done > /tmp/log.txt &&
          sleep infinity
```

## install Helm Chart

**install Helm**

```shell
cd /root
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
helm versioncd /root``curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3``chmod 700 get_helm.sh``./get_helm.sh``helm version
```

## install Nvidia GPU Operator

**install Nvidia demo**

```shell
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
helm repo update
kubectl create ns gpu-operator
helm install --devel nvidia/gpu-operator -n gpu-operator --wait --generate-name  --set operator.defaultRuntime=containerd
```



## Install GPU demo

**deploy Stream Analytics demo**

```shell
helm fetch https://helm.ngc.nvidia.com/nvidia/charts/video-analytics-demo-0.1.8.tgz && helm install video-analytics-demo-0.1.8.tgz --generate-name
kubectl get pod -A
```



**Get login info**

```shell
export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services video-analytics-demo-0-1686148424)
export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
echo rtsp://$NODE_IP:$NODE_PORT/ds-test
export ANT_NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services video-analytics-demo-0-1686148424-webui)
export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
echo http://$NODE_IP:$ANT_NODE_PORT
```



## CLI to check the setup

**Check Kubernetes status**

```shell
root@ubuntu-vm:~# kubectl get pod -A
NAMESPACE      NAME                                                              READY   STATUS      RESTARTS   AGE
default        video-analytics-demo-0-1686148424-5bb9c44455-8g86s                1/1     Running     0          12h
default        video-analytics-demo-0-1686148424-webui-849c9c96b7-kkcv4          2/2     Running     0          12h
gpu-operator   gpu-feature-discovery-68s5s                                       1/1     Running     0          12h
gpu-operator   gpu-operator-1686148090-node-feature-discovery-master-66fcnhpk7   1/1     Running     0          12h
gpu-operator   gpu-operator-1686148090-node-feature-discovery-worker-q28bv       1/1     Running     0          12h
gpu-operator   gpu-operator-959f74d9d-rmdhw                                      1/1     Running     0          12h
gpu-operator   nvidia-container-toolkit-daemonset-7bn49                          1/1     Running     0          12h
gpu-operator   nvidia-cuda-validator-ppw2h                                       0/1     Completed   0          12h
gpu-operator   nvidia-dcgm-exporter-lk4nh                                        1/1     Running     0          12h
gpu-operator   nvidia-device-plugin-daemonset-x2rgp                              1/1     Running     0          12h
gpu-operator   nvidia-device-plugin-validator-z6pnz                              0/1     Completed   0          12h
gpu-operator   nvidia-operator-validator-zthdf                                   1/1     Running     0          12h
kube-system    antrea-agent-gnnrv                                                2/2     Running     0          12h
kube-system    antrea-controller-7df55b7dcb-fw88m                                1/1     Running     0          12h
kube-system    coredns-565d847f94-6zbmj                                          1/1     Running     0          12h
kube-system    coredns-565d847f94-q8tx6                                          1/1     Running     0          12h
kube-system    etcd-ubuntu-vm                                                    1/1     Running     0          12h
kube-system    kube-apiserver-ubuntu-vm                                          1/1     Running     0          12h
kube-system    kube-controller-manager-ubuntu-vm                                 1/1     Running     0          12h
kube-system    kube-proxy-qd4js                                                  1/1     Running     0          12h
kube-system    kube-scheduler-ubuntu-vm                                          1/1     Running     0          12h
root@ubuntu-vm:~#
```

# Open web bowser

It can analyze car, person, bicycle, and card model/brand/color.

# ![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-57-23.png)

# Trouble shooting

## ESXi VM Ubuntu 22.04 can not bootstrap after adding GPU passthrough

Sometimes, if deploy Ubuntu 22.04 desktop with PCI passthrough directly on ESXi, it can not boot up.

The workaround is to deploy 20.04 desktop (and upgrade to 22.04). If Ubuntu 20.04 desktop is good enough, no need to upgrade it to 22.04.

To upgrade from Ubuntu 20.04 to 22.04, steps are as below.

Select the grey/white color ICON 'Software Updater' (not Software & Updates), and it will do the upgrade job automatically.

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-9_9-59-11.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-9_10-1-44.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-9_10-2-6.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-9_10-2-49.png)



## vmtools does not run

If the vmtools status is 'installed, but not running', just install both open-vm-tools-desktop and open-vm-tools. Rebooting might be required.

**install vmtools**

```shell
sudo su
apt-get install -y open-vm-tools-desktop open-vm-tools
```

## Check Kubernetes status

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_11-7-8.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_11-7-30.png)

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_11-9-34.png)

## Check GPU status

![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_11-7-53.png)



![img](./02 - GPU Quick Demo on tinykube - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_11-8-26.png)

NVIDIA GPU driver install and uninstall is the first step to handle GPU. There are a few ways to do that.

# Know Before You Go

## GPU drivers version and CUDA version

When we talk about 'GPU driver version', it usually means GPU Linux driver. GPU Linux driver is slightly different from GPU Windows driver.

- GPU driver contains CUDA packages. Install GPU driver will in CUDA driver automatically. But some CUDA tools will be installed.
- CUDA driver has GPU driver as well. It will ask user if they prefer to install GPU driver. CUDA driver will install lots of CUDA tools as well.

Conclusion,

- for quick Demo set up, direct GPU driver installation is preferred.
- In development environment, CUDA installation is better.  

## How to download/install specific driver version

https://download.nvidia.com/XFree86/Linux-x86_64/

https://developer.nvidia.com/cuda-toolkit-archive

## How to check the relations between GPU driver and CUDA driver

For example CUDA 11.7.1, from its release notes.

https://docs.nvidia.com/cuda/archive/11.7.1/cuda-toolkit-release-notes/index.html

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_15-26-45.png)

![image-2023-6-27_15-26-45](https://github.com/router-gao/ai-demos/assets/144886373/6cbc1d72-3c50-4a2d-9129-36b158714107)


# Check the GPU driver version and CUDA version after installation

Use command 'nvidia-smi'

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_15-54-15.png)

![image-2023-6-27_15-54-15](https://github.com/router-gao/ai-demos/assets/144886373/c8a17399-f8e3-4b15-b785-d56baa73cd2a)


# Installation Process

Install gcc and make first.

**install gcc and make**

```shell
apt-get install gcc make -y
```



## Option - 1, install GPU driver from Ubuntu GUI

It's simple and direct on Ubuntu desktop OS.

Select Software & Updates - Additional Drivers - Select proper drivers. Most of the time, the first one with 'tested' label is preferred. 

Click 'Apply Changes', and system rebooting is required after driver is successfully installed.

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-17-50.png) 
![image-2023-6-8_10-17-50](https://github.com/router-gao/ai-demos/assets/144886373/0726eb48-df65-4253-aa71-2fbc83fed2e8)


![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-19-24.png) 

![image-2023-6-8_10-19-24](https://github.com/router-gao/ai-demos/assets/144886373/20cc44b8-a4b2-4671-8ffe-8566fb45cd0e)


After rebooting, check the status by command 'nvidia-smi', and Nvidia App will be installed automatically.

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_20-16-31.png)

![image-2023-6-6_20-16-31](https://github.com/router-gao/ai-demos/assets/144886373/a2c8f065-5bfa-4bc6-a5c5-8fd2f31167c9)


![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-53-28.png) 

![image-2023-6-6_17-53-28](https://github.com/router-gao/ai-demos/assets/144886373/cc8c0e7d-c72f-411f-b5f2-b477e5d64af1)


![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-54-10.png)

![image-2023-6-6_17-54-10](https://github.com/router-gao/ai-demos/assets/144886373/dd795b3d-f687-4ea8-94d0-be0e8b07566c)


## Option - 2, install GPU driver from Ubuntu CLI

If's Ubuntu server OS, CLI install a direct way.

Steps to install GPU driver

**apt-get update**

```shell
apt-get update -y
```

**get the recommanded driver version, line 8 with 'recommended' tag**

```
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



## Option - 3, install CUDA and it will install GPU driver by selection

**Before doing any CUDA related configuration on Ubuntu Desktop OS, use CLI 'init 3' to exit graphic GUI, and use CLI 'init 5' to get GUI back.**

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_18-32-29.png)

![image-2023-7-12_18-32-29](https://github.com/router-gao/ai-demos/assets/144886373/8474d2bb-e7ac-4d10-b36b-2770b7bd1dde)


![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_18-32-55.png)

![image-2023-7-12_18-32-55](https://github.com/router-gao/ai-demos/assets/144886373/78271983-7fce-49e1-83fd-b86080c0f200)



The CUDA tool kit document includes installation guide. There are 2 steps.

Step 1, blacklist nouveau and **reboot** the VM

**balcklist nouveau**

```shell
echo '' > /etc/modprobe.d/nvidia-installer-disable-nouveau.conf
cat >> /etc/modprobe.d/nvidia-installer-disable-nouveau.conf <<-EOF
blacklist nouveau
options nouveau modeset=0
EOF
 
echo '' > /etc/modprobe.d/nvidia.conf
cat >> /etc/modprobe.d/nvidia.conf <<-EOF
options nvidia NVreg_OpenRmEnableUnsupportedGpus=1
EOF
 
update-initramfs -u
```



Step 2, download and run the installer sudo sh cuda_<version>_linux.run, example of cuda_11.7.1 is as below.

https://developer.nvidia.com/cuda-downloads

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-18-28.png)
![image-2023-6-27_16-18-28](https://github.com/router-gao/ai-demos/assets/144886373/7d6962c4-9189-4ad0-8616-b5a0b7310ca2)



**run the CUDA installer**

```shell
wget https://developer.download.nvidia.com/compute/cuda/12.1.1/local_installers/cuda_12.1.1_530.30.02_linux.run
sudo sh cuda_12.1.1_530.30.02_linux.run -m=kernel-open
```

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-27-8.png) 
![image-2023-6-27_16-27-8](https://github.com/router-gao/ai-demos/assets/144886373/ce439664-0562-494c-8b30-d3d0ba1c929a)



![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-27-45.png)
![image-2023-6-27_16-27-45](https://github.com/router-gao/ai-demos/assets/144886373/7d9505ac-7ac7-43d2-ac6a-caf4d1af88bf)



monitor the logs

**monitor the logs**

```shell
root@ubuntu-vm:/home/ubuntu# cd /var/log
root@ubuntu-vm:/var/log#
root@ubuntu-vm:/var/log# ll | grep cuda
-rw-r--r--   1 root      root                570 Jun 27 08:27 cuda-installer.log
-rw-r--r--   1 root      root            1006657 Jun 26 03:16 cuda-uninstaller.log
root@ubuntu-vm:/var/log#
root@ubuntu-vm:/var/log# tail -f cuda-installer.log
[INFO]: Installing: CUDA Command Line Tools 12.1
[INFO]: Installing: cuda-cupti
[INFO]: Installing: cuda-gdb
[INFO]: Installing: nvdisasm
[INFO]: Installing: nvprof
[INFO]: Installing: nvtx
[INFO]: Installing: compute-sanitizer
...
 
root@ubuntu-vm:/var/log# ll | grep -i cuda
-rw-r--r--   1 root      root                287 Jun 27 08:25 cuda-installer.log
-rw-r--r--   1 root      root            1006657 Jun 26 03:16 cuda-uninstaller.log
root@ubuntu-vm:/var/log#
root@ubuntu-vm:/var/log#
root@ubuntu-vm:/var/log# tail -f cuda-installer.log
[INFO]: Installing: cuda-cuobjdump
[INFO]: Installing: cuda-cuxxfilt
[INFO]: Installing: cuda-nvcc
[INFO]: Installing: cuda-nvprune
[INFO]: Installing: libnvvm-samples
...
```

# Uninstall

If the GPU driver is installed directly (not from cuda), I can not find a 'perfect' and 'clean' uninstall by following such CLIs like 'apt --purge remove ..'

Below are a few ways tested and is working good all the time.

## Restore snapshot

No need for explanation.

## nvidia-uninstall command, if the driver is install from cuda

**nvidia-uninstall**

```shell
nvidia-uninstall
```

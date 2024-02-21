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

# Check the GPU driver version and CUDA version after installation

Use command 'nvidia-smi'

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_15-54-15.png)

# Installation Process

Install gcc and make first.

**install gcc and make**

```
apt-get install gcc make -y
```

## Option - 1, install GPU driver from Ubuntu GUI

It's simple and direct on Ubuntu desktop OS.

Select Software & Updates - Additional Drivers - Select proper drivers. Most of the time, the first one with 'tested' label is preferred. 

Click 'Apply Changes', and system rebooting is required after driver is successfully installed.

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-17-50.png) ![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-8_10-19-24.png) 



After rebooting, check the status by command 'nvidia-smi', and Nvidia App will be installed automatically.

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_20-16-31.png)![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-53-28.png) ![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-6_17-54-10.png)

## Option - 2, install GPU driver from Ubuntu CLI

If's Ubuntu server OS, CLI install a direct way.

Steps to install GPU driver

**apt-get update**

```
apt-get update -y
```

**get the recommanded driver version, line 8 with 'recommended' tag**

```
root``@ubuntu``-``2204``-server:/home/ubuntu#``root``@ubuntu``-``2204``-server:/home/ubuntu# ubuntu-drivers devices``== /sys/devices/pci0000:``02``/``0000``:``02``:``03.0` `==``modalias : pci:v000010DEd00001EB8sv000010DEsd000012A2bc03sc02i00``vendor  : NVIDIA Corporation``model  : TU104GL [Tesla T4]``driver  : nvidia-driver-``515``-server - distro non-free``driver  : nvidia-driver-``530` `- distro non-free recommended``driver  : nvidia-driver-``525` `- distro non-free``driver  : nvidia-driver-``525``-server - distro non-free``driver  : nvidia-driver-``515` `- distro non-free``driver  : nvidia-driver-``418``-server - distro non-free``driver  : nvidia-driver-``510` `- distro non-free``driver  : nvidia-driver-``470` `- distro non-free``driver  : nvidia-driver-``450``-server - distro non-free``driver  : nvidia-driver-``470``-server - distro non-free``driver  : xserver-xorg-video-nouveau - distro free builtin` `== /sys/devices/pci0000:``00``/``0000``:``00``:0f.``0` `==``modalias : pci:v000015ADd00000405sv000015ADsd00000405bc03sc00i00``vendor  : VMware``model  : SVGA II Adapter``manual_install: True``driver  : open-vm-tools-desktop - distro free` `root``@ubuntu``-``2204``-server:/home/ubuntu#
```

**install the recommanded GPU driver**

```
root``@ubuntu``-``2204``-server:/home/ubuntu# apt-get install nvidia-driver-``530` `-y``Reading ``package` `lists... Done``Building dependency tree... Done``..``Processing triggers ``for` `initramfs-tools (``0``.140ubuntu13.``1``) ...``update-initramfs: Generating /boot/initrd.img-``5.15``.``0``-``73``-generic``Processing triggers ``for` `libgdk-pixbuf-``2.0``-``0``:amd64 (``2.42``.``8``+dfsg-1ubuntu0.``2``) ...``Processing triggers ``for` `libc-bin (``2.35``-0ubuntu3.``1``) ...``Scanning processes...``Scanning linux images...` `Running kernel seems to be up-to-date.` `No services need to be restarted.` `No containers need to be restarted.` `No user sessions are running outdated binaries.` `No VM guests are running outdated hypervisor (qemu) binaries on ``this` `host.``root``@ubuntu``-``2204``-server:/home/ubuntu#``root``@ubuntu``-``2204``-server:/home/ubuntu# reboot
```

**reboot and try command nvidia-smi**

```
root``@ubuntu``-``2204``-server:/home/ubuntu# nvidia-smi``Thu Jun ``22` `08``:``24``:``53` `2023``+---------------------------------------------------------------------------------------+``| NVIDIA-SMI ``530.41``.``03`       `Driver Version: ``530.41``.``03`  `CUDA Version: ``12.1`   `|``|-----------------------------------------+----------------------+----------------------+``| GPU Name         Persistence-M| Bus-Id    Disp.A | Volatile Uncorr. ECC |``| Fan Temp Perf      Pwr:Usage/Cap|     Memory-Usage | GPU-Util Compute M. |``|                     |           |        MIG M. |``|=========================================+======================+======================|``|  ``0` `Tesla T4            Off| ``00000000``:``02``:``03.0` `Off |          ``0` `|``| N/A  45C  P8        11W / 70W|   2MiB / 15360MiB |   ``0``%   Default |``|                     |           |         N/A |``+-----------------------------------------+----------------------+----------------------+` `+---------------------------------------------------------------------------------------+``| Processes:                                      |``| GPU  GI  CI    PID  Type  Process name              GPU Memory |``|    ID  ID                               Usage   |``|=======================================================================================|``| No running processes found                              |``+---------------------------------------------------------------------------------------+``root``@ubuntu``-``2204``-server:/home/ubuntu#
```

**lsmod**

```
root``@ubuntu``-``2004``-server:/home/ubuntu# lsmod | grep -i nvidia``nvidia_uvm      ``1265664` `2``nvidia_drm       ``65536` `2``nvidia_modeset    ``1273856` `2` `nvidia_drm``nvidia       ``55713792` `505` `nvidia_uvm,nvidia_modeset``drm_kms_helper    ``184320` `2` `vmwgfx,nvidia_drm``drm          ``495616` `10` `vmwgfx,drm_kms_helper,nvidia,nvidia_drm,ttm``root``@ubuntu``-``2004``-server:/home/ubuntu#
```

## Option - 3, install CUDA and it will install GPU driver by selection

**Before doing any CUDA related configuration on Ubuntu Desktop OS, use CLI 'init 3' to exit graphic GUI, and use CLI 'init 5' to get GUI back.**

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_18-32-29.png)

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_18-32-55.png)

The CUDA tool kit document includes installation guide. There are 2 steps.

Step 1, blacklist nouveau and **reboot** the VM

**balcklist nouveau**

```
echo ``''` `> /etc/modprobe.d/nvidia-installer-disable-nouveau.conf``cat >> /etc/modprobe.d/nvidia-installer-disable-nouveau.conf <<-EOF``blacklist nouveau``options nouveau modeset=``0``EOF` `echo ``''` `> /etc/modprobe.d/nvidia.conf``cat >> /etc/modprobe.d/nvidia.conf <<-EOF``options nvidia NVreg_OpenRmEnableUnsupportedGpus=``1``EOF` `update-initramfs -u
```



Step 2, download and run the installer sudo sh cuda_<version>_linux.run, example of cuda_11.7.1 is as below.

https://developer.nvidia.com/cuda-downloads

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-18-28.png)

**run the cuda installer**

```
wget https:``//developer.download.nvidia.com/compute/cuda/12.1.1/local_installers/cuda_12.1.1_530.30.02_linux.run``sudo sh cuda_12.``1``.1_530.``30``.02_linux.run -m=kernel-open
```

![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-27-8.png) ![img](./11 - NVIDIA GPU Driver and CUDA install on Ubuntu (Advanced) - HoTT Team - Public - VMware Core Confluence_files/image-2023-6-27_16-27-45.png)

monitor the logs

**monitor the logs**

```
root``@ubuntu``-vm:/home/ubuntu# cd /var/log``root``@ubuntu``-vm:/var/log#``root``@ubuntu``-vm:/var/log# ll | grep cuda``-rw-r--r--  ``1` `root   root        ``570` `Jun ``27` `08``:``27` `cuda-installer.log``-rw-r--r--  ``1` `root   root      ``1006657` `Jun ``26` `03``:``16` `cuda-uninstaller.log``root``@ubuntu``-vm:/var/log#``root``@ubuntu``-vm:/var/log# tail -f cuda-installer.log``[INFO]: Installing: CUDA Command Line Tools ``12.1``[INFO]: Installing: cuda-cupti``[INFO]: Installing: cuda-gdb``[INFO]: Installing: nvdisasm``[INFO]: Installing: nvprof``[INFO]: Installing: nvtx``[INFO]: Installing: compute-sanitizer``...` `root``@ubuntu``-vm:/var/log# ll | grep -i cuda``-rw-r--r--  ``1` `root   root        ``287` `Jun ``27` `08``:``25` `cuda-installer.log``-rw-r--r--  ``1` `root   root      ``1006657` `Jun ``26` `03``:``16` `cuda-uninstaller.log``root``@ubuntu``-vm:/var/log#``root``@ubuntu``-vm:/var/log#``root``@ubuntu``-vm:/var/log# tail -f cuda-installer.log``[INFO]: Installing: cuda-cuobjdump``[INFO]: Installing: cuda-cuxxfilt``[INFO]: Installing: cuda-nvcc``[INFO]: Installing: cuda-nvprune``[INFO]: Installing: libnvvm-samples``...
```

# Uninstall

If the GPU driver is installed directly (not from cuda), I can not find a 'perfect' and 'clean' uninstall by following such CLIs like 'apt --purge remove ..'

Below are a few ways tested and is working good all the time.

## Restore snapshot

No need for explanation.

## nvidia-uninstall command, if the driver is install from cuda

**nvidia-uninstall**

```
nvidia-uninstall
```

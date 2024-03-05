## vGPU installation

the driver could be download from NVIDIA license server https://nvia.nvidia.com

The document is here. https://docs.nvidia.com/grid/16.0/grid-vgpu-user-guide/index.html#installing-vgpu-drivers-linux-from-debian-package

## vGPU driver installation

```shell
root@ubuntu-vm:/home/ubuntu# sudo chown -Rv _apt:root /var/cache/apt/archives/partial/
root@ubuntu-vm:/home/ubuntu# sudo chmod -Rv 700 /var/cache/apt/archives/partial/
ownership of '/var/cache/apt/archives/partial/' retained as _apt:root
mode of '/var/cache/apt/archives/partial/' retained as 0700 (rwx------)
root@ubuntu-vm:/home/ubuntu# apt-get install ./nvidia-linux-grid-525_525.125.06_amd64.deb -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'nvidia-linux-grid-525' instead of './nvidia-linux-grid-525_525.125.06_amd64.deb'
nvidia-linux-grid-525 is already the newest version (525.125.06).
0 upgraded, 0 newly installed, 0 to remove and 78 not upgraded.
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# apt-get install ./nvidia-linux-grid-525_525.125.06_amd64.deb -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
...
Setting up build-essential (12.9ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
Scanning processes...
Scanning linux images...

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```

## vGPU license activation

The document is here. https://docs.nvidia.com/grid/16.0/grid-licensing-user-guide/index.html

Copy *.tok file to /etc/nvidia/ClientConfigToken/ ,which is nvidia directory



```shell
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# cp client_configuration_token_08-29-2023-07-34-28.tok /etc/nvidia/ClientConfigToken/
root@ubuntu-vm:/home/ubuntu# ll /etc/nvidia/ClientConfigToken/
total 12
drwxr-x--x 2 root root 4096 Aug 29 13:35 ./
drwxr-xr-x 5 root root 4096 Aug 29 13:30 ../
-rw-r--r-- 1 root root 2728 Aug 29 13:35 client_configuration_token_08-29-2023-07-34-28.tok
root@ubuntu-vm:/home/ubuntu#
```

Reboot VM or restart service 'nvidia-gridd'

The output should looks like as below.

![image-2023-8-29_22-37-34](https://github.com/router-gao/ai-demos/assets/144886373/943fbabd-5842-4f5f-8187-35f7af248375)




![image-2023-8-29_22-38-54](https://github.com/router-gao/ai-demos/assets/144886373/8913b67c-792b-4ebe-b3c0-6e230a9d1e22)


After install tinykube and GPU Operator, the output is as below.


![image-2023-8-29_23-21-54](https://github.com/router-gao/ai-demos/assets/144886373/91e869bc-c949-4e37-aeab-2f6b21615d19)


After install deepstream App, the output is as below.


![image-2023-8-29_23-34-20](https://github.com/router-gao/ai-demos/assets/144886373/5e60f94c-1e75-4d87-aeea-b8d5b0e90f7c)


Migration and traffic analysis demo

![image-2023-8-29_23-36-39](https://github.com/router-gao/ai-demos/assets/144886373/a65fc669-59a5-4f4b-bd60-8d7a390abe76)


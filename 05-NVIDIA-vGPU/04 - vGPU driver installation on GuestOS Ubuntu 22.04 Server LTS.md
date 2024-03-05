
vGPU installation
the driver could be download from NVIDIA license server https://nvia.nvidia.com

The document is here. https://docs.nvidia.com/grid/16.0/grid-vgpu-user-guide/index.html#installing-vgpu-drivers-linux-from-debian-package

vGPU driver installation
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
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
vGPU license activation
The document is here. https://docs.nvidia.com/grid/16.0/grid-licensing-user-guide/index.html

Copy *.tok file to /etc/nvidia/ClientConfigToken/

copy tok file nvidia directory
1
2
3
4
5
6
7
8
root@ubuntu-vm:/home/ubuntu#
root@ubuntu-vm:/home/ubuntu# cp client_configuration_token_08-29-2023-07-34-28.tok /etc/nvidia/ClientConfigToken/
root@ubuntu-vm:/home/ubuntu# ll /etc/nvidia/ClientConfigToken/
total 12
drwxr-x--x 2 root root 4096 Aug 29 13:35 ./
drwxr-xr-x 5 root root 4096 Aug 29 13:30 ../
-rw-r--r-- 1 root root 2728 Aug 29 13:35 client_configuration_token_08-29-2023-07-34-28.tok
root@ubuntu-vm:/home/ubuntu#
Reboot VM or restart service 'nvidia-gridd'

The output should looks like as below.

 

After install tinykube and GPU Operator, the output is as below.



After install deepstream App, the output is as below.



Migration and traffic analysis demo


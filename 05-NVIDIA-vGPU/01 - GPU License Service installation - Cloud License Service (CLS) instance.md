## There are 2 kinds of license service - CLS and DLS

* Cloud License Service (CLS) instance. 
A CLS instance is hosted on the NVIDIA Licensing Portal. If the VMs can access Internet all the time, use CLS for quick installation and configuration.

* Delegated License Service (DLS) instance. 
A DLS instance is hosted on-premises at a location that is accessible from your private network, such as inside your data center. If the VMs are running is airgap environment, DLS is the choice.

**It's recommended to install the GPU License System in the first step. Without Licence Service (either CLS or DLS), vGPU on VMs can not be activated in Guest OS!**

The process of CLS installation is

- [ ] register NVIDIA Enterprise account with VMware email and apply for vGPU trial license
- [ ] login to NVIDIA Licensing Port and confirm the trial license
- [ ] create a License Service for vGPU

## register NVIDIA Enterprise account and apply for vGPU trial license

Use VMware email to register NVIDIA Enterprise Account.
https://enterpriseproductregistration.nvidia.com/?LicType=EVAL&ProductFamily=vGPU

To apply for NAVIE trial license, use the link below.

https://enterpriseproductregistration.nvidia.com/?LicType=EVAL&ProductFamily=NVAIEnterprise

## login to NVIDIA Licensing Port and confirm the trial license

https://nvid.nvidia.com/
NLP - Dashboard (nvidia.com)

## create a License Service for vGPU

The process is -

- [ ] create license server

- [ ] create service instance
- [ ] bind the license server to the service instance
- [ ] install the license server the the service instance
- [ ] download the *.tok file from service instance
- [ ] upload the *.tok file to VMs and activate the vGPU license on VMs
- [ ] check the 'LEASES' information from NVIDIA Licensing Portal

### create license server

### create Service Instance

### bind License Server to the Service Instance

### install License Server to the Service Instance

### Select the right *.tok file and download it to local

### upload the *.tok file to VMs and activate the vGPU license on VMs

Follow the quick start guide to active vGPU in Ubuntu/Windows, etc.

vGPU Quick Start Guide v3.1.0
https://docs.nvidia.com/license-system/latest/nvidia-license-system-quick-start-guide/

**Example of selecting the right *.tok file for Guest OS.**

The Guest OS is Ubuntu 22.04 LTS, and its profile is grid_T4_2A, so it's required license is vApps.


https://docs.nvidia.com/grid/latest/grid-vgpu-user-guide/#vgpu-types-tesla-t4



One more way to check the License and other information is to run the CLI on ESXi host. From the below screen shot, it shows lots of information.

### Upload *.tok file and active the vGPU on VM (Ubuntu)

active vGPU on Ubuntu

```shell
chmod 744 client_configuration_token_07-22-2023-02-10-21.tok
mv client_configuration_token_07-22-2023-02-10-21.tok /etc/nvidia/ClientConfigToken/
service nvidia-gridd restart
service nvidia-gridd status
nvidia-smi -q | grep -i license
```

check license status

```bash
root@ubuntu-vm:~# nvidia-smi -q | grep -i license
    vGPU Software Licensed Product
        License Status                    : Licensed (Expiry: 2023-7-23 13:17:27 GMT)
root@ubuntu-vm:~#
```



### Upload *.tok file and active the vGPU on VM (Windows10)

Copy the client configuration token to the %SystemDrive%:\Program Files\NVIDIA Corporation\vGPU Licensing\ClientConfigToken folder.
Restart Windows OS

### check the 'LEASES' information from NVIDIA Licensing Portal

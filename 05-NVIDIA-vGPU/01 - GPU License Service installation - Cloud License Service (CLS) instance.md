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
![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57.png) 
![image-2023-7-25_15-30-57](https://github.com/router-gao/ai-demos/assets/144886373/4045690e-eea1-4400-b2a0-58a6c3e3cfb0)


![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-1.png) 

![image-2023-7-25_15-30-57-1](https://github.com/router-gao/ai-demos/assets/144886373/1640edf5-6ce9-4848-9c5c-e9d6a7778ef7)

![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-2.png) 
![image-2023-7-25_15-30-57-2](https://github.com/router-gao/ai-demos/assets/144886373/e5a0e831-e8ba-494c-af35-fc4dbd53314d)


![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-3.png)
![image-2023-7-25_15-30-57-3](https://github.com/router-gao/ai-demos/assets/144886373/a1adbd62-8247-4b71-b4b8-8673d4abc9bb)

### create Service Instance
 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-4.png)
 ![image-2023-7-25_15-30-57-4](https://github.com/router-gao/ai-demos/assets/144886373/cae556d4-9d27-4ff8-8dae-e71f26332963)


 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-5.png)
 ![image-2023-7-25_15-30-57-5](https://github.com/router-gao/ai-demos/assets/144886373/b27c1e33-21a0-46d4-88f5-5e892b1fb391)


### bind License Server to the Service Instance
 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-6.png) 
 ![image-2023-7-25_15-30-57-6](https://github.com/router-gao/ai-demos/assets/144886373/0b00ab84-1560-4170-a909-de546c320d81)


![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-7.png)
![image-2023-7-25_15-30-57-7](https://github.com/router-gao/ai-demos/assets/144886373/51c487d6-7839-44d1-bcf5-3644cf3e2ba5)


### install License Server to the Service Instance
 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-8.png)
 ![image-2023-7-25_15-30-57-8](https://github.com/router-gao/ai-demos/assets/144886373/632f0722-27e2-441f-b753-678ca2ee1d8b)


 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-9.png)
 ![image-2023-7-25_15-30-57-9](https://github.com/router-gao/ai-demos/assets/144886373/72a3a6da-e169-4024-808a-237b88f6ceed)


![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-10.png) 
![image-2023-7-25_15-30-57-10](https://github.com/router-gao/ai-demos/assets/144886373/de818ce9-08aa-4f99-8473-667ab9f134e9)


![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-11.png)
![image-2023-7-25_15-30-57-11](https://github.com/router-gao/ai-demos/assets/144886373/e7890b24-9057-4ccc-815d-7874b7422d00)


### Select the right *.tok file and download it to local
 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-12.png)
 ![image-2023-7-25_15-30-57-12](https://github.com/router-gao/ai-demos/assets/144886373/de5ebe53-ed2c-4feb-a904-1f0f162d8537)


 ![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_15-30-57-13.png)
 ![image-2023-7-25_15-30-57-13](https://github.com/router-gao/ai-demos/assets/144886373/f42e2238-9792-4a0d-b06c-2641c1930b52)


### upload the *.tok file to VMs and activate the vGPU license on VMs


Follow the quick start guide to active vGPU in Ubuntu/Windows, etc.

vGPU Quick Start Guide v3.1.0
https://docs.nvidia.com/license-system/latest/nvidia-license-system-quick-start-guide/

**Example of selecting the right *.tok file for Guest OS.**

The Guest OS is Ubuntu 22.04 LTS, and its profile is grid_T4_2A, so it's required license is vApps.
![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-27_16-18-59.png)
![image-2023-7-27_16-18-59](https://github.com/router-gao/ai-demos/assets/144886373/ee792b1a-9d5b-4115-909c-c34d999ed59d)


https://docs.nvidia.com/grid/latest/grid-vgpu-user-guide/#vgpu-types-tesla-t4

![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-27_16-14-6.png)
![image-2023-7-27_16-14-6](https://github.com/router-gao/ai-demos/assets/144886373/7aa6abad-9dbb-4b1f-842c-b3422e3c6261)


One more way to check the License and other information is to run the CLI on ESXi host. From the below screen shot, it shows lots of information.
![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-27_16-22-15.png)
![image-2023-7-27_16-22-15](https://github.com/router-gao/ai-demos/assets/144886373/168484c4-3573-408e-ae46-b009f941be9d)


### Upload *.tok file and active the vGPU on VM (Ubuntu)

active vGPU on Ubuntu

```bash
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

![img](./01 - GPU License Service installation - Cloud License Service (CLS) instance - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-25_16-9-30.png)
![image-2023-7-25_16-9-30](https://github.com/router-gao/ai-demos/assets/144886373/ab3d370d-6444-481f-852c-9736d549cf06)





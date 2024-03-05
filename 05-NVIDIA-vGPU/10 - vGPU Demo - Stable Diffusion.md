## Process

### VMware Side Configuration

- [ ] Install GPU drivers and GPU manager on ESXi (SSH login)
- [ ] PCI device set up

- [ ] VM (Windows10 or Ubuntu desktop) set up


### NVIDIA Software Configuration

- [ ] License Server set up
- [ ] Install vGPU drivers in Guest OS

- [ ] Download *.tok file and active the vGPU license

- [ ] Monitor the vGPU Status


### App Stable Diffusion Deployment

- [ ] Install python 3.10 and Git
- [ ] Download automatic1111 web GUI

- [ ] Download Stable Diffusion 1.5/2.0 model

- [ ] Start automatic1111 and load Stable Diffusion

- [ ] You can try Stable Diffusion features (txt2img, img2img...)


## Critical Steps Screen Shots

**PCI Device set up**

![img](./10 - vGPU Demo - Stable Diffusion - HoTT Team - Public - VMware Core Confluence_files/image-2023-8-28_9-10-11.png) 

![image-2023-8-28_9-10-11](https://github.com/router-gao/ai-demos/assets/144886373/a16c8b14-3bec-4a02-93c9-7dd43d6b4a58)


![img](./10 - vGPU Demo - Stable Diffusion - HoTT Team - Public - VMware Core Confluence_files/image-2023-8-28_9-10-32.png)

![image-2023-8-28_9-10-32](https://github.com/router-gao/ai-demos/assets/144886373/71ae367a-cdb9-4704-95ad-e3d31b177b7b)


![img](./10 - vGPU Demo - Stable Diffusion - HoTT Team - Public - VMware Core Confluence_files/image-2023-8-28_9-10-58.png)
![image-2023-8-28_9-10-58](https://github.com/router-gao/ai-demos/assets/144886373/2078e40d-ccf2-4e5a-88e6-9cfa38447181)

**VM set up**

![img](./10 - vGPU Demo - Stable Diffusion - HoTT Team - Public - VMware Core Confluence_files/image-2023-8-28_9-11-45.png)

![image-2023-8-28_9-11-45](https://github.com/router-gao/ai-demos/assets/144886373/909b7439-9b57-4edd-978a-8ebcda0daca8)

**Download drivers from license driver** ( https://nvid.nvidia.com/ ), detail process could be found here. https://github.com/router-gao/ai-demos/blob/main/05-NVIDIA-vGPU/01%20-%20GPU%20License%20Service%20installation%20-%20Cloud%20License%20Service%20(CLS)%20instance.md

![image-2023-8-28_9-13-12](https://github.com/router-gao/ai-demos/assets/144886373/3813a286-1d0b-4d62-8382-a4624c0a4821)



**Unzip the driver file and get the GuestOS drivers. Install the Windows driver. Reboot the GuestOS to active the license.**



![image-2023-8-28_9-13-35](https://github.com/router-gao/ai-demos/assets/144886373/f9ab4224-d59d-4b62-8e98-ff2cfb3b15f2)



**Generate client config token and put it into GuestOS directory C:\Program Files\NVIDIA Corporation\vGPU Licensing\ClientConfigToken**

![image-2023-8-28_9-14-33](https://github.com/router-gao/ai-demos/assets/144886373/8f69ca55-f3c7-4e0d-b7a7-1ceb0fb5890b)



![image-2023-8-28_9-14-49](https://github.com/router-gao/ai-demos/assets/144886373/6632393a-1746-4dc0-8f8f-e2f374e0ca28)



 ![image-2023-8-28_9-15-14](https://github.com/router-gao/ai-demos/assets/144886373/f1f69677-22eb-4619-b084-25b08a21d320)

**login to license portal and check if the license is activated successfully.**



![image-2023-8-28_9-16-55](https://github.com/router-gao/ai-demos/assets/144886373/eadc4002-fa20-4637-a736-b6c79741707e)

**Monitor the GPU performance from Task manager**




![image-2023-8-28_9-18-15](https://github.com/router-gao/ai-demos/assets/144886373/68be303a-f769-4421-8b26-d4f5dab04f11)



**Install Python 3.10 from Microsoft Store on GuestOS, and check the result.**

![image-2023-8-28_9-19-24](https://github.com/router-gao/ai-demos/assets/144886373/ca15032f-6325-4e04-ba33-a784ddf140f8)



 ![image-2023-8-28_9-20-12](https://github.com/router-gao/ai-demos/assets/144886373/c2bd2f02-07ad-4951-bec4-aee7955439a0)

**Install Git on GuestOS, the download link is  https://git-scm.com/download/win** 


![image-2023-8-28_9-21-8](https://github.com/router-gao/ai-demos/assets/144886373/6e3e062c-360f-4530-99ec-8a7b7be2b981)




Gitclone automatic1111 to GuestOS. (git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git)
![image-2023-8-28_9-22-37](https://github.com/router-gao/ai-demos/assets/144886373/1eb0370a-c9bf-4bc3-9b94-19f0aa01df26)





**Download Stable Diffusion model (*.ckpt file) https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt**

**And move the ckpt file to directory C:\Users\admin\stable-diffusion-webui\models\Stable-diffusion**


![image-2023-8-28_9-24-55](https://github.com/router-gao/ai-demos/assets/144886373/c15076fd-d032-43e2-aab7-38ae6aa772bb)



**Start automatic1111 (double click the webui-user.bat file in directory C:\Users\admin\stable-diffusion-webui ) to load Stable Diffusion 1.5**

![image-2023-8-28_9-25-31](https://github.com/router-gao/ai-demos/assets/144886373/7ae90dd2-68d0-49ba-803c-23d20a769a1a)



**From the CMD Window to monitor the process. It may cost 10 minutes to download and install all packages.**

**At last it will show the URL to login the Stable Diffusion GUI [http://127.0.0.1:7860](http://127.0.0.1:7860/) (no username and password is required)**


![image-2023-8-28_9-27-29](https://github.com/router-gao/ai-demos/assets/144886373/890832c6-6d72-4275-b61a-348ce149c5b8)


![image-2023-8-28_9-27-46](https://github.com/router-gao/ai-demos/assets/144886373/b6372c74-d94a-4034-90f7-d5a783d05fb5)

**Login to http://127.0.01:7860 to test some Prompts**

- Prompt1:  Cute darth vader style minion, holidays in Paris Eiffel Tower, unreal engine, octane render, 4k




- Prompt2: Cute small cat sitting in a movie theater eating chicken wiggs watching a movie ,unreal engine, cozy indoor lighting, artstation, detailed, digital painting,cinematic,character design by mark ryden and pixar and hayao miyazaki, unreal 5, daz, hyperrealistic, octane render
- Negative prompt: ugly, ugly arms, ugly hands,
- Parameters: 
  - Steps: 25, 
  - Sampler: Euler a, 
  - CFG scale: 8.0, 
  - Seed: 3099373267, 
  - Size: 512x512

![image-2023-8-25_2-39-1](https://github.com/router-gao/ai-demos/assets/144886373/8716d1d5-1b3c-4f6c-bb43-f13b7eac5452)


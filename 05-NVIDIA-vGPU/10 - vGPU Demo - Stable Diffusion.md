Process
VMware Side Configuration
Install GPU drivers and GPU manager on ESXi (SSH login)

PCI device set up

VM (Windows10 or Ubuntu desktop) set up

NVIDIA Software Configuration
License Server set up

Install vGPU drivers in Guest OS

Download *.tok file and active the vGPU license

Monitor the vGPU Status

App Stable Diffusion Deployment
Install python 3.10 and Git

Download automatic1111 web GUI

Download Stable Diffusion 1.5/2.0 model

Start automatic1111 and load Stable Diffusion

You can try Stable Diffusion features (txt2img, img2img...)



PCI Device  set up

 

VM set up



Download drivers from license driver ( https://nvid.nvidia.com/ ), detail process could be found here. ( 01 - GPU License Service installation - Cloud License Service (CLS) instance )



Unzip the driver file and get the GuestOS drivers. Install the Windows driver. Reboot the GuestOS to active the license.





Generate client config token and put it into GuestOS directory C:\Program Files\NVIDIA Corporation\vGPU Licensing\ClientConfigToken

  

login to license portal and check if the license is activated successfully.



Monitor the GPU performance from Task manager



Install Python 3.10 from Microsoft Store on GuestOS, and check the result.

 

Install Git on GuestOS, the download link is  https://git-scm.com/download/win 



Gitclone automatic1111 to GuestOS. (git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git)


Download Stable Diffusion model (*.ckpt file) https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt

And move the ckpt file to directory C:\Users\admin\stable-diffusion-webui\models\Stable-diffusion



Start automatic1111 (double click the webui-user.bat file in directory C:\Users\admin\stable-diffusion-webui ) to load Stable Diffusion 1.5



From the CMD Window to monitor the process. It may cost 10 minutes to download and install all packages.

At last it will show the URL to login the Stable Diffusion GUI http://127.0.0.1:7860 (no username and password is required)

 

Login to http://127.0.01:7860 to test some Prompts

Prompt1:  Cute darth vader style minion, holidays in Paris Eiffel Tower, unreal engine, octane render, 4k



Prompt2: Cute small cat sitting in a movie theater eating chicken wiggs watching a movie ,unreal engine, cozy indoor lighting, artstation, detailed, digital painting,cinematic,character design by mark ryden and pixar and hayao miyazaki, unreal 5, daz, hyperrealistic, octane render
Negative prompt: ugly, ugly arms, ugly hands,
Parameters: Steps: 25, Sampler: Euler a, CFG scale: 8.0, Seed: 3099373267, Size: 512x512





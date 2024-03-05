**The installation process is 5 minutes or less, while it may cost you the whole day to figure out 'why the vGPU does not work' or 'why the App does not work'.**

Please go through the check list carefully. 

- [ ] confirm the features of GPU hardware

- [ ] figure out the right license for vGPU
- [ ] download driver software bundle
- [ ] apply NVIDIA account
- [ ] set up trial license server
- [ ] set up BIOS
- [ ] check ESXi GPU configuration - important!
- [ ] install vGPU driver and Management daemon
- [ ] install drivers on the VMs and activate the trial license
- [ ] run GPU Apps

## figure out the right license for vGPU

01 - GPU License Service installation - Cloud License Service (CLS) instance, "Example of selecting the right *.tok file for Guest OS."

https://github.com/router-gao/ai-demos/blob/main/05-NVIDIA-vGPU/01%20-%20GPU%20License%20Service%20installation%20-%20Cloud%20License%20Service%20(CLS)%20instance.md

## download driver software bundle

01 - GPU License Service installation - Cloud License Service (CLS) instance

https://github.com/router-gao/ai-demos/blob/main/05-NVIDIA-vGPU/01%20-%20GPU%20License%20Service%20installation%20-%20Cloud%20License%20Service%20(CLS)%20instance.md

## apply NVIDIA account and set up trial license server

follow the Confluence page here.

01 - GPU License Service installation - Cloud License Service (CLS) instance

https://github.com/router-gao/ai-demos/blob/main/05-NVIDIA-vGPU/01%20-%20GPU%20License%20Service%20installation%20-%20Cloud%20License%20Service%20(CLS)%20instance.md

## set up BIOS

SR-IOV enabled for any MIG test in the future.

## check ESXi GPU configuration - important!

Make sure GPU Passthrough is disabled!

In some cases, GPU is configured as 'passthrough enabled'. In that case, GPU drivers can be installed, but 'nvidia-smi' output will show error messages.


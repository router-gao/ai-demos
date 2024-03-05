Created @ 2023-Aug

Llama 2 could be deployed by text-generation-webui automatically on MacOS, Linux, and Windows.

Currently (2023-Aug) the most simple way is Windows 10 VM + Passthrough GPU. Ubuntu 22.04 desktop are almost the same.

## Pre-config

Win10 VM resource as below

16 vCPU (50% utilization in the demo)
32G RAM (50% utilization in the demo)
500G thin provisioning HD （150G used for Llama-2-13B model）
T4 GPU passthrough (6G is used in Llama-2-13B model)
Install T4 GPU driver. After rebooting, check the status by CLI "nvidia-smi"

## Installation of text-generation-webui

Please follow this doc, 02 - text-generation-webui

## Download and load Llama 2 model

In WDC, Llama-2-7B model may need 2 - 3 minutes to down, Llama-2-13B needs 15 - 20 mins in the first time, and about 5 minutes after that. (maybe CDN helps)



## Basic Configuration



## Demo of Deployment, Tuning, Validation

https://github.com/router-gao/ai-demos/tree/main/01-fine-tuning


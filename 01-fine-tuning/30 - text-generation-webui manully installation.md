Manually installation can make a better understanding of fine-tuning components and the process.

Please follow the guide here. https://github.com/oobabooga/text-generation-webui

There are one-click automation installation guide for text-generation-webui. To save time of environment, automation installation is the choice.

02 - text-generation-webui



Resource of the VM
OS = Ubuntu 22.04 desktop LTS

vCPU = 32

RAM = 64G

Harddisk = 500G (thin provision)



bash script
#!/bin/bash
cd ~
curl -sL "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" > "miniconda3.sh"
bash miniconda3.sh
echo "miniconda is installed"
 
echo "
#### please copy the below command to activate the textgen session and install packages ####
source /home/ubuntu/.bashrc
conda create -n textgen python=3.10.9 -y
conda activate textgen
echo "textgen is activated"
 
echo "install PyTorch"
pip3 install torch torchvision torchaudio
 
cd ~/
git clone https://github.com/oobabooga/text-generation-webui
cd ./text-generation-webui
pip install -r requirements.txt
 
"
 
echo "
#### to start the the webui, copy the command below to run ####
# conda activate textgen
# cd ~/text-generation-webui
# python server.py --share
 
"




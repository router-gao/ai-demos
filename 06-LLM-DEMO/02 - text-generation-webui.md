
Github https://github.com/oobabooga/text-generation-webui

Conda/Anaconda is not mandatory. Text-generation-webui will install it automatically.

## Download the One-click installer

![img](./02 - text-generation-webui - HoTT Team - Public - VMware Core Confluence_files/image-2023-8-14_21-44-23.png)

![image-2023-8-14_21-44-23](https://github.com/router-gao/ai-demos/assets/144886373/016fc872-b319-4779-ac6f-0bbd8f67d927)


### Ubuntu 22.04 LTS desktop installation

Download the installation file, and execute the CLI as below

Ubuntu CMD

```shell
$ apt-get update -y
$ apt-get install net-tools
$ apt-get install zip
$ unzip oobabooga_linux.zip
$ bash start_linux.sh
```


By default text-generation-webui will start automatically when power on.

### Windows 10 installation

- [ ] download 7zip
- [ ] unzip the zip file and click to install
- [ ] To start text-generation-webui after power on, click "start_windows.bat" file

### Login 

By default, only 127.0.0.1:7860 is accessible for the same VM.


![image-2023-9-21_13-16-18](https://github.com/router-gao/ai-demos/assets/144886373/241b3f3e-4480-4836-b65c-dfb6027f7fef)

The login page is http://127.0.0.1:7860

![image-2023-8-14_21-50-18](https://github.com/router-gao/ai-demos/assets/144886373/e2bc72e3-885e-4ff5-9d01-d6fab4010eda)


To make access from public URL, echo '--share' to the file ./oobabooga_linux/CMD_FLAGS.txt

![image-2023-9-21_13-20-1](https://github.com/router-gao/ai-demos/assets/144886373/c209fc9d-3695-42df-9a98-47f818265315)


![image-2023-9-21_13-19-15](https://github.com/router-gao/ai-demos/assets/144886373/8fa44b22-29e0-4ade-a2e9-86751e27a882)




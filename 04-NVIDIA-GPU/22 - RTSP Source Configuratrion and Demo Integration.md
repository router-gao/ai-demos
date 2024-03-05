# VLC

There are a few ways to generate RTSP stream to the App.

- regular RTSP camera
- regular connected to laptop, and VLC on that laptop converts the video into RTSP stream (or a few RTSM streams)
- a few video clips on the laptop, and VLC converts those videos into RTSP stream (or a few RTSM streams)

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_16-39-9.png)

![image-2023-7-11_16-39-9](https://github.com/router-gao/ai-demos/assets/144886373/9bea3abe-7bd9-419f-a314-0581b5d18299)


## Camera is the RTSP source

Use a regular RTSP Camera.

## Laptop integrated camera/desktop + VLC is the RTSP source

Ubuntu 22.04 desktop is recommended.

Ubuntu 22.04 configuration as below.

### disable screen lock

Settings - Privacy - disable 'Automatic Screen Lock'

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_16-46-15.png)

![image-2023-7-11_16-46-15](https://github.com/router-gao/ai-demos/assets/144886373/c3dcfff7-2175-4cd0-acb8-e058324a7efd)


### install free video editor 'shotcut'

**install shotcut**

```shell
apt-get install -y shotcut
```

### build a long video (60 mins or longer)

Open a sample video and keeps appending it into 30 - 50 mins long video

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_16-53-40.png)
![image-2023-7-11_16-53-40](https://github.com/router-gao/ai-demos/assets/144886373/ec2ad43d-a330-4eb7-b4e7-a8da2b6f9f26)



Select H.264 Baseline/Main Profile and export the new video.

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_16-55-36.png)

![image-2023-7-11_16-55-36](https://github.com/router-gao/ai-demos/assets/144886373/65ac0d9c-afb5-4929-8966-0d5cafe15107)


### install VLC and start the VLC stream server

Use CLI 'snap install vlc' to install VLC. In this way, VLC could play network stream by default. 

Other installation method, for example 'apt-get install -y vlc', the VLC may not be able to play rtsp stream without configuration.

**install VLC**

```shell
root@ubuntu-t460p:/home/ubuntu#
root@ubuntu-t460p:/home/ubuntu# snap install vlc
vlc 3.0.18 from VideoLAN✓ installed
root@ubuntu-t460p:/home/ubuntu#
root@ubuntu-t460p:/home/ubuntu# vlc -version
VLC is not supposed to be run as root. Sorry.
If you need to use real-time priorities and/or privileged TCP ports
you can use vlc-wrapper (make sure it is Set-UID root and
cannot be run by non-trusted users first).
root@ubuntu-t460p:/home/ubuntu#
```

### Start the first RTSP stream



![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36.png) 

![image-2023-7-4_23-16-36](https://github.com/router-gao/ai-demos/assets/144886373/adb89cc1-f780-412e-bca6-18b041b1e64b)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-1.png) 

![image-2023-7-4_23-16-36-1](https://github.com/router-gao/ai-demos/assets/144886373/c2ed937f-b18c-46da-a921-cd57eb168307)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-2.png) 

![image-2023-7-4_23-16-36-2](https://github.com/router-gao/ai-demos/assets/144886373/b297b241-a58b-49ee-b1b1-e38e906d4211)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-3.png)

![image-2023-7-4_23-16-36-3](https://github.com/router-gao/ai-demos/assets/144886373/b23e138a-90e5-4647-bd10-45438bab1402)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-4.png)

![image-2023-7-4_23-16-36-4](https://github.com/router-gao/ai-demos/assets/144886373/8c7ac251-786a-4ac5-86be-50426581d98b)


 ![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-5.png) 

![image-2023-7-4_23-16-36-5](https://github.com/router-gao/ai-demos/assets/144886373/0d3b5200-e64f-4070-8f19-dc7850890563)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-6.png) 

![image-2023-7-4_23-16-36-6](https://github.com/router-gao/ai-demos/assets/144886373/4c46e84a-268b-46de-94c5-9f3348f62a44)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-7.png) 

![image-2023-7-4_23-16-36-7](https://github.com/router-gao/ai-demos/assets/144886373/265dc9d1-3703-4b9b-859d-f6257d995afb)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-4_23-16-36-8.png) 

![image-2023-7-4_23-16-36-8](https://github.com/router-gao/ai-demos/assets/144886373/5deabda1-e70a-422b-b15c-f72a44dad668)


### start more VLC streams (in case more RTSP streams is required, which is optional)

Right click VLC icon and select 'New Window'. Repeat the above step and select a different port number of the new stream.

On another VM, open multi-VLC GUI to check if the all VLC sources are up and running.

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_17-1-1.png) 

![image-2023-7-11_17-1-1](https://github.com/router-gao/ai-demos/assets/144886373/18b1917b-879d-42b4-9073-4914dbe1df91)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_17-3-30.png)

![image-2023-7-11_17-3-30](https://github.com/router-gao/ai-demos/assets/144886373/7608c587-980c-4604-b2d5-ba334af0e41a)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_23-51-30.png)

![image-2023-7-11_23-51-30](https://github.com/router-gao/ai-demos/assets/144886373/3262725c-0716-4037-a408-70c549daa03f)


# RTSP Demo

To integrated multi RTSP sources into video, please follow the doc here. 

https://catalog.ngc.nvidia.com/orgs/nvidia/helm-charts/video-analytics-demo

**fetch helm chart to local**

```shell
root@ubuntu-vm:~# helm fetch https://helm.ngc.nvidia.com/nvidia/charts/video-analytics-demo-0.1.8.tgz --untar
root@ubuntu-vm:~#
root@ubuntu-vm:~# ll
total 142516
drwx------ 10 root   root       4096 Jul 10 15:54 ./
drwxr-xr-x 19 root   root       4096 Jun 26 03:42 ../
...
-rw-r--r--  1 root   root        341 Jun 29 07:19 ubuntu-22.04.yaml
drwxr-xr-x  4 root   root       4096 Jul 10 15:54 video-analytics-demo/
drwxr-xr-x  2 root   root       4096 Jul 10 15:54 video-analytics-demo-0.1.8.tgz/
-rw-------  1 root   root      13622 Jul  5 08:42 .viminfo
-rw-r--r--  1 root   root        215 Jul  2 16:22 .wget-hsts
root@ubuntu-vm:~#
root@ubuntu-vm:~#
root@ubuntu-vm:~# cd video-analytics-demo
root@ubuntu-vm:~/video-analytics-demo#
root@ubuntu-vm:~/video-analytics-demo# vim values.yaml
root@ubuntu-vm:~/video-analytics-demo#
```



Edit rtsp sources as below. And add 'rtspnodePort: 31113' to service section for VLC client monitoring.

**edit values.yaml**

```shell
root@ubuntu-vm:~# cat video-analytics-demo/values.yaml | grep camera -C 20
...
service:
  type: NodePort
  port: 80
  rtspnodePort: 31113
  webuiPort: 5080
  webuinodePort: 31115
 
#specify camera IP as rtsp://username:password@ip
#or rtsp://ip if it has no username and password
 
cameras:
  camera1: rtsp://10.0.72.106:8553/
  camera2: rtsp://10.0.72.106:8552/
  camera3: rtsp://10.0.72.106:8553/
  camera4: rtsp://10.0.72.106:8552/
  camera5: rtsp://10.0.72.106:8553/
  camera6: rtsp://10.0.72.106:8552/
  camera7: rtsp://10.0.72.106:8553/
  camera8: rtsp://10.0.72.106:8552/
  camera9: rtsp://10.0.72.106:8553/
  camera10: rtsp://10.0.72.106:8552/
  camera11: rtsp://10.0.72.106:8553/
  camera12: rtsp://10.0.72.106:8552/
  camera13: rtsp://10.0.72.106:8553/
  camera14: rtsp://10.0.72.106:8552/
  camera15: rtsp://10.0.72.106:8553/
  camera16: rtsp://10.0.72.106:8552/
 
...
root@ubuntu-vm:~#
```

Deploy helm chart, and get the rtsp info and web monitor info.

**deploy helm chart**

```shell
root@ubuntu-vm:~# helm install iva --values video-analytics-demo/values.yaml video-analytics-demo
NAME: iva
LAST DEPLOYED: Tue Jul 11 15:54:19 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the RTSP URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services iva-video-analytics-demo)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo rtsp://$NODE_IP:$NODE_PORT/ds-test
 
2.Get the WebUI URL by running these commands:
  export ANT_NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services iva-video-analytics-demo-webui)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$ANT_NODE_PORT
  Disclaimer:
  Note: Due to the output from DeepStream being real-time via RTSP, you may experience occasional hiccups in the video stream depending on network conditions.
root@ubuntu-vm:~#
root@ubuntu-vm:~#   export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services iva-video-analytics-demo)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo rtsp://$NODE_IP:$NODE_PORT/ds-test
rtsp://10.0.72.102:31113/ds-test
root@ubuntu-vm:~#
root@ubuntu-vm:~#   export ANT_NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services iva-video-analytics-demo-webui)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$ANT_NODE_PORT
http://10.0.72.102:31115
root@ubuntu-vm:~#
```

The web GUI and VLC client output.

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_23-58-7.png) 

![image-2023-7-11_23-58-7](https://github.com/router-gao/ai-demos/assets/144886373/71e6b9dd-5ac0-4366-88c8-39679fcecabb)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-11_23-59-18.png)

![image-2023-7-11_23-59-18](https://github.com/router-gao/ai-demos/assets/144886373/d81196e2-3151-4460-b539-8de23edba3b3)


Prometheus web GUI

![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-1-24.png)

![image-2023-7-12_0-1-24](https://github.com/router-gao/ai-demos/assets/144886373/3573fd68-404d-4df5-a8ce-44c0ed5405dd)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-1-48.png)

![image-2023-7-12_0-1-48](https://github.com/router-gao/ai-demos/assets/144886373/126b4daf-802a-458a-b054-2e695c369b37)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-4-1.png)
![image-2023-7-12_0-4-1](https://github.com/router-gao/ai-demos/assets/144886373/27dab62c-f19f-4c6f-bbe2-741fa02a0acd)



![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-4-43.png)

![image-2023-7-12_0-4-43](https://github.com/router-gao/ai-demos/assets/144886373/50c33822-283b-46a7-986a-a030028bb4e5)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-5-52.png)

![image-2023-7-12_0-5-52](https://github.com/router-gao/ai-demos/assets/144886373/0c25bd03-676c-4748-8afd-830a9753cb42)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-6-27.png)

![image-2023-7-12_0-6-27](https://github.com/router-gao/ai-demos/assets/144886373/68d3c5f7-2e41-4f5f-9f79-457d1fc2bfee)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-7-46.png)

![image-2023-7-12_0-7-46](https://github.com/router-gao/ai-demos/assets/144886373/76c11544-8443-4296-a608-c62ad5e573bc)


![img](./22 - RTSP Source Configuratrion and Demo Integration - HoTT Team - Public - VMware Core Confluence_files/image-2023-7-12_0-8-50.png)

![image-2023-7-12_0-8-50](https://github.com/router-gao/ai-demos/assets/144886373/8b9602f3-85f8-49e2-b2f8-87bf16641f68)


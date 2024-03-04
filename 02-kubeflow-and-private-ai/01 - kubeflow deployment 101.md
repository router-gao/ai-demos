### A few ways to deploy kubeflow

microk8s based deployment (recommended for first time user)
https://charmed-kubeflow.io/docs

https://charmed-kubeflow.io/docs/install

Deploy a Ubuntu 22.04 Desktop on ESXi, and follow the document above. It will work.

### Cloud vendor based deployment

Packaged Distributions of Kubeflow. On 2023-Oct, the active distributions are as below. https://www.kubeflow.org/docs/started/installing-kubeflow/

VMware solution is TKGS based. https://vmware.github.io/vSphere-machine-learning-extension/

![image-2023-10-8_16-58-50](https://github.com/router-gao/ai-demos/assets/144886373/b1ff79c1-e3c2-427d-a362-8a093b6f2566)

### Manifest based deployment (Raw Kubeflow Manifests)

The document of Kubeflow Manifests is here. https://github.com/kubeflow/manifests

There are 2 kinds of deployment

### single command to install everything (recommend for advanced demo, quite similar to production deployment)

Ubuntu 22.04, minikube

03 - minikube kubeflow deployment

### step by step individual components installation

Ubuntu 22.04, minikube


### Process as below

- bootstrap Ubuntu 22.04 desktop version or Ubuntu 22.04 server version VM (16 vCPU, 32G RAM, 500G harddisk)

- install docker from script
- install minikube, kubectl and kustomize from script
- install kubeflow
- edit service and login to kubeflow

```shell
Install docker from script

#!/bin/bash

# Update package list

echo "Updating package list..."
sudo apt-get update -y

# Install Docker

echo "Installing Docker..."
sudo apt-get install -y docker.io

# Enable and start Docker service

echo "Enabling and starting Docker service..."
sudo systemctl enable docker
sudo systemctl start docker

# Test Docker installation

echo "Testing Docker installation..."
docker ps
docker run hello-world

# Add the current user to the Docker group

echo "Adding current user to Docker group..."
sudo usermod -aG docker $USER
newgrp docker

# reboot the vm

echo "Docker is installed successfully! Please reboot the VM!"
```



### Install minikube, kubectl and kustomize from script

install-minikube-kubectl-kustomize.sh



### Install kubeflow

Need 5 - 10 mins to finish.

```shell
#!/bin/bash

# Clone Kubeflow manifests and apply resources

echo "Cloning Kubeflow manifests..."
cd ~
git clone https://github.com/kubeflow/manifests/
cd ~/manifests
echo "Applying Kubeflow resources..."
while ! kustomize build example | kubectl apply -f -; do
    echo "Retrying to apply resources"
    sleep 10
done


echo "Script execution completed."
```



### Edit service and login to kubeflow

There are 2 services need to be edit 

### kubernetes dashboard (optional)

Get minikube dashboard api by using the command below

```shell
$ minikube dashboard --url 
```

Use command below to monitor dashboard is up and running

```shell
$ watch kubectl get pod -n kubernetes-dashboard
```



Config kubectl proxy as below. The original port 35443 is mapped to 8001

```shell
$ kubectl proxy --address='0.0.0.0' --disable-filter=true
```



Login from web browser from URL **http://<vm-ip>:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/**







### kubeflow

The default username and password to login kubeflow is **user@example.com, 12341234** 

**To login from the same VM, use the command below, and login from web browser http://localhost:8080**

```shell
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```



**To login from other VMs, use the command below, and login from web browser http://<ubuntu-ip>:<port>.**

In our case, the port number is 31380. Other port number is also accepted.

```shell
kubectl port-forward --address 0.0.0.0 svc/istio-ingressgateway -n istio-system 31380:80
```










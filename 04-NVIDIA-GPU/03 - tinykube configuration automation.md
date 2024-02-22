Keep configuration automation scripts here.

# swapoff

**swappoff**

```shell
#!/bin/bash
 
# Check if the script is being run as root
if [ "$EUID" -ne 0 ]
  then echo "Please run as root"
  exit
fi
 
# Disable swap
swapoff -a
 
# Remove swap entry from /etc/fstab
sed -i '/swap/Id' /etc/fstab
 
# Inform the user
echo "Swap has been permanently disabled and removed from /etc/fstab."
 
# Reboot to apply the changes
read -p "Do you want to reboot your system now? (y/n): " choice
if [ "$choice" = "y" ] || [ "$choice" = "Y" ]; then
  reboot
fi
```



# Deploy tinykube on Ubuntu 20.04/22.04

**preconfig**

```shell
#!/bin/bash
 
# Update package lists
echo "Updating package lists..."
apt-get update -y
 
# Install required packages
echo "Installing required packages..."
apt-get install -y net-tools vim curl wget openssh-server
apt-get install -y zstd conntrack ethtool socat make build-essential libseccomp-dev pkg-config jq apparmor unzip btrfs-progs libbtrfs-dev
 
# Disable swap
echo "Disabling swap..."
sudo swapoff -a
 
# Remove swap file (assuming it's located at /swap.img)
echo "Removing swap file..."
sudo rm /swap.img
 
# Install golang and alien
echo "Installing golang and alien..."
apt-get install -y golang alien
 
# Check Go version
echo "Checking Go version..."
go version
 
# Check Alien version
echo "Checking Alien version..."
alien --version
 
# Check if RPM package exists
rpm_package="tinykube-v1.25.7+tinykube.2-3.x86_64.rpm"
if [ ! -f "$rpm_package" ]; then
  echo "Error: RPM package '$rpm_package' not found!"
  exit 1
fi
 
# Convert RPM package to DEB using Alien
echo "Converting RPM package to DEB..."
alien -d "$rpm_package"
 
# Install the DEB package
echo "Installing Tinykube..."
dpkg -i tinykube_0v1.25.7+tinykube.2-4_amd64.deb
 
# Check Tinykube version
echo "Checking Tinykube version..."
tinykube version
 
echo "Script execution completed."
```



**deploy tinykube**

```shell
#!/bin/bash
 
# Navigate to the root directory
cd /
 
# Search for file1.txt and store the result in a variable
file_path=$(find / -name "tinykube_0v1.25.7+tinykube.2-4_amd64.deb")
 
# Check if the file exists
if [ -z "$file_path" ]; then
    echo "File file1.txt not found."
else
    # Extract the directory path from the file path
    dir_path=$(dirname "$file_path")
 
 
    # Navigate to the directory
    cd "$dir_path"
    echo "Navigated to $dir_path"
fi
 
 
# start to delete tinykube
echo "#### tinykube delete snc ####"
tinykube delete -f
 
echo "#### dpkg -r tinykube ####"
dpkg -r tinykube
 
echo "#### delete cluster config files ####"
rm -rf $HOME/.kube/config
 
echo "#### delete antrea cni config and antrea.yaml files ####"
rm -rf /root/antrea.*
rm -rf /etc/cni/net.d
rm -rf /var/lib/etcd
 
echo "#### clean up work is done ####"
 
echo "####install tinykube"
dpkg -i tinykube_0v1.25.7+tinykube.2-4_amd64.deb
echo "#### sleeep 30 seconds"
sleep 30
tinykube version
 
echo "#### deploy kubernetes"
tinykube start --skip-phases=default-cni
 
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
 
 
echo "#### start to install CNI antre ###"
wget https://github.com/antrea-io/antrea/releases/download/v1.2.3/antrea.yml
sed -i 's/projects.registry.vmware.com\/antrea\/antrea-ubuntu\:v1.2.3/projects-stg.registry.vmware.com\/tkg\/antrea-advanced-debian\:v1.2.3_vmware.4/g' antrea.yml
kubectl apply -f antrea.yml
 
 
echo "#### sleep 180 seconds"
sleep 180
 
 
echo "#### create a dummy pod"
cat > ubuntu-22.04.yaml <<-EOF
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-pod
spec:
  containers:
    - name: ubuntu-container
      image: ubuntu:22.04
      command: ["/bin/bash", "-c"]
      args:
        - |
          apt-get update -y &&
          apt-get install -y net-tools vim iputils-ping &&
          echo done > /tmp/log.txt &&
          sleep infinity
EOF
 
kubectl apply -f ubuntu-22.04.yaml
 
echo "#### check dummy pod status"
kubectl get pod -A
 
echo "#### tinykube installation is done ####"
```



# Helm installation and GPU-Operator installation

**install helm**

```shell
#!/bin/bash
 
# Install Helm
echo "Installing Helm..."
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm --yes
 
# Verify installation
echo "Verifying Helm installation..."
helm version
 
# Add Nvidia GPU Operator to local Helm repository
echo "Adding Nvidia GPU Operator to local Helm repository..."
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia
helm repo update
 
# Check if 'gpu-operator' namespace exists, if not, create it
echo "Checking if 'gpu-operator' namespace exists..."
if ! kubectl get namespace gpu-operator >/dev/null 2>&1; then
  echo "Creating 'gpu-operator' namespace..."
  kubectl create namespace gpu-operator
fi
 
# Deploy Nvidia GPU Operator in 'gpu-operator' namespace
echo "Deploying Nvidia GPU Operator in 'gpu-operator' namespace..."
helm install gpu-operator --devel nvidia/gpu-operator -n gpu-operator --create-namespace --wait --set operator.defaultRuntime=containerd
 
echo "Nvidia GPU Operator deployment completed successfully."
echo "wait for a couple of mins for gpu-operator pods running"
helm list -A
kubectl get pod -A

```



# Harbor implementation

**Harbor Integration**

```shell
#!/bin/bash
  
config_file='''version = 2
  
[plugins]
  [plugins."io.containerd.grpc.v1.cri"]
    sandbox_image = "k8s.gcr.io/pause:3.7"
    [plugins."io.containerd.grpc.v1.cri".registry]
      [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."harbor.example.com"]
          endpoint = ["https://harbor.example.com"]
      [plugins."io.containerd.grpc.v1.cri".registry.configs]
        [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor.example.com"]
          [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor.example.com".tls]
            insecure_skip_verify = true
            [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor.example.com".auth]
              username = "admin"
              password = "MySecurePassword"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
    runtime_type = "io.containerd.runc.v2"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
    SystemdCgroup = true'''
  
default_fqdn="harbor.example.com"
default_username="admin"
default_password="MySecurePassword"
  
echo "Default FQDN: $default_fqdn"
echo "Default username: $default_username"
echo "Default password: $default_password"
  
read -p "Enter the Harbor FQDN (or press Enter to use default): " harbor_fqdn
read -p "Enter the Harbor username (or press Enter to use default): " harbor_username
  
# Prompt for password without displaying input
stty -echo
read -p "Enter the Harbor password (or press Enter to use default): " harbor_password
stty echo
echo
  
# Assign default values if input is empty
if [ -z "$harbor_fqdn" ]; then
  harbor_fqdn="$default_fqdn"
fi
  
if [ -z "$harbor_username" ]; then
  harbor_username="$default_username"
fi
  
if [ -z "$harbor_password" ]; then
  harbor_password="$default_password"
fi
  
# Replace the Harbor URL, username, and password in the config file using sed
config_file=$(echo "$config_file" | sed "s/harbor.example.com/$harbor_fqdn/g")
config_file=$(echo "$config_file" | sed "s/admin/$harbor_username/g")
config_file=$(echo "$config_file" | sed "s/MySecurePassword/$harbor_password/g")
  
config_file_path="config.toml"
  
# Save the updated config file
echo "$config_file" > "$config_file_path"
  
echo "Harbor configuration updated in $config_file_path"
echo "Config file uploaded to the current directory"
echo "Please run systemctl restart containerd"
```



**Example of /etc/containerd/config.toml**

```shell
root@tinykube-129-2:/home/ubuntu# cat /etc/containerd/config.toml
 
version = 2
 
[plugins]
  [plugins."io.containerd.grpc.v1.cri"]
    sandbox_image = "k8s.gcr.io/pause:3.7"
    [plugins."io.containerd.grpc.v1.cri".registry]
      [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."harbor-20.tinykube.rocks"]
          endpoint = ["https://harbor-20.tinykube.rocks"]
      [plugins."io.containerd.grpc.v1.cri".registry.configs]
        [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor-20.tinykube.rocks"]
          [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor-20.tinykube.rocks".tls]
            insecure_skip_verify = true
            [plugins."io.containerd.grpc.v1.cri".registry.configs."harbor-20.tinykube.rocks".auth]
              username = "admin"
              password = "Harbor12345"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
    runtime_type = "io.containerd.runc.v2"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
    SystemdCgroup = true
root@tinykube-129-2:/home/ubuntu#
```



Tinykube default sandbox is [k8s.gcr.io/pause:3.7](http://k8s.gcr.io/pause:3.7). If it's Airgap environment, we can modify the sandbox_image as below.

 *sandbox_image = "10.0.72.130/pause/pause:3.7"*

**pause:3.7 handling in Airgap environment**

```shell
root@tinykube-129-2:/etc/containerd# cat config.toml
version = 2
 
[plugins]
  [plugins."io.containerd.grpc.v1.cri"]
    sandbox_image = "10.0.72.130/pause/pause:3.7"
    [plugins."io.containerd.grpc.v1.cri".registry]
      [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."10.0.72.130"]
          endpoint = ["https://10.0.72.130"]
      [plugins."io.containerd.grpc.v1.cri".registry.configs]
        [plugins."io.containerd.grpc.v1.cri".registry.configs."10.0.72.130"]
          [plugins."io.containerd.grpc.v1.cri".registry.configs."10.0.72.130".tls]
            insecure_skip_verify = true
            [plugins."io.containerd.grpc.v1.cri".registry.configs."10.0.72.130".auth]
              username = "admin"
              password = "Harbor12345"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
    runtime_type = "io.containerd.runc.v2"
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
    SystemdCgroup = true
 
root@tinykube-129-2:/etc/containerd#
```

# Modify static IP on Ubuntu 22.04 Server OS and 20.04 Server OS

**modify static IP on Ubuntu**

```shell
#!/bin/bash
 
# Prompt user for Ubuntu version
read -p "Enter Ubuntu version (1=22.04, 2=20.04): " ubuntu_version
 
# Prompt user for network details
read -p "Enter Ethernet interface name (default is ens33): " ethernet_name
ethernet_name=${ethernet_name:-ens33}
 
read -p "Enter IP address: " ip_address
read -p "Enter subnet mask (default is 24): " subnet_mask_input
read -p "Enter gateway: " gateway
read -p "Enter DNS server(s) (comma-separated if multiple): " dns_servers
 
# Set the default subnet mask to 24 if the input is empty
subnet_mask=${subnet_mask_input:-24}
 
 
# Determine the netplan configuration file path based on the Ubuntu version
if [ "$ubuntu_version" = "1" ]; then
    config_file="/etc/netplan/01-netcfg.yaml"
elif [ "$ubuntu_version" = "2" ]; then
    config_file="/etc/netplan/00-installer-config.yaml"
else
    echo "Invalid Ubuntu version!"
    exit 1
fi
 
# Echo network configuration details
echo "Configuring network:"
echo "Ubuntu version: $ubuntu_version"
echo "Ethernet interface: $ethernet_name"
echo "IP address: $ip_address/$subnet_mask"
echo "Gateway: $gateway"
echo "DNS servers: $dns_servers"
 
# Create the draft netplan configuration file
echo "Creating draft netplan configuration file..."
cat > "$config_file" << EOL
network:
  version: 2
  renderer: networkd
  ethernets:
    $ethernet_name:
      addresses:
        - $ip_address/$subnet_mask
      routes:
        - to: 0.0.0.0/0
          via: $gateway
      nameservers:
        addresses: [$dns_servers]
EOL
 
# Apply the netplan configuration
echo "Applying netplan configuration..."
# sudo netplan apply
 
echo "Configuration file created and applied successfully."
```

# Official Process

## Regular TKGm Workload Cluster bootstrapping (Single node-pool)

**single node-pool no GPU official yaml**

```shell
#! ---------------------------------------------------------------------
#! Basic cluster creation configuration
#! ---------------------------------------------------------------------
 
CLUSTER_NAME: workload-31
CLUSTER_PLAN: dev
NAMESPACE: default
# CLUSTER_API_SERVER_PORT: # For deployments without NSX Advanced Load Balancer
CNI: antrea
 
#! ---------------------------------------------------------------------
#! Node configuration
#! ---------------------------------------------------------------------
 
# SIZE:
# CONTROLPLANE_SIZE:
# WORKER_SIZE:
 
# VSPHERE_NUM_CPUS: 2
# VSPHERE_DISK_GIB: 40
# VSPHERE_MEM_MIB: 4096
 
# VSPHERE_CONTROL_PLANE_NUM_CPUS: 2
# VSPHERE_CONTROL_PLANE_DISK_GIB: 40
# VSPHERE_CONTROL_PLANE_MEM_MIB: 8192
VSPHERE_WORKER_NUM_CPUS: 8
# VSPHERE_WORKER_DISK_GIB: 40
VSPHERE_WORKER_MEM_MIB: 16384
 
# CONTROL_PLANE_MACHINE_COUNT:
WORKER_MACHINE_COUNT: 1
# WORKER_MACHINE_COUNT_0:
# WORKER_MACHINE_COUNT_1:
# WORKER_MACHINE_COUNT_2:
 
#! ---------------------------------------------------------------------
#! vSphere configuration
#! ---------------------------------------------------------------------
 
#VSPHERE_CLONE_MODE: "fullClone"
VSPHERE_NETWORK: /Datacenter/network/pg-vlan2003-tkgm
# VSPHERE_TEMPLATE:
# VSPHERE_TEMPLATE_MOID:
# IS_WINDOWS_WORKLOAD_CLUSTER: false
# VIP_NETWORK_INTERFACE: "eth0"
VSPHERE_SSH_AUTHORIZED_KEY: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2hFxSAbATgfpJeXx67tn12ux8B8aZ6DITdqsvM8pzXQeuK7Op4gxvNsTi+cr7gJFjipUtrSasB2eUSRRCN4lFW3PikKMVwp6bKyr/AkoQAoX3TNWubkb4hAfsMJkCtsrP/yzkMR+fGNbbBAv7iYCI2EIRlFrpj7FvwGmSrlIm7OPz0NjFh0QDE3oh6SnKxLFTMHW7kpjSjWXdL4uIbnXXnL5n3XvaA3vBminmN16o5KicR3aEcwZcQ6a3xhL5yx788WK8jp3tinSysIOuCV6pUfU/g9dl7kEfnUubUB2niPOb3BTaP8V/eMH5ONnmdz7izreNtvEuvYmtUByAE8upaQZZaw1IA3JR3JS2fOJSYPdV9IiEFC8Rsskbno9j3FEuYov0ZEFKavh0s3yOV3vxrmzjl8lXnMomGHSnCL6EDn1nvH3giC9LNwwxCkKl/6Z2C4mZENoqBzQMGNt4shLUfqBfWeFzFx8QzZJK7MSFr/L45OUgWMKdRweiwb7p0VH2BYIBjBadbPnLxwGvzQYUEATVZhrnX5fCqi+jJ9sEQfzKC3Bmm3sy+qsTLQTf3JmCGonW30IPmxzd8xP07gvtJF85/ANknDjCfE3KNcrbXaw4enSgcoq1j1NmSCTgobOhXltJEsrfgGDkgpon5W3JfNlhzvls+RuizZGOMtzLIw== email@example.com
VSPHERE_USERNAME: administrator@vsphere.local
VSPHERE_PASSWORD: <encoded:Vk13YXJlMSE=>
# VSPHERE_REGION:
# VSPHERE_ZONE:
# VSPHERE_AZ_0:
# VSPHERE_AZ_1:
# VSPHERE_AZ_2:
# VSPHERE_AZ_CONTROL_PLANE_MATCHING_LABELS:
VSPHERE_SERVER: 10.252.12.99
VSPHERE_DATACENTER: /Datacenter
VSPHERE_RESOURCE_POOL: /Datacenter/host/00-cluster-mgmt/Resources/rp-tkg-workload-111
VSPHERE_DATASTORE: /Datacenter/datastore/ds-30-2T-02
VSPHERE_FOLDER: /Datacenter/vm/folder-tkg
# VSPHERE_MTU:
# VSPHERE_STORAGE_POLICY_ID
# VSPHERE_WORKER_PCI_DEVICES:
# VSPHERE_CONTROL_PLANE_PCI_DEVICES:
# VSPHERE_IGNORE_PCI_DEVICES_ALLOW_LIST:
# VSPHERE_CONTROL_PLANE_CUSTOM_VMX_KEYS:
# VSPHERE_WORKER_CUSTOM_VMX_KEYS:
# WORKER_ROLLOUT_STRATEGY: "RollingUpdate"
# VSPHERE_CONTROL_PLANE_HARDWARE_VERSION:
# VSPHERE_WORKER_HARDWARE_VERSION:
VSPHERE_TLS_THUMBPRINT:
VSPHERE_INSECURE: "true"
VSPHERE_CONTROL_PLANE_ENDPOINT: 10.242.3.31
# VSPHERE_CONTROL_PLANE_ENDPOINT_PORT: 6443
# VSPHERE_ADDITIONAL_FQDN:
AVI_CONTROL_PLANE_HA_PROVIDER: false
 
#! ---------------------------------------------------------------------
#! NSX specific configuration for enabling NSX routable pods
#! ---------------------------------------------------------------------
 
# NSXT_POD_ROUTING_ENABLED: false
# NSXT_ROUTER_PATH: ""
# NSXT_USERNAME: ""
# NSXT_PASSWORD: ""
# NSXT_MANAGER_HOST: ""
# NSXT_ALLOW_UNVERIFIED_SSL: false
# NSXT_REMOTE_AUTH: false
# NSXT_VMC_ACCESS_TOKEN: ""
# NSXT_VMC_AUTH_HOST: ""
# NSXT_CLIENT_CERT_KEY_DATA: ""
# NSXT_CLIENT_CERT_DATA: ""
# NSXT_ROOT_CA_DATA: ""
# NSXT_SECRET_NAME: "cloud-provider-vsphere-nsxt-credentials"
# NSXT_SECRET_NAMESPACE: "kube-system"
 
#! ---------------------------------------------------------------------
#! Common configuration
#! ---------------------------------------------------------------------
 
# TKG_CUSTOM_IMAGE_REPOSITORY: ""
# TKG_CUSTOM_IMAGE_REPOSITORY_SKIP_TLS_VERIFY: false
# TKG_CUSTOM_IMAGE_REPOSITORY_CA_CERTIFICATE: ""
 
# TKG_HTTP_PROXY: ""
# TKG_HTTPS_PROXY: ""
# TKG_NO_PROXY: ""
# TKG_PROXY_CA_CERT: ""
 
ENABLE_AUDIT_LOGGING: false
ENABLE_DEFAULT_STORAGE_CLASS: true
 
CLUSTER_CIDR: 100.96.0.0/11
SERVICE_CIDR: 100.64.0.0/13
 
OS_NAME: "ubuntu"
OS_VERSION: "20.04"
OS_ARCH: amd64
 
#! ---------------------------------------------------------------------
#! Autoscaler configuration
#! ---------------------------------------------------------------------
 
ENABLE_AUTOSCALER: false
# AUTOSCALER_MAX_NODES_TOTAL: "0"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_ADD: "10m"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_DELETE: "10s"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_FAILURE: "3m"
# AUTOSCALER_SCALE_DOWN_UNNEEDED_TIME: "10m"
# AUTOSCALER_MAX_NODE_PROVISION_TIME: "15m"
# AUTOSCALER_MIN_SIZE_0:
# AUTOSCALER_MAX_SIZE_0:
# AUTOSCALER_MIN_SIZE_1:
# AUTOSCALER_MAX_SIZE_1:
# AUTOSCALER_MIN_SIZE_2:
# AUTOSCALER_MAX_SIZE_2:
 
#! ---------------------------------------------------------------------
#! Antrea CNI configuration
#! ---------------------------------------------------------------------
# ANTREA_NO_SNAT: false
# ANTREA_DISABLE_UDP_TUNNEL_OFFLOAD: false
# ANTREA_TRAFFIC_ENCAP_MODE: "encap"
# ANTREA_EGRESS_EXCEPT_CIDRS: ""
# ANTREA_NODEPORTLOCAL_ENABLED: true
# ANTREA_NODEPORTLOCAL_PORTRANGE: 61000-62000
# ANTREA_PROXY_ALL: false
# ANTREA_PROXY_NODEPORT_ADDRS: ""
# ANTREA_PROXY_SKIP_SERVICES: ""
# ANTREA_PROXY_LOAD_BALANCER_IPS: false
# ANTREA_FLOWEXPORTER_COLLECTOR_ADDRESS: "flow-aggregator.flow-aggregator.svc:4739:tls"
# ANTREA_FLOWEXPORTER_POLL_INTERVAL: "5s"
# ANTREA_FLOWEXPORTER_ACTIVE_TIMEOUT: "30s"
# ANTREA_FLOWEXPORTER_IDLE_TIMEOUT: "15s"
# ANTREA_KUBE_APISERVER_OVERRIDE:
# ANTREA_TRANSPORT_INTERFACE:
# ANTREA_TRANSPORT_INTERFACE_CIDRS: ""
# ANTREA_MULTICAST_INTERFACES: ""
# ANTREA_MULTICAST_IGMPQUERY_INTERVAL: "125s"
# ANTREA_TUNNEL_TYPE: geneve
# ANTREA_ENABLE_USAGE_REPORTING: false
# ANTREA_ENABLE_BRIDGING_MODE: false
# ANTREA_DISABLE_TXCHECKSUM_OFFLOAD: false
# ANTREA_DNS_SERVER_OVERRIDE: ""
# ANTREA_MULTICLUSTER_ENABLE: false
# ANTREA_MULTICLUSTER_NAMESPACE: ""
```



## Regular TKGm Workload Cluster bootstrapping (create/delete multiple node-pool)

**multiple node-pool**

```yaml
name: md-1
replicas: 2
labels:
  np2: true
vsphere:
  memoryMiB: 8192
  diskGiB: 64
  numCPUs: 4
  datacenter: /Datacenter
  datastore: /Datacenter/datastore/ds-local-222-03
#  storagePolicyName: name
  folder: /Datacenter/vm/folder-tkg
  resourcePool: /Datacenter/host/02-cluster-gpu/Resources/rp-workload-gpu-cluster
  vcIP: 10.252.12.99
  #template: templateName
  cloneMode: "fullClone"
  network: /Datacenter/network/pg-vlan2003-tkgm
  workerClass: tkg-worker
  tkrResolver: os-name=ubuntu,os-arch=amd64
```

**create new node-pool**

```shell
ubuntu@ubuntu-bootstapping-142:~$ tanzu cluster node-pool set workload-31 -f workload-gpu-np2-31.yaml --base-machine-deployment md-0
Cluster update for node pool 'md-1' completed successfully
ubuntu@ubuntu-bootstapping-142:~$ tanzu cluster list
  NAME         NAMESPACE  STATUS   CONTROLPLANE  WORKERS  KUBERNETES        ROLES   PLAN  TKR
  workload-31  default    running  1/1           3/3      v1.27.5+vmware.1  <none>  dev   v1.27.5---vmware.1-tkg.1
ubuntu@ubuntu-bootstapping-142:~$ tanzu cluster node-pool list workload-31
  NAME  NAMESPACE  PHASE    REPLICAS  READY  UPDATED  UNAVAILABLE
  md-0  default    Running  1         1      1        0
  md-1  default    Running  2         2      2        0
ubuntu@ubuntu-bootstapping-142:~$
```



**kubectl output**

```shell
capv@workload-31-s4fkx-wkltk:~$ sudo kubectl get node -o wide --kubeconfig=/etc/kubernetes/admin.conf
NAME                                            STATUS   ROLES           AGE   VERSION            INTERNAL-IP    EXTERNAL-IP    OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
workload-31-md-0-dl8wb-674d45b95x9dwd8-wmhhn    Ready    <none>          24m   v1.27.5+vmware.1   10.242.3.149   10.242.3.149   Ubuntu 20.04.6 LTS   5.4.0-162-generic   containerd://1.6.18-1-gdbc99e5b1
workload-31-md-1-sjp7c-857c45fc54xwh8b6-gcsrb   Ready    <none>          10m   v1.27.5+vmware.1   10.242.3.151   10.242.3.151   Ubuntu 20.04.6 LTS   5.4.0-162-generic   containerd://1.6.18-1-gdbc99e5b1
workload-31-md-1-sjp7c-857c45fc54xwh8b6-nx766   Ready    <none>          10m   v1.27.5+vmware.1   10.242.3.150   10.242.3.150   Ubuntu 20.04.6 LTS   5.4.0-162-generic   containerd://1.6.18-1-gdbc99e5b1
workload-31-s4fkx-wkltk                         Ready    control-plane   25m   v1.27.5+vmware.1   10.242.3.148   10.242.3.148   Ubuntu 20.04.6 LTS   5.4.0-162-generic   containerd://1.6.18-1-gdbc99e5b1
capv@workload-31-s4fkx-wkltk:~$
```



## GPU TKGm Workload Cluster bootstrapping (Single GPU node-pool)

**single GPU node-pool**

```shell
#! ---------------------------------------------------------------------
#! Basic cluster creation configuration
#! ---------------------------------------------------------------------
 
CLUSTER_NAME: workload-pci-33
CLUSTER_PLAN: dev
NAMESPACE: default
# CLUSTER_API_SERVER_PORT: # For deployments without NSX Advanced Load Balancer
CNI: antrea
 
#! ---------------------------------------------------------------------
#! Node configuration
#! ---------------------------------------------------------------------
 
# SIZE:
# CONTROLPLANE_SIZE:
# WORKER_SIZE:
 
# VSPHERE_NUM_CPUS: 2
# VSPHERE_DISK_GIB: 40
# VSPHERE_MEM_MIB: 4096
 
# VSPHERE_CONTROL_PLANE_NUM_CPUS: 2
# VSPHERE_CONTROL_PLANE_DISK_GIB: 40
# VSPHERE_CONTROL_PLANE_MEM_MIB: 8192
VSPHERE_WORKER_NUM_CPUS: 32
# VSPHERE_WORKER_DISK_GIB: 40
VSPHERE_WORKER_MEM_MIB: 65536
 
# CONTROL_PLANE_MACHINE_COUNT:
# WORKER_MACHINE_COUNT:
# WORKER_MACHINE_COUNT_0:
# WORKER_MACHINE_COUNT_1:
# WORKER_MACHINE_COUNT_2:
 
#! ---------------------------------------------------------------------
#! vSphere configuration
#! ---------------------------------------------------------------------
 
#VSPHERE_CLONE_MODE: "fullClone"
VSPHERE_NETWORK: /Datacenter/network/pg-vlan2003-tkgm
# VSPHERE_TEMPLATE:
# VSPHERE_TEMPLATE_MOID:
# IS_WINDOWS_WORKLOAD_CLUSTER: false
# VIP_NETWORK_INTERFACE: "eth0"
VSPHERE_SSH_AUTHORIZED_KEY: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2hFxSAbATgfpJeXx67tn12ux8B8aZ6DITdqsvM8pzXQeuK7Op4gxvNsTi+cr7gJFjipUtrSasB2eUSRRCN4lFW3PikKMVwp6bKyr/AkoQAoX3TNWubkb4hAfsMJkCtsrP/yzkMR+fGNbbBAv7iYCI2EIRlFrpj7FvwGmSrlIm7OPz0NjFh0QDE3oh6SnKxLFTMHW7kpjSjWXdL4uIbnXXnL5n3XvaA3vBminmN16o5KicR3aEcwZcQ6a3xhL5yx788WK8jp3tinSysIOuCV6pUfU/g9dl7kEfnUubUB2niPOb3BTaP8V/eMH5ONnmdz7izreNtvEuvYmtUByAE8upaQZZaw1IA3JR3JS2fOJSYPdV9IiEFC8Rsskbno9j3FEuYov0ZEFKavh0s3yOV3vxrmzjl8lXnMomGHSnCL6EDn1nvH3giC9LNwwxCkKl/6Z2C4mZENoqBzQMGNt4shLUfqBfWeFzFx8QzZJK7MSFr/L45OUgWMKdRweiwb7p0VH2BYIBjBadbPnLxwGvzQYUEATVZhrnX5fCqi+jJ9sEQfzKC3Bmm3sy+qsTLQTf3JmCGonW30IPmxzd8xP07gvtJF85/ANknDjCfE3KNcrbXaw4enSgcoq1j1NmSCTgobOhXltJEsrfgGDkgpon5W3JfNlhzvls+RuizZGOMtzLIw== email@example.com
VSPHERE_USERNAME: administrator@vsphere.local
VSPHERE_PASSWORD: <encoded:Vk13YXJlMSE=>
# VSPHERE_REGION:
# VSPHERE_ZONE:
# VSPHERE_AZ_0:
# VSPHERE_AZ_1:
# VSPHERE_AZ_2:
# VSPHERE_AZ_CONTROL_PLANE_MATCHING_LABELS:
VSPHERE_SERVER: 10.252.12.99
VSPHERE_DATACENTER: /Datacenter
VSPHERE_RESOURCE_POOL: /Datacenter/host/02-cluster-gpu/Resources/rp-workload-gpu-cluster
VSPHERE_DATASTORE: /Datacenter/datastore/ds-local-222-03
VSPHERE_FOLDER: /Datacenter/vm/folder-tkg
# VSPHERE_MTU:
# VSPHERE_STORAGE_POLICY_ID
VSPHERE_WORKER_PCI_DEVICES: "0x10DE:0x1EB8"
# VSPHERE_CONTROL_PLANE_PCI_DEVICES:
VSPHERE_IGNORE_PCI_DEVICES_ALLOW_LIST: false
# VSPHERE_CONTROL_PLANE_CUSTOM_VMX_KEYS:
VSPHERE_WORKER_CUSTOM_VMX_KEYS: 'pciPassthru.allowP2P=true,pciPassthru.RelaxACSforP2P=true,pciPassthru.use64bitMMIO=true,pciPassthru.64bitMMIOSizeGB=32'
WORKER_ROLLOUT_STRATEGY: "OnDelete"
# VSPHERE_CONTROL_PLANE_HARDWARE_VERSION:
VSPHERE_WORKER_HARDWARE_VERSION: vmx-17
VSPHERE_TLS_THUMBPRINT:
VSPHERE_INSECURE: "true"
VSPHERE_CONTROL_PLANE_ENDPOINT: 10.242.3.33
# VSPHERE_CONTROL_PLANE_ENDPOINT_PORT: 6443
# VSPHERE_ADDITIONAL_FQDN:
AVI_CONTROL_PLANE_HA_PROVIDER: false
 
#! ---------------------------------------------------------------------
#! NSX specific configuration for enabling NSX routable pods
#! ---------------------------------------------------------------------
 
# NSXT_POD_ROUTING_ENABLED: false
# NSXT_ROUTER_PATH: ""
# NSXT_USERNAME: ""
# NSXT_PASSWORD: ""
# NSXT_MANAGER_HOST: ""
# NSXT_ALLOW_UNVERIFIED_SSL: false
# NSXT_REMOTE_AUTH: false
# NSXT_VMC_ACCESS_TOKEN: ""
# NSXT_VMC_AUTH_HOST: ""
# NSXT_CLIENT_CERT_KEY_DATA: ""
# NSXT_CLIENT_CERT_DATA: ""
# NSXT_ROOT_CA_DATA: ""
# NSXT_SECRET_NAME: "cloud-provider-vsphere-nsxt-credentials"
# NSXT_SECRET_NAMESPACE: "kube-system"
 
#! ---------------------------------------------------------------------
#! Common configuration
#! ---------------------------------------------------------------------
 
# TKG_CUSTOM_IMAGE_REPOSITORY: ""
# TKG_CUSTOM_IMAGE_REPOSITORY_SKIP_TLS_VERIFY: false
# TKG_CUSTOM_IMAGE_REPOSITORY_CA_CERTIFICATE: ""
 
# TKG_HTTP_PROXY: ""
# TKG_HTTPS_PROXY: ""
# TKG_NO_PROXY: ""
# TKG_PROXY_CA_CERT: ""
 
ENABLE_AUDIT_LOGGING: false
ENABLE_DEFAULT_STORAGE_CLASS: true
 
CLUSTER_CIDR: 100.96.0.0/11
SERVICE_CIDR: 100.64.0.0/13
 
OS_NAME: "ubuntu"
OS_VERSION: "20.04"
OS_ARCH: amd64
 
#! ---------------------------------------------------------------------
#! Autoscaler configuration
#! ---------------------------------------------------------------------
 
ENABLE_AUTOSCALER: false
# AUTOSCALER_MAX_NODES_TOTAL: "0"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_ADD: "10m"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_DELETE: "10s"
# AUTOSCALER_SCALE_DOWN_DELAY_AFTER_FAILURE: "3m"
# AUTOSCALER_SCALE_DOWN_UNNEEDED_TIME: "10m"
# AUTOSCALER_MAX_NODE_PROVISION_TIME: "15m"
# AUTOSCALER_MIN_SIZE_0:
# AUTOSCALER_MAX_SIZE_0:
# AUTOSCALER_MIN_SIZE_1:
# AUTOSCALER_MAX_SIZE_1:
# AUTOSCALER_MIN_SIZE_2:
# AUTOSCALER_MAX_SIZE_2:
 
#! ---------------------------------------------------------------------
#! Antrea CNI configuration
#! ---------------------------------------------------------------------
# ANTREA_NO_SNAT: false
# ANTREA_DISABLE_UDP_TUNNEL_OFFLOAD: false
# ANTREA_TRAFFIC_ENCAP_MODE: "encap"
# ANTREA_EGRESS_EXCEPT_CIDRS: ""
# ANTREA_NODEPORTLOCAL_ENABLED: true
# ANTREA_NODEPORTLOCAL_PORTRANGE: 61000-62000
# ANTREA_PROXY_ALL: false
# ANTREA_PROXY_NODEPORT_ADDRS: ""
# ANTREA_PROXY_SKIP_SERVICES: ""
# ANTREA_PROXY_LOAD_BALANCER_IPS: false
# ANTREA_FLOWEXPORTER_COLLECTOR_ADDRESS: "flow-aggregator.flow-aggregator.svc:4739:tls"
# ANTREA_FLOWEXPORTER_POLL_INTERVAL: "5s"
# ANTREA_FLOWEXPORTER_ACTIVE_TIMEOUT: "30s"
# ANTREA_FLOWEXPORTER_IDLE_TIMEOUT: "15s"
# ANTREA_KUBE_APISERVER_OVERRIDE:
# ANTREA_TRANSPORT_INTERFACE:
# ANTREA_TRANSPORT_INTERFACE_CIDRS: ""
# ANTREA_MULTICAST_INTERFACES: ""
# ANTREA_MULTICAST_IGMPQUERY_INTERVAL: "125s"
# ANTREA_TUNNEL_TYPE: geneve
# ANTREA_ENABLE_USAGE_REPORTING: false
# ANTREA_ENABLE_BRIDGING_MODE: false
# ANTREA_DISABLE_TXCHECKSUM_OFFLOAD: false
# ANTREA_DNS_SERVER_OVERRIDE: ""
# ANTREA_MULTICLUSTER_ENABLE: false
# ANTREA_MULTICLUSTER_NAMESPACE: ""
```

## GPU TKGm Workload Cluster bootstrapping (Multiple GPU node-pool)

## GPU TKGm Workload Cluster bootstrapping (Hybrid node-pool, for example one GPU node-pool, and one non-GPU node-pool)

This is not supported from config file on TKG2.4. User could created regular non-GPU node-pool and add GPU passthrough manually.

1. create node-pool
2. power off VM, and upgrade compatibility to VMX-17 or higher
3. add GPU PCI passthrough to the VM 
4. power on the VM and install the GPU driver
5. install nvidia GPU-Operator (follow the CLI on docs.vmware.com)
6. reboot VM



# Non-official process

## Regular TKGm Workload Cluster bootstrapping (Single node-pool)

**single node pool**

```yaml
apiVersion: cpi.tanzu.vmware.com/v1alpha1
kind: VSphereCPIConfig
metadata:
  name: workload-pci-34
  namespace: default
spec:
  vsphereCPI:
    mode: vsphereCPI
    tlsCipherSuites: TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305,TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    vmNetwork:
      excludeExternalSubnetCidr: 10.242.3.33/32
      excludeInternalSubnetCidr: 10.242.3.33/32
---
apiVersion: csi.tanzu.vmware.com/v1alpha1
kind: VSphereCSIConfig
metadata:
  name: workload-pci-34
  namespace: default
spec:
  vsphereCSI:
    config:
      datacenter: /Datacenter
      httpProxy: ""
      httpsProxy: ""
      insecureFlag: true
      noProxy: ""
      region: null
      tlsThumbprint: ""
      useTopologyCategories: false
      zone: null
    mode: vsphereCSI
---
apiVersion: run.tanzu.vmware.com/v1alpha3
kind: ClusterBootstrap
metadata:
  annotations:
    tkg.tanzu.vmware.com/add-missing-fields-from-tkr: v1.27.5---vmware.1-tkg.1
  name: workload-pci-34
  namespace: default
spec:
  additionalPackages:
  - refName: metrics-server*
  - refName: secretgen-controller*
  - refName: pinniped*
  cpi:
    refName: vsphere-cpi*
    valuesFrom:
      providerRef:
        apiGroup: cpi.tanzu.vmware.com
        kind: VSphereCPIConfig
        name: workload-pci-34
  csi:
    refName: vsphere-csi*
    valuesFrom:
      providerRef:
        apiGroup: csi.tanzu.vmware.com
        kind: VSphereCSIConfig
        name: workload-pci-34
  kapp:
    refName: kapp-controller*
---
apiVersion: v1
kind: Secret
metadata:
  name: workload-pci-34
  namespace: default
stringData:
  password: VMware1!
  username: administrator@vsphere.local
---
apiVersion: cluster.x-k8s.io/v1beta1
kind: Cluster
metadata:
  annotations:
    osInfo: ubuntu,20.04,amd64
    tkg.tanzu.vmware.com/cluster-controlplane-endpoint: 10.242.3.33
    tkg/plan: dev
  labels:
    tkg.tanzu.vmware.com/cluster-name: workload-pci-34
  name: workload-pci-34
  namespace: default
spec:
  clusterNetwork:
    pods:
      cidrBlocks:
      - 100.96.0.0/11
    services:
      cidrBlocks:
      - 100.64.0.0/13
  topology:
    class: tkg-vsphere-default-v1.1.1
    controlPlane:
      metadata:
        annotations:
          run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
      replicas: 1
    variables:
    - name: cni
      value: antrea
    - name: controlPlaneCertificateRotation
      value:
        activate: true
        daysBefore: 90
    - name: auditLogging
      value:
        enabled: false
    - name: podSecurityStandard
      value:
        audit: restricted
        deactivated: false
        warn: restricted
    - name: apiServerEndpoint
      value: 10.242.3.34
    - name: aviAPIServerHAProvider
      value: false
    - name: vcenter
      value:
        cloneMode: fullClone
        datacenter: /Datacenter
        datastore: /Datacenter/datastore/ds-local-222-03
        folder: /Datacenter/vm/folder-tkg
        network: /Datacenter/network/pg-vlan2003-tkgm
        resourcePool: /Datacenter/host/02-cluster-gpu/Resources/rp-workload-gpu-cluster
        server: 10.252.12.99
        storagePolicyID: ""
        tlsThumbprint: ""
    - name: user
      value:
        sshAuthorizedKeys:
        - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2hFxSAbATgfpJeXx67tn12ux8B8aZ6DITdqsvM8pzXQeuK7Op4gxvNsTi+cr7gJFjipUtrSasB2eUSRRCN4lFW3PikKMVwp6bKyr/AkoQAoX3TNWubkb4hAfsMJkCtsrP/yzkMR+fGNbbBAv7iYCI2EIRlFrpj7FvwGmSrlIm7OPz0NjFh0QDE3oh6SnKxLFTMHW7kpjSjWXdL4uIbnXXnL5n3XvaA3vBminmN16o5KicR3aEcwZcQ6a3xhL5yx788WK8jp3tinSysIOuCV6pUfU/g9dl7kEfnUubUB2niPOb3BTaP8V/eMH5ONnmdz7izreNtvEuvYmtUByAE8upaQZZaw1IA3JR3JS2fOJSYPdV9IiEFC8Rsskbno9j3FEuYov0ZEFKavh0s3yOV3vxrmzjl8lXnMomGHSnCL6EDn1nvH3giC9LNwwxCkKl/6Z2C4mZENoqBzQMGNt4shLUfqBfWeFzFx8QzZJK7MSFr/L45OUgWMKdRweiwb7p0VH2BYIBjBadbPnLxwGvzQYUEATVZhrnX5fCqi+jJ9sEQfzKC3Bmm3sy+qsTLQTf3JmCGonW30IPmxzd8xP07gvtJF85/ANknDjCfE3KNcrbXaw4enSgcoq1j1NmSCTgobOhXltJEsrfgGDkgpon5W3JfNlhzvls+RuizZGOMtzLIw==
    - name: controlPlane
      value:
        machine:
          diskGiB: 40
          memoryMiB: 8192
          numCPUs: 2
    - name: worker
      value:
        machine:
          diskGiB: 40
          memoryMiB: 32768
          numCPUs: 16
    - name: security
      value:
        fileIntegrityMonitoring:
          enabled: false
        imagePolicy:
          pullAlways: false
          webhook:
            enabled: false
            spec:
              allowTTL: 50
              defaultAllow: true
              denyTTL: 60
              retryBackoff: 500
        kubeletOptions:
          eventQPS: 50
          streamConnectionIdleTimeout: 4h0m0s
        systemCryptoPolicy: default
    version: v1.27.5+vmware.1-tkg.1
    workers:
      machineDeployments:
      - class: tkg-worker
        metadata:
          annotations:
            run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
        name: md-0
        replicas: 2
        strategy:
          type: OnDelete
```

## Regular TKGm Workload Cluster bootstrapping (multiple node-pool)

**multiple node-pool no GPU**

```yaml
apiVersion: cpi.tanzu.vmware.com/v1alpha1
kind: VSphereCPIConfig
metadata:
  name: workload-pci-33
  namespace: default
spec:
  vsphereCPI:
    mode: vsphereCPI
    tlsCipherSuites: TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305,TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    vmNetwork:
      excludeExternalSubnetCidr: 10.242.3.33/32
      excludeInternalSubnetCidr: 10.242.3.33/32
---
apiVersion: csi.tanzu.vmware.com/v1alpha1
kind: VSphereCSIConfig
metadata:
  name: workload-pci-33
  namespace: default
spec:
  vsphereCSI:
    config:
      datacenter: /Datacenter
      httpProxy: ""
      httpsProxy: ""
      insecureFlag: true
      noProxy: ""
      region: null
      tlsThumbprint: ""
      useTopologyCategories: false
      zone: null
    mode: vsphereCSI
---
apiVersion: run.tanzu.vmware.com/v1alpha3
kind: ClusterBootstrap
metadata:
  annotations:
    tkg.tanzu.vmware.com/add-missing-fields-from-tkr: v1.27.5---vmware.1-tkg.1
  name: workload-pci-33
  namespace: default
spec:
  additionalPackages:
  - refName: metrics-server*
  - refName: secretgen-controller*
  - refName: pinniped*
  cpi:
    refName: vsphere-cpi*
    valuesFrom:
      providerRef:
        apiGroup: cpi.tanzu.vmware.com
        kind: VSphereCPIConfig
        name: workload-pci-33
  csi:
    refName: vsphere-csi*
    valuesFrom:
      providerRef:
        apiGroup: csi.tanzu.vmware.com
        kind: VSphereCSIConfig
        name: workload-pci-33
  kapp:
    refName: kapp-controller*
---
apiVersion: v1
kind: Secret
metadata:
  name: workload-pci-33
  namespace: default
stringData:
  password: VMware1!
  username: administrator@vsphere.local
---
apiVersion: cluster.x-k8s.io/v1beta1
kind: Cluster
metadata:
  annotations:
    osInfo: ubuntu,20.04,amd64
    tkg.tanzu.vmware.com/cluster-controlplane-endpoint: 10.242.3.33
    tkg/plan: dev
  labels:
    tkg.tanzu.vmware.com/cluster-name: workload-pci-33
  name: workload-pci-33
  namespace: default
spec:
  clusterNetwork:
    pods:
      cidrBlocks:
      - 100.96.0.0/11
    services:
      cidrBlocks:
      - 100.64.0.0/13
  topology:
    class: tkg-vsphere-default-v1.1.1
    controlPlane:
      metadata:
        annotations:
          run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
      replicas: 1
    variables:
    - name: cni
      value: antrea
    - name: controlPlaneCertificateRotation
      value:
        activate: true
        daysBefore: 90
    - name: auditLogging
      value:
        enabled: false
    - name: podSecurityStandard
      value:
        audit: restricted
        deactivated: false
        warn: restricted
    - name: apiServerEndpoint
      value: 10.242.3.33
    - name: aviAPIServerHAProvider
      value: false
    - name: vcenter
      value:
        cloneMode: fullClone
        datacenter: /Datacenter
        datastore: /Datacenter/datastore/ds-local-222-03
        folder: /Datacenter/vm/folder-tkg
        network: /Datacenter/network/pg-vlan2003-tkgm
        resourcePool: /Datacenter/host/02-cluster-gpu/Resources/rp-workload-gpu-cluster
        server: 10.252.12.99
        storagePolicyID: ""
        tlsThumbprint: ""
    - name: user
      value:
        sshAuthorizedKeys:
        - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2hFxSAbATgfpJeXx67tn12ux8B8aZ6DITdqsvM8pzXQeuK7Op4gxvNsTi+cr7gJFjipUtrSasB2eUSRRCN4lFW3PikKMVwp6bKyr/AkoQAoX3TNWubkb4hAfsMJkCtsrP/yzkMR+fGNbbBAv7iYCI2EIRlFrpj7FvwGmSrlIm7OPz0NjFh0QDE3oh6SnKxLFTMHW7kpjSjWXdL4uIbnXXnL5n3XvaA3vBminmN16o5KicR3aEcwZcQ6a3xhL5yx788WK8jp3tinSysIOuCV6pUfU/g9dl7kEfnUubUB2niPOb3BTaP8V/eMH5ONnmdz7izreNtvEuvYmtUByAE8upaQZZaw1IA3JR3JS2fOJSYPdV9IiEFC8Rsskbno9j3FEuYov0ZEFKavh0s3yOV3vxrmzjl8lXnMomGHSnCL6EDn1nvH3giC9LNwwxCkKl/6Z2C4mZENoqBzQMGNt4shLUfqBfWeFzFx8QzZJK7MSFr/L45OUgWMKdRweiwb7p0VH2BYIBjBadbPnLxwGvzQYUEATVZhrnX5fCqi+jJ9sEQfzKC3Bmm3sy+qsTLQTf3JmCGonW30IPmxzd8xP07gvtJF85/ANknDjCfE3KNcrbXaw4enSgcoq1j1NmSCTgobOhXltJEsrfgGDkgpon5W3JfNlhzvls+RuizZGOMtzLIw==
    - name: controlPlane
      value:
        machine:
          diskGiB: 40
          memoryMiB: 8192
          numCPUs: 2
    - name: worker
      value:
        machine:
          diskGiB: 40
          memoryMiB: 65536
          numCPUs: 32
    - name: security
      value:
        fileIntegrityMonitoring:
          enabled: false
        imagePolicy:
          pullAlways: false
          webhook:
            enabled: false
            spec:
              allowTTL: 50
              defaultAllow: true
              denyTTL: 60
              retryBackoff: 500
        kubeletOptions:
          eventQPS: 50
          streamConnectionIdleTimeout: 4h0m0s
        systemCryptoPolicy: default
    version: v1.27.5+vmware.1-tkg.1
    workers:
      machineDeployments:
      - class: tkg-worker
        metadata:
          annotations:
            run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
        name: md-0
        replicas: 1
        strategy:
          type: OnDelete
      - class: tkg-worker
        metadata:
          annotations:
            run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
        name: md-1
        replicas: 1
        strategy:
          type: OnDelete
        variables:
          overrides:
          - name: worker
            value:
              machine:
                diskGiB: 300
                memoryMiB: 32768
                numCPUs: 16
```

**tanzu output**

```shell
ubuntu@ubuntu-bootstapping-142:~$ tanzu cluster get workload-pci-33 --show-details
  NAME             NAMESPACE  STATUS   CONTROLPLANE  WORKERS  KUBERNETES        ROLES   TKR
  workload-pci-33  default    running  1/1           2/2      v1.27.5+vmware.1  <none>  v1.27.5---vmware.1-tkg.1
 
 
Details:
 
NAME                                                                                    READY  SEVERITY  REASON  SINCE  MESSAGE
/workload-pci-33                                                                        True                     2m51s
├─ClusterInfrastructure - VSphereCluster/workload-pci-33-wgfkm                          True                     4m25s
├─ControlPlane - KubeadmControlPlane/workload-pci-33-2fdsf                              True                     2m51s
│ └─Machine/workload-pci-33-2fdsf-wpw52                                                 True                     2m52s
│   ├─BootstrapConfig - KubeadmConfig/workload-pci-33-2fdsf-xn9wc                       True                     4m24s
│   └─MachineInfrastructure - VSphereMachine/workload-pci-33-control-plane-scqzc-vjmjl  True                     2m52s
└─Workers
  ├─MachineDeployment/workload-pci-33-md-0-jgqqq                                        True                     31s
  │ └─Machine/workload-pci-33-md-0-jgqqq-5b6b7c8b89xgqflg-lf6sz                         True                     32s
  │   ├─BootstrapConfig - KubeadmConfig/workload-pci-33-md-0-bootstrap-4p275-qtsld      True                     2m55s
  │   └─MachineInfrastructure - VSphereMachine/workload-pci-33-md-0-infra-sbddj-qrjtn   True                     32s
  └─MachineDeployment/workload-pci-33-md-1-8fd7d                                        True                     30s
    └─Machine/workload-pci-33-md-1-8fd7d-5565c46668x6c6wp-pjfd5                         True                     32s
      ├─BootstrapConfig - KubeadmConfig/workload-pci-33-md-1-bootstrap-xq6zg-q5qg9      True                     2m55s
      └─MachineInfrastructure - VSphereMachine/workload-pci-33-md-1-infra-wqrcw-2hssx   True                     32s
ubuntu@ubuntu-bootstapping-142:~$
ubuntu@ubuntu-bootstapping-142:~$
ubuntu@ubuntu-bootstapping-142:~$ tanzu cluster node-pool list workload-pci-33
  NAME  NAMESPACE  PHASE    REPLICAS  READY  UPDATED  UNAVAILABLE
  md-0  default    Running  1         1      1        0
  md-1  default    Running  1         1      1        0
ubuntu@ubuntu-bootstapping-142:~$
```



## GPU TKGm Workload Cluster bootstrapping (Single GPU node-pool)

**GPU single node pool**

```yaml
apiVersion: run.tanzu.vmware.com/v1alpha3
kind: ClusterBootstrap
metadata:
  annotations:
    tkg.tanzu.vmware.com/add-missing-fields-from-tkr: v1.27.5---vmware.1-tkg.1
  name: workload-pci-33
  namespace: default
spec:
  additionalPackages:
  - refName: metrics-server*
  - refName: secretgen-controller*
  - refName: pinniped*
  cpi:
    refName: vsphere-cpi*
    valuesFrom:
      providerRef:
        apiGroup: cpi.tanzu.vmware.com
        kind: VSphereCPIConfig
        name: workload-pci-33
  csi:
    refName: vsphere-csi*
    valuesFrom:
      providerRef:
        apiGroup: csi.tanzu.vmware.com
        kind: VSphereCSIConfig
        name: workload-pci-33
  kapp:
    refName: kapp-controller*
---
apiVersion: v1
kind: Secret
metadata:
  name: workload-pci-33
  namespace: default
stringData:
  password: VMware1!
  username: administrator@vsphere.local
---
apiVersion: cluster.x-k8s.io/v1beta1
kind: Cluster
metadata:
  annotations:
    osInfo: ubuntu,20.04,amd64
    tkg.tanzu.vmware.com/cluster-controlplane-endpoint: 10.242.3.33
    tkg/plan: dev
  labels:
    tkg.tanzu.vmware.com/cluster-name: workload-pci-33
  name: workload-pci-33
  namespace: default
spec:
  clusterNetwork:
    pods:
      cidrBlocks:
      - 100.96.0.0/11
    services:
      cidrBlocks:
      - 100.64.0.0/13
  topology:
    class: tkg-vsphere-default-v1.1.1
    controlPlane:
      metadata:
        annotations:
          run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
      replicas: 1
    variables:
    - name: cni
      value: antrea
    - name: controlPlaneCertificateRotation
      value:
        activate: true
        daysBefore: 90
    - name: auditLogging
      value:
        enabled: false
    - name: podSecurityStandard
      value:
        audit: restricted
        deactivated: false
        warn: restricted
    - name: apiServerEndpoint
      value: 10.242.3.33
    - name: aviAPIServerHAProvider
      value: false
    - name: vcenter
      value:
        cloneMode: fullClone
        datacenter: /Datacenter
        datastore: /Datacenter/datastore/ds-local-222-03
        folder: /Datacenter/vm/folder-tkg
        network: /Datacenter/network/pg-vlan2003-tkgm
        resourcePool: /Datacenter/host/02-cluster-gpu/Resources/rp-workload-gpu-cluster
        server: 10.252.12.99
        storagePolicyID: ""
        tlsThumbprint: ""
    - name: user
      value:
        sshAuthorizedKeys:
        - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC2hFxSAbATgfpJeXx67tn12ux8B8aZ6DITdqsvM8pzXQeuK7Op4gxvNsTi+cr7gJFjipUtrSasB2eUSRRCN4lFW3PikKMVwp6bKyr/AkoQAoX3TNWubkb4hAfsMJkCtsrP/yzkMR+fGNbbBAv7iYCI2EIRlFrpj7FvwGmSrlIm7OPz0NjFh0QDE3oh6SnKxLFTMHW7kpjSjWXdL4uIbnXXnL5n3XvaA3vBminmN16o5KicR3aEcwZcQ6a3xhL5yx788WK8jp3tinSysIOuCV6pUfU/g9dl7kEfnUubUB2niPOb3BTaP8V/eMH5ONnmdz7izreNtvEuvYmtUByAE8upaQZZaw1IA3JR3JS2fOJSYPdV9IiEFC8Rsskbno9j3FEuYov0ZEFKavh0s3yOV3vxrmzjl8lXnMomGHSnCL6EDn1nvH3giC9LNwwxCkKl/6Z2C4mZENoqBzQMGNt4shLUfqBfWeFzFx8QzZJK7MSFr/L45OUgWMKdRweiwb7p0VH2BYIBjBadbPnLxwGvzQYUEATVZhrnX5fCqi+jJ9sEQfzKC3Bmm3sy+qsTLQTf3JmCGonW30IPmxzd8xP07gvtJF85/ANknDjCfE3KNcrbXaw4enSgcoq1j1NmSCTgobOhXltJEsrfgGDkgpon5W3JfNlhzvls+RuizZGOMtzLIw==
    - name: controlPlane
      value:
        machine:
          diskGiB: 40
          memoryMiB: 8192
          numCPUs: 2
    - name: worker
      value:
        machine:
          customVMXKeys:
            pciPassthru.64bitMMIOSizeGB: "32"
            pciPassthru.RelaxACSforP2P: "true"
            pciPassthru.allowP2P: "true"
            pciPassthru.use64bitMMIO: "true"
          diskGiB: 40
          memoryMiB: 65536
          numCPUs: 32
    - name: pci
      value:
        worker:
          devices:
          - deviceId: 7864
            vendorId: 4318
          hardwareVersion: vmx-17
    - name: security
      value:
        fileIntegrityMonitoring:
          enabled: false
        imagePolicy:
          pullAlways: false
          webhook:
            enabled: false
            spec:
              allowTTL: 50
              defaultAllow: true
              denyTTL: 60
              retryBackoff: 500
        kubeletOptions:
          eventQPS: 50
          streamConnectionIdleTimeout: 4h0m0s
        systemCryptoPolicy: default
    version: v1.27.5+vmware.1-tkg.1
    workers:
      machineDeployments:
      - class: tkg-worker
        metadata:
          annotations:
            run.tanzu.vmware.com/resolve-os-image: image-type=ova,os-name=ubuntu
        name: md-0
        replicas: 1
        strategy:
          type: OnDelete
```



## GPU TKGm Workload Cluster bootstrapping (Multiple GPU node-pool)



## GPU TKGm Workload Cluster bootstrapping (Hybrid node-pool, for example one GPU node-pool, and one non-GPU node-pool)

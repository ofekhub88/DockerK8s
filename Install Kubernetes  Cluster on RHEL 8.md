### ( If you need to go through a poxy , run the follwong )

```bash
export HTTP_PROXY=<your proxy url with port >
export HTTPS_PROXY=$HTTP_PROXY
export http_proxy=$HTTP_PROXY
export https_proxy=$HTTP_PROXY
export NO_PROXY=localhost,hostname1,2...
export no_proxy=$NO_PROXY
```



``` bash
$ sudo swapoff -a

$ sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

$ sudo dnf install -y iproute-tc

```

## On master Node 

```bash
$ sudo firewall-cmd --permanent --add-port=6443/tcp
$ sudo firewall-cmd --permanent --add-port=2379-2380/tcp
$ sudo firewall-cmd --permanent --add-port=10250/tcp
$ sudo firewall-cmd --permanent --add-port=10251/tcp
$ sudo firewall-cmd --permanent --add-port=10252/tcp
$ sudo firewall-cmd --reload
```

## On Worker Node 
```bash
$ sudo firewall-cmd --permanent --add-port=10250/tcp
$ sudo firewall-cmd --permanent --add-port=30000-32767/tcp                                                 
$ sudo firewall-cmd --reload

```
## Install CRI-O container runtime
```bash
$sudo vi /etc/modules-load.d/k8s.conf 
#add
#====
overlay
br_netfilter
#=====

$ sudo modprobe overlay
$ sudo modprobe br_netfilter
$ sudo vi /etc/sysctl.d/k8s.conf
#add the following lines 
#=======
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.bridge.bridge-nf-call-ip6tables = 1
#=======
$sudo sysctl --system
```
### if  file /proc/sys/net/ipv4/ip_forward still contains a 0 value  run the below commands
```bash
$  sysctl -w net.ipv4.ip_forward=1
 $ echo 1 > /proc/sys/net/ipv4/ip_forward
```  
### To install CRI-O, set the $VERSION environment variable to match your CRI-O version. For instance, to install CRI-O version 1.21 set the $VERSION as shown:
```bash 
$ export VERSION=1.21
and run the folwoing ,
$ sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/CentOS_8/devel:kubic:libcontainers:stable.repo

$ sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$VERSION/CentOS_8/devel:kubic:libcontainers:stable:cri-o:$VERSION.repo
  
$ sudo dnf install cri-o 
$ sudo systemctl enable cri-o
$ sudo systemctl start cri-o
```


## Install Kubernetes Packages
```bash
$sudo vi /etc/yum.repos.d/kubernetes.repo
#======
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
#=========
$sudo dnf install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

$ sudo systemctl enable kubelet
$ sudo systemctl start kubelet
```

```
### configure the procy for Cri
```bash 
$ vi /etc/systemd/system/crio.service.d/10-default-env.conf
$  mkdir  /etc/systemd/system/crio.service.d
# add the folwoing lines 
#===========

[Service]
Environment="HTTP_PROXY=< your Proxu>"
Environment="HTTPS_PROXY=< your Proxu>"
Environment="NO_PROXY=<Your hostes list with comma separte "
#=====================
$systemctl status  cri-o
$systemctl restart  cri-o
$systemctl status  cri-o




$ mkdir -p /etc/systemd/system/kubelet.service.d/
$ echo "[Service]" >> /etc/systemd/system/kubelet.service.d/proxy.conf
$ echo "Environment=\"HTTP_PROXY=<Your proxy URL> \"" >> /etc/systemd/system/kubelet.service.d/proxy.conf
$ echo "Environment=\"HTTPS_PROXY=<Your proxy URL>"" >> /etc/systemd/system/kubelet.service.d/proxy.conf
$ echo "Environment=\"NO_PROXY=<Your Hosts name with comma sprated  \"" >> /etc/systemd/system/kubelet.service.d/proxy.conf

$ systemctl daemon-reload
$ systemctl restart kubelet

```
## Create Cluster
```bash
$sudo kubeadm init 

$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

```
## install Clalico CNI 
```batch
$ kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
$ kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```


## Configure User Exp
```bach

$sudo kubectl completion bash >/etc/bash_completion.d/kubectl
$sudo chmod 755 /etc/bash_completion.d/kubectl
#For each user you that run teh kubectl you can add 
$ echo 'alias k=kubectl' >>~/.bashrc
$ echo 'complete -F __start_kubectl k' >>~/.bashrc
```

## Install teh dashbord 
```bach

instruction are in https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

```

## Configure the Dashbord to run on node port 30444
```yaml
# Create Yaml file
---
kind: Service
apiVersion: v1
metadata:
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kubernetes-dashboard
spec:
  #ports:
  #  - port: 443
  #    targetPort: 8443
  type: NodePort
  ports:
  - nodePort: 30444
    port: 8888
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
# Then run the yamnl file

 $ kubectl apply -f dashsvc.yaml
```
### to let your master node to run pods of dashbord for exmaple run teh tain node command 
```bach
kubectl taint nodes --all node-role.kubernetes.io/<node name master for exmaple>-
```
### to get the login dashbord toekn run teh command
```bach
$ kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
#after dashbord is ready you can access it 
#https://`hostname`:30444
```

### install metric server
```bach
 kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
 ```

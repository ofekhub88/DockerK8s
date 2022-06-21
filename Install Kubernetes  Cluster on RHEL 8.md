``` bash
sudo swapoff -a

sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

sudo dnf install -y iproute-tc

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
sudo vi /etc/modules-load.d/k8s.conf 
#add
#====
overlay
br_netfilter
#=====

$ sudo modprobe overlay
$ sudo modprobe br_netfilter
$ sudo vi /etc/sysctl.d/k8s.conf
#add the following lines 

net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.bridge.bridge-nf-call-ip6tables = 1
sudo sysctl --system
```
# if  file /proc/sys/net/ipv4/ip_forward still contains a 0 value 
  sysctl -w net.ipv4.ip_forward=1
  echo 1 > /proc/sys/net/ipv4/ip_forward
  
  # To install CRI-O, set the $VERSION environment variable to match your CRI-O version. For instance, to install CRI-O version 1.21 set the $VERSION as shown:

$ export VERSION=1.21
  
  # ביםםדק איק VERSION 
  
  

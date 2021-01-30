---
description: Get started
---

# Kubernetes

## Kubernetes Local

## Deploy 4 server cluster

* 2 ubuntu
* 2 centos

### Mini\_kube

[https://kubernetes.io/docs/tasks/tools/install-minikube/](https://kubernetes.io/docs/tasks/tools/install-minikube/)

## UBUNTU

* Download ubuntu server - [link](https://ubuntu.com/download/server)
* set static ip's, set uname & password, set disk

  > \[!NOTE\] Unlike centos default diskpartition puts all storage in `/` and takes 500mb for `/boot/efi` and not sure whether we can have a user named root even possible, it is good to give an option to set a different admin user

> Also has option to deploy kubernetes, docker, ....\(awscli, gcp cli\) during boot.

### Personal opinion

* has both `curl` and `wget` by default
* has option to install docker during boot - no fuss about installation
* 
### Customisations

```text
sudo groupadd docker
sudo gpasswd -a $USER docker || sudo usermod -a -G docker $USER
```

> \[!NOTE\] possible reboot `sudo reboot now` [https://ostechnix.com/run-particular-commands-without-sudo-password-linux/](https://ostechnix.com/run-particular-commands-without-sudo-password-linux/) [https://dev.to/nabbisen/docker-without-sudo-34ci](https://dev.to/nabbisen/docker-without-sudo-34ci)

### Install kubernetes

```text
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt install kubeadm kubelet kubectl kubernetes-cni
```

> \[!Warn\] Need to turn off swap memory - [https://serverfault.com/questions/881517/why-disable-swap-on-kubernetes](https://serverfault.com/questions/881517/why-disable-swap-on-kubernetes)

```text
sudo swapoff -a
# comment out /swapfile
```

[https://phoenixnap.com/kb/install-kubernetes-on-ubuntu](https://phoenixnap.com/kb/install-kubernetes-on-ubuntu) [https://linuxconfig.org/how-to-install-kubernetes-on-ubuntu-20-04-focal-fossa-linux](https://linuxconfig.org/how-to-install-kubernetes-on-ubuntu-20-04-focal-fossa-linux)


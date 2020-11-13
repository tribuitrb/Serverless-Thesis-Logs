
```
sudo su -

apt-get update && sudo apt-get install -y apt-transport-https

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

apt-get update

apt-get install -y kubelet kubeadm kubectl

apt-mark hold kubelet kubeadm kubectl

swapoff -a
```

# Logs

```
root@worker1:~# apt-get update && sudo apt-get install -y apt-transport-https
Hit:1 https://download.docker.com/linux/ubuntu focal InRelease
Hit:2 http://vn.archive.ubuntu.com/ubuntu focal InRelease
Hit:3 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:4 http://vn.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:5 http://vn.archive.ubuntu.com/ubuntu focal-backports InRelease
Reading package lists... Done
Reading package lists... Done
Building dependency tree
Reading state information... Done
apt-transport-https is already the newest version (2.0.2ubuntu0.1).
The following package was automatically installed and is no longer required:
  libfprint-2-tod1
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@worker1:~# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
OK
root@worker1:~# cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
> deb https://apt.kubernetes.io/ kubernetes-xenial main
> EOF
deb https://apt.kubernetes.io/ kubernetes-xenial main
root@worker1:~# apt-get update
Hit:1 https://download.docker.com/linux/ubuntu focal InRelease
Hit:2 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:4 http://vn.archive.ubuntu.com/ubuntu focal InRelease
Hit:5 http://vn.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:6 http://vn.archive.ubuntu.com/ubuntu focal-backports InRelease
Get:3 https://packages.cloud.google.com/apt kubernetes-xenial InRelease [8.993 B]
Get:7 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 Packages [41,7 kB]
Fetched 50,7 kB in 2s (27,7 kB/s)
Reading package lists... Done
root@worker1:~# apt-get install -y kubelet kubeadm kubectl
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no longer required:
  libfprint-2-tod1
Use 'apt autoremove' to remove it.
The following additional packages will be installed:
  conntrack cri-tools ebtables kubernetes-cni socat
Suggested packages:
  nftables
The following NEW packages will be installed:
  conntrack cri-tools ebtables kubeadm kubectl kubelet kubernetes-cni socat
        0 upgraded, 8 newly installed, 0 to remove and 0 not upgraded.
Need to get 68,5 MB of archives.
After this operation, 292 MB of additional disk space will be used.
Get:1 http://vn.archive.ubuntu.com/ubuntu focal/main amd64 conntrack amd64 1:1.4.5-2 [30,3 kB]
Get:2 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 cri-tools amd64 1.13.0-01 [8.775 kB]
Get:5 http://vn.archive.ubuntu.com/ubuntu focal/main amd64 ebtables amd64 2.0.11-3build1 [80,3 kB]
Get:8 http://vn.archive.ubuntu.com/ubuntu focal/main amd64 socat amd64 1.7.3.3-2 [323 kB]
Get:3 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubernetes-cni amd64 0.8.7-00 [25,0 MB]
Get:4 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubelet amd64 1.19.4-00 [18,2 MB]
Get:6 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubectl amd64 1.19.4-00 [8.347 kB]
Get:7 https://packages.cloud.google.com/apt kubernetes-xenial/main amd64 kubeadm amd64 1.19.4-00 [7.759 kB]
Fetched 68,5 MB in 9s (7.510 kB/s)
Selecting previously unselected package conntrack.
(Reading database ... 183230 files and directories currently installed.)
Preparing to unpack .../0-conntrack_1%3a1.4.5-2_amd64.deb ...
Unpacking conntrack (1:1.4.5-2) ...
Selecting previously unselected package cri-tools.
Preparing to unpack .../1-cri-tools_1.13.0-01_amd64.deb ...
Unpacking cri-tools (1.13.0-01) ...
Selecting previously unselected package ebtables.
Preparing to unpack .../2-ebtables_2.0.11-3build1_amd64.deb ...
Unpacking ebtables (2.0.11-3build1) ...
Selecting previously unselected package kubernetes-cni.
Preparing to unpack .../3-kubernetes-cni_0.8.7-00_amd64.deb ...
Unpacking kubernetes-cni (0.8.7-00) ...
Selecting previously unselected package socat.
Preparing to unpack .../4-socat_1.7.3.3-2_amd64.deb ...
Unpacking socat (1.7.3.3-2) ...
Selecting previously unselected package kubelet.
Preparing to unpack .../5-kubelet_1.19.4-00_amd64.deb ...
Unpacking kubelet (1.19.4-00) ...
Selecting previously unselected package kubectl.
Preparing to unpack .../6-kubectl_1.19.4-00_amd64.deb ...
Unpacking kubectl (1.19.4-00) ...
Selecting previously unselected package kubeadm.
Preparing to unpack .../7-kubeadm_1.19.4-00_amd64.deb ...
Unpacking kubeadm (1.19.4-00) ...
Setting up conntrack (1:1.4.5-2) ...
Setting up kubectl (1.19.4-00) ...
Setting up ebtables (2.0.11-3build1) ...
Setting up socat (1.7.3.3-2) ...
Setting up cri-tools (1.13.0-01) ...
Setting up kubernetes-cni (0.8.7-00) ...
Setting up kubelet (1.19.4-00) ...
Created symlink /etc/systemd/system/multi-user.target.wants/kubelet.service → /lib/systemd/system/kubelet.service.
Setting up kubeadm (1.19.4-00) ...
Processing triggers for man-db (2.9.1-1) ...
root@worker1:~# apt-mark hold kubelet kubeadm kubectl
kubelet set on hold.
kubeadm set on hold.
kubectl set on hold.
```
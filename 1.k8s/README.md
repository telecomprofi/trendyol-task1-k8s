# Installation of K8s cluster with kubespray

# kernel upgrade on Centos7

It turns out servers at Alibaba cloud are running CentOS7.x use old kernel 3.10.x which does not support overlay2 filesystem driver that is required to run Kuberenetes/Docker/Containerd efficiently.

8.208.12.185 | CHANGED | rc=0 >>
3.10.0-957.21.3.el7.x86_64
8.208.94.225 | CHANGED | rc=0 >>
3.10.0-957.21.3.el7.x86_64
8.208.92.149 | CHANGED | rc=0 >>
3.10.0-957.21.3.el7.x86_64
8.208.16.195 | CHANGED | rc=0 >>
3.10.0-957.21.3.el7.x86_64

So I have to update kernel to newer mainline version:
with the following set of ansible ad-hoc one-liners:
```
ansible -i servers all --become-user root -a 'rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org'
ansible -i servers all --become-user root -a 'rpm -Uvh https://www.elrepo.org/elrepo-release-7.el7.elrepo.noarch.rpm'
ansible -i servers all --become-user root -a 'yum --enablerepo=elrepo-kernel install kernel-ml -y'
```
and set grub boot to select the newer kernel:
```
grub2-set-default 0
```
and chek that newer kernel will be selected upo reboot:
```
cat /etc/grub2.cfg  | grep 5.17 
```
then reboot
```
ansible -i servers all --become-user root -m reboot
```

### kubespray config

at local machine:
sudo -i
git clone https://github.com/southbridgeio/kubespray
cd kubespray
pip install -r requirements.txt


update /etc/hosts
192.168.4.79 k8s-master
192.168.4.78 k8s-worker
192.168.4.76 consul-prometheus-alertmanager-grafana
192.168.4.77 elk-gitlab


### kubespray install






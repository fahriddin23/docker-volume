# docker-volume
Installing Docker on Centos 7 in AWS

yum install -q -y http://mirror.centos.org/centos/7/extras/x86_64/Packages/container-selinux-2.42-1.gitad8f0f7.el7.noarch.rpm
yum install -q -y http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/h/haveged-1.9.1-1.el7.x86_64.rpm
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -q -y firewalld docker-ce
systemctl enable firewalld
systemctl start firewalld
firewall-cmd --add-port=2377/tcp --permanent
firewall-cmd --add-port=2376/tcp --permanent
firewall-cmd --add-port=7946/tcp --permanent
firewall-cmd --add-port=7946/udp --permanent
firewall-cmd --add-port=4789/udp --permanent
firewall-cmd --zone=public --permanent --add-masquerade
firewall-cmd --reload
systemctl enable haveged
systemctl start haveged
systemctl enable docker
systemctl start docker
setenforce 1

# raven-system-api
An experimental project 


## Development Setup




## Server Setup

The server I have used is Alma Linux 10 minimal setup as a starting point, the complete setup procedure is detailed bellow. For now I have decided to disallow SELinux although this could be reinstated in the future, also I have left out any firewall capability because on a cloud installation the firewall will be handled upstream of the server. The software uses PHP 8.5.* along with a postgres database and redis it was decided that mongodb will not be used at this time and any object like documents will be serialised and stored in the database.

### Initial Setup
```
setenforce 0

cat >/etc/selinux/config <<EOL
SELINUX=disabled
SELINUXTYPE=targeted
EOL

fallocate -l 8G /swapfile

chmod 600 /swapfile

mkswap /swapfile

swapon /swapfile

cat >>/etc/fstab <<EOL
/swapfile swap swap defaults 0 0
EOL

sysctl vm.swappiness=2

echo "vm.swappiness = 2" >> /etc/sysctl.conf

dnf install -y epel-release

/usr/bin/crb enable

dnf -y install https://rpms.remirepo.net/enterprise/remi-release-10.rpm

dnf install -y nano wget bind-utils net-tools git zip unzip tar 

dnf update -y
```

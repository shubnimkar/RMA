# Open-PBS Configuration

`On all Nodes`

## Disable Firewalld

    systemctl stop firewalld
    systemctl disable firewalld
    systemctl status firewalld

## Disable SELinux:

    setenforce 0
    getenforce


## Set-up host config file /etc/hosts file 

    192.168.100.211 master master.cdac.in
    192.168.100.210 cn1 cn1.cdac.in
    192.168.100.197 cn2 cn2.cdac.in
    
## sync hosts files across nodes

    rsync /etc/hosts root@192.168.100.211:/etc/hosts
    rsync /etc/hosts root@192.168.100.197:/etc/hosts

` ON MASTER`

## Setup password-less SSH 

    ssh-keygen -t rsa

Now copy the key to other nodes

    ssh-copy-id root@node address

## Install GIT and clone openpbs repo (ON MASTER)

    yum install git -y

Clone OpenPBS repo from git hub

    git clone https://github.com/openpbs/openpbs.git

## install Development Tools on a CentOS / RHEL server (ON MASTER)

Type the following yum command as root user:

    yum group install "Development Tools"

If above command failed, try:

    yum groupinstall "Development Tools"

A note about failing groupinstall on CentOS/RHEL 
To install all the packages belonging to a package group called “Development Tools” use the following command:

     yum --setopt=group_package_types=mandatory,default,optional groupinstall "Development Tools"

OR

     yum --setopt=group_package_types=mandatory,default,optional group install "Development Tools"


-------------------------------------------------------------------------------------------------------------------------------
history

15  yum --setopt=group_package_types=mandatory,default,optional groupinstall "Development Tools"
   16  yum group list
   17  ll
   18  cd Downloads/
   19  ll
   20  cd
   21  ll
   22  ll openpbs/
   23  clear
   24  ll
   25  ll openpbs/
   26  cd openpbs/
   27  rpmbuild -ba openpbs.spec
   28  cat openpbs.spec
   29  cd
   30  mv openpbs/ openpbs-23.06.06
   31  cd openpbs-23.06.06/
   32  rpmbuild -ba openpbs.spec
   33  cd
   34  tar -cvf /root/rpmbuild/SOURCES/openpbs-23.06.06.tar.gz openpbs-23.06.06/
   35  cd openpbs-23.06.06/
   36  ll
   37  rpmbuild -ba openpbs.spec
   38  history



















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




















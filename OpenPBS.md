# Open-PBS Configuration

### On all nodes

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

## Setup password-less SSH (MASTER)

ssh-keygen -t rsa
ssh-copy-id root@client address

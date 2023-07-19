# Open-PBS Configuration


# Disable Firewalld

    systemctl stop firewalld
    systemctl disable firewalld
    systemctl status firewalld

# Disable SELinux:

    setenforce 0
    getenforce


# /etc/hosts file 

    192.168.100.211 master master.cdac.in
    192.168.100.210 cn1 cn1.cdac.in
    192.168.100.197 cn2 cn2.cdac.in
    
# sync hosts files across nodes

    rsync /etc/hosts root@192.168.100.211:/etc/hosts
    rsync /etc/hosts root@192.168.100.197:/etc/hosts

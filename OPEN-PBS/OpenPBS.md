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



[root@master openpbs-23.06.06]# yum install libtool-ltdl-devel hwloc-devel libXt-devel libedit-devel libical-devel ncurses-devel postgresql-devel postgresql-contrib python3-devel  tcl-devel tk-devel zlib-devel expat-devel openssl-devel  -y
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: centos.mirror.net.in
 * extras: centos.mirror.net.in
 * updates: centos.mirror.net.in
Package libtool-ltdl-devel-2.4.2-22.el7_3.x86_64 already installed and latest version
Package hwloc-devel-1.11.8-4.el7.x86_64 already installed and latest version
Package libXt-devel-1.1.5-3.el7.x86_64 already installed and latest version
Package libedit-devel-3.0-12.20121213cvs.el7.x86_64 already installed and latest version
Package libical-devel-3.0.3-2.el7.x86_64 already installed and latest version
Package ncurses-devel-5.9-14.20130511.el7_4.x86_64 already installed and latest version
Package postgresql-devel-9.2.24-8.el7_9.x86_64 already installed and latest version
Package postgresql-contrib-9.2.24-8.el7_9.x86_64 already installed and latest version
Package python3-devel-3.6.8-19.el7_9.x86_64 already installed and latest version
Package 1:tcl-devel-8.5.13-8.el7.x86_64 already installed and latest version
Package 1:tk-devel-8.5.13-6.el7.x86_64 already installed and latest version
Package zlib-devel-1.2.7-21.el7_9.x86_64 already installed and latest version
Package expat-devel-2.1.0-15.el7_9.x86_64 already installed and latest version
Package 1:openssl-devel-1.0.2k-26.el7_9.x86_64 already installed and latest version
Nothing to do

To build RPM
tar -cvf /root/rpmbuild/SOURCES/openpbs-23.06.06.tar.gz openpbs-23.06.06/

In openpbs folder
rpmbuild -ba openpbs.spec


[root@master openpbs-23.06.06]# cd /root/rpmbuild/
[root@master rpmbuild]# ll
total 0
drwxr-xr-x. 3 root root 30 Jul 19 20:30 BUILD
drwxr-xr-x. 2 root root  6 Jul 19 20:31 BUILDROOT
drwxr-xr-x. 3 root root 20 Jul 19 20:31 RPMS
drwxr-xr-x. 2 root root 37 Jul 19 20:07 SOURCES
drwxr-xr-x. 2 root root  6 Jul 19 20:03 SPECS
drwxr-xr-x. 2 root root 40 Jul 19 20:31 SRPMS
[root@master rpmbuild]# cd RPMS/
[root@master RPMS]# ll
total 0
drwxr-xr-x. 2 root root 231 Jul 19 20:31 x86_64
[root@master RPMS]# cd x86_64/
[root@master x86_64]# ll
total 14544
-rw-r--r--. 1 root root 1757740 Jul 19 20:31 openpbs-client-23.06.06-0.x86_64.rpm
-rw-r--r--. 1 root root 7577780 Jul 19 20:31 openpbs-debuginfo-23.06.06-0.x86_64.rpm
-rw-r--r--. 1 root root  508136 Jul 19 20:31 openpbs-devel-23.06.06-0.x86_64.rpm
-rw-r--r--. 1 root root 2086520 Jul 19 20:31 openpbs-execution-23.06.06-0.x86_64.rpm
-rw-r--r--. 1 root root 2946428 Jul 19 20:31 openpbs-server-23.06.06-0.x86_64.rpm
[root@master x86_64]# yum install openpbs-server-23.06.06-0.x86_64.rpm
Loaded plugins: fastestmirror, langpacks
Examining openpbs-server-23.06.06-0.x86_64.rpm: openpbs-server-23.06.06-0.x86_64
Marking openpbs-server-23.06.06-0.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package openpbs-server.x86_64 0:23.06.06-0 will be installed
--> Processing Dependency: postgresql-server >= 9.1 for package: openpbs-server-23.06.06-0.x86_64
Loading mirror speeds from cached hostfile
 * base: centos.mirror.net.in
 * extras: centos.mirror.net.in
 * updates: centos.mirror.net.in
--> Running transaction check
---> Package postgresql-server.x86_64 0:9.2.24-8.el7_9 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================================================
 Package                  Arch          Version                  Repository                                Size
================================================================================================================
Installing:
 openpbs-server           x86_64        23.06.06-0               /openpbs-server-23.06.06-0.x86_64         11 M
Installing for dependencies:
 postgresql-server        x86_64        9.2.24-8.el7_9           updates                                  3.8 M

Transaction Summary
================================================================================================================
Install  1 Package (+1 Dependent package)

Total size: 14 M
Total download size: 3.8 M
Installed size: 27 M
Is this ok [y/d/N]: y
Downloading packages:
postgresql-server-9.2.24-8.el7_9.x86_64.rpm                                              | 3.8 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : postgresql-server-9.2.24-8.el7_9.x86_64                                                      1/2
  Installing : openpbs-server-23.06.06-0.x86_64                                                             2/2
*** PBS Installation Summary
***
*** Postinstall script called as follows:
*** /opt/pbs/libexec/pbs_postinstall server 23.06.06 /opt/pbs /var/spool/pbs postgres
***
*** No configuration file found.
*** Creating new configuration file: /etc/pbs.conf
*** Replacing /etc/pbs.conf with /etc/pbs.conf.23.06.06
*** /etc/pbs.conf has been created.
***
*** Registering PBS as a service.
Created symlink from /etc/systemd/system/multi-user.target.wants/pbs.service to /usr/lib/systemd/system/pbs.service.
***
*** PBS_HOME is /var/spool/pbs
*** Creating new file /var/spool/pbs/pbs_environment
*** WARNING: TZ not set in /var/spool/pbs/pbs_environment
***
*** The PBS server has been installed in /opt/pbs/sbin.
*** The PBS scheduler has been installed in /opt/pbs/sbin.
***
*** The PBS communication agent has been installed in /opt/pbs/sbin.
***
*** The PBS MOM has been installed in /opt/pbs/sbin.
***
*** The PBS commands have been installed in /opt/pbs/bin.
***
*** End of /opt/pbs/libexec/pbs_postinstall
  Verifying  : postgresql-server-9.2.24-8.el7_9.x86_64                                                      1/2
  Verifying  : openpbs-server-23.06.06-0.x86_64                                                             2/2

Installed:
  openpbs-server.x86_64 0:23.06.06-0

Dependency Installed:
  postgresql-server.x86_64 0:9.2.24-8.el7_9

Complete!
[root@master x86_64]# systemctl status pbs
● pbs.service - Portable Batch System
   Loaded: loaded (/opt/pbs/libexec/pbs_init.d; enabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: man:pbs(8)
[root@master x86_64]# vim /etc/pbs.conf
[root@master x86_64]# etc /etc/pbs.conf
bash: etc: command not found...
[root@master x86_64]# cat /etc/pbs.conf
PBS_EXEC=/opt/pbs
PBS_SERVER=master
PBS_START_SERVER=1
PBS_START_SCHED=1
PBS_START_COMM=1
PBS_START_MOM=0
PBS_HOME=/var/spool/pbs
PBS_CORE_LIMIT=unlimited
PBS_SCP=/bin/scp
[root@master x86_64]# chmod 4755 /opt/pbs/sbin/pbs
pbs_comm             pbs_dataservice.bin  pbs_ds_monitor       pbs_ds_password.bin  pbsfs                pbs_iff              pbs_probe            pbs_sched            pbs_server.bin       pbs_upgrade_job
pbs_dataservice      pbs_demux            pbs_ds_password      pbs_ds_systemd       pbs_idled            pbs_mom              pbs_rcp              pbs_server           pbs_snapshot
[root@master x86_64]# chmod 4755 /opt/pbs/sbin/pbs_iff /opt/pbs/sbin/pbs_rcp

[root@master x86_64]# systemctl restart pbs
[root@master x86_64]# systemctl status pbs
● pbs.service - Portable Batch System
   Loaded: loaded (/opt/pbs/libexec/pbs_init.d; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2023-07-19 20:46:58 IST; 6s ago
     Docs: man:pbs(8)
  Process: 86055 ExecStart=/opt/pbs/libexec/pbs_init.d start (code=exited, status=0/SUCCESS)
    Tasks: 9
   Memory: 27.8M
   CGroup: /system.slice/pbs.service
           ├─87028 /opt/pbs/sbin/pbs_comm
           ├─87034 /opt/pbs/sbin/pbs_sched
           ├─87091 /opt/pbs/sbin/pbs_ds_monitor monitor
           ├─87128 /usr/bin/postgres -D /var/spool/pbs/datastore -p 15007
           ├─87132 postgres: logger process
           ├─87139 postgres: checkpointer process
           ├─87140 postgres: writer process
           ├─87142 postgres: wal writer process
           ├─87143 postgres: autovacuum launcher process
           ├─87144 postgres: stats collector process
           ├─87186 postgres: postgres pbs_datastore 192.168.100.211(44412) idle
           └─87188 /opt/pbs/sbin/pbs_server.bin

Jul 19 20:46:55 master pbs_init.d[86055]: /opt/pbs/sbin/pbs_comm ready (pid=87028), Proxy Name:master:17001, Threads:4
Jul 19 20:46:55 master pbs_init.d[86055]: PBS comm
Jul 19 20:46:55 master pbs_init.d[86055]: PBS sched
Jul 19 20:46:55 master su[87049]: (to postgres) root on none
Jul 19 20:46:55 master su[87092]: (to postgres) root on none
Jul 19 20:46:57 master su[87150]: (to postgres) root on none
Jul 19 20:46:58 master pbs_init.d[86055]: Connecting to PBS dataservice...connected to PBS dataservice@master
Jul 19 20:46:58 master pbs_init.d[86055]: Connecting to PBS dataservice...connected to PBS dataservice@master
Jul 19 20:46:58 master pbs_init.d[86055]: PBS server
Jul 19 20:46:58 master systemd[1]: Started Portable Batch System.

[root@master x86_64]# cat /etc/pbs.conf
PBS_EXEC=/opt/pbs
PBS_SERVER=master
PBS_START_SERVER=1
PBS_START_SCHED=1
PBS_START_COMM=1
PBS_START_MOM=0
PBS_HOME=/var/spool/pbs
PBS_CORE_LIMIT=unlimited
PBS_SCP=/bin/scp
[root@master x86_64]# /etc/init.d/pbs
Usage: pbs --version
Usage: pbs {start|stop|restart|status}
[root@master x86_64]# /etc/init.d/pbs status
pbs_server is pid 87188
pbs_sched is pid 87034
pbs_comm is 87028






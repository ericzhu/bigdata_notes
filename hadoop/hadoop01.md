
MapReduce in charge of computing
YARN in charge of resource scheduling

HDFS is a distributed file system.

Name Node (Table of Content): The server that remembers the location of every file blocks
Secondary Name Node: redundant copy the name node
Date Node (Chapters and pages): The server where the data is stored

YARN is a resource manager.
ex: A cluster includes 3 nodes
Node A: 40G Memory, 4 CPU -> Node Manager A
Node B: 40G Memory, 4 CPU -> Node Manager B
Node C: 40G Memory, 4 CPU -> Node Manager C

Resource manager manages 120G Memory and 12 CPU


What does the YARN manage? CPU and Memory
YARN has two key coponents: 
Resource Manager: Manage the resource in a cluster of nodes.
Node Manager: Manage the resource in a individual node.
Client submits job to resource manager. YARN creates 

* Resource Manager - Boss of the cluster
* Node Manager - Boss of an individual node
* Application Master - The boss of an application
* Container - managed by node managers, it is virtualized independent server. it has it own RAM, CPU, Disk and network.


![hadoop eco-system](../images/hadoop_ecosystem.png)

MapReduce

In map phase -> each worker process a small chunk of data
In reduce paths -> summary the output of each worker and generate the result on a server that do the the summarization


Create a template linux virtual machine

What we will set in the virtual machine
1. RAM Size
2. Disk Size
3. IP Address
4. Host Name

Change the host name and host name mapping

```shell
[root@n100 ~]# cat /etc/hostname
n100
[root@n100 ~]#
[root@n100 ~]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.10.100  n100
192.168.10.101  n101
192.168.10.102  n102
192.168.10.103  n103
192.168.10.104  n104
```

Stop and disable firewall
```shell
[root@n100 ~]# systemctl stop firewalld
[root@n100 ~]# systemctl disable firewalld.service
```

Add a new user to centos
```shell
[root@n100 ~]# useradd lab1
[root@n100 ~]# passwd lab1
Changing password for user lab1.
New password:
BAD PASSWORD: The password is shorter than 7 characters
Retype new password:
passwd: all authentication tokens updated successfully.
```

Allow user to run command use super user previlige withou password

```shell
[root@n100 lab]# vim /etc/sudoers
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL

## Allows members of the 'sys' group to run networking, software,
## service management apps and more.
# %sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES, LOCATE, DRIVERS

## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL

lab     ALL=(ALL)       NOPASSWD:ALL

```

install JDK and configure environment variable

```shell
[lab@n102-hadoop software]$ tar -zxvf jdk-8u212-linux-x64.tar.gz -C ../module/

# Change add environment variable to this file
[lab@n102-hadoop ~]$ sudo vim /etc/profile

# instead of change the /etc/profile, add a new shell file in /etc/profile.d
[lab@n102-hadoop ~]$ sudo touch /etc/profile.d/my_envs.sh
[lab@n102-hadoop ~]$ chmod 777 /etc/profile.d/my_envs.sh
[lab@n102-hadoop ~]$ vim /etc/profile.d/my_envs.sh

# JAVA HOME
export JAVA_HOME=/opt/module/jdk1.8.0_212
export PATH=$PATH:$JAVA_HOME/bin
```

Hadoop running mode

local - files stored in local file system
pseuto distributed - files are stored in the HDFS file system
fully distributed - files are stored in HDFS and multi servers cordinate

Run Hadoop word count in local running mode

```shell
[lab@n102-hadoop hadoop-3.1.3]$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount wcinput/ wcoutput/
```

rsync vs scp command


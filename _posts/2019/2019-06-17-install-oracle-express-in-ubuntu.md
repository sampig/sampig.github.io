---
layout: post
title: "Install Oracle Database Express Edition on Ubuntu 16.04"
date: 2019-06-17 12:35:00 +0200
category: tutorial
tagline: ""
tags: [Ubuntu, Oracle]
abstract : "Install Oracle Database Express 11g Release 2 (11.2) for Linux x86-64 on Ubuntu 16.04."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Requirements](#requirements)
    - [System Environment](#system-environment)
    - [Permission Requirement](#permission-requirement)
* [Installation](#installation)
    - [Preparation](#preparation)
    - [Start Installation](#start-installation)
    - [Management](#management)
* [The End](#the-end)
* [References](#references)


# Introduction

Oracle Database Express Edition (Oracle Database XE) is a free version of Oracle relational database.
With Oracle Database XE, use an intuitive, browser-based interface to administer the database, create tables, views and other database objects, import, export, and view table data, run queries and SQL scripts and generate reports.

It also includes some tools to manage the Oracle database.


# Requirements

## System Environment

1. Network protocol. The following protocols are supported: IPC, Named Pipes, SDP, TCP/IP, TCP/IP with SSL.
2. RAM: 256 MB minimum, 512 MB recommended.
3. Packages: glibc>=2.3.4-2.41, make>=3.80, binutils>=2.16.91.0.5, gcc>=4.1.2, libaio>=0.3.104.
4. Minimum swap space required is 2 GB or twice the size of RAM.

## Permission Requirement

Must have root permission.


# Installation

Before installation, download the correct version of Oracle Database XE from [Oracle Database Express Edition (XE) Downloads](https://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html){:target="_blank"}.

## Preparation

It only provides the installation of an RPM file for Linux.
So we need to take some actions to make it adapt to Ubuntu system.

Install some required packages:
```bash
sudo apt-get install alien libaio1 unixodbc
```

Use `unzip *.zip` command to unzip the downloaded package.
Then some files and directories are generated in the `Disk1` directory.

There is an RPM file for the installation in the directory.
Convert it to DEB package format for Ubuntu:
```bash
sudo alien --scripts -d oracle-xe*.rpm
```

Create a required `chkconfig` script with the content below:
```
#!/bin/bash
# Oracle 11gR2 XE installer chkconfig hack for Ubuntu
file=/etc/init.d/oracle-xe
if [[ ! `tail -n1 $file | grep INIT` ]]; then
    echo >> $file
    echo '### BEGIN INIT INFO' >> $file
    echo '# Provides: OracleXE' >> $file
    echo '# Required-Start: $remote_fs $syslog' >> $file
    echo '# Required-Stop: $remote_fs $syslog' >> $file
    echo '# Default-Start: 2 3 4 5' >> $file
    echo '# Default-Stop: 0 1 6' >> $file
    echo '# Short-Description: Oracle 11g Express Edition' >> $file
    echo '### END INIT INFO' >> $file
fi
update-rc.d oracle-xe defaults 80 01
```

Change the permission of this file `/sbin/chkconfig` to be executable using `chmod 755`.

Set kernel parameters.
Oracle 11gR2 XE requires additional kernel parameters which you need to create a file `/etc/sysctl.d/60-oracle.conf` input the content below:
```
# Oracle 11g XE kernel parameters 
fs.file-max=6815744  
net.ipv4.ip_local_port_range=9000 65000  
kernel.sem=250 32000 100 128 
kernel.shmmax=536870912 
```

Load the kernel parameters:
```
sudo service procps start
```

Verify the new parameters are loaded using:
```
sudo sysctl -q fs.file-max
```
You should see the file-max value that you entered earlier.

Set up `/dev/shm` mount point for Oracle.
Create a file `/etc/rc2.d/S01shm_load` using root permission.
Copy the following into the file and save.
```bash
#!/bin/sh
case "$1" in
    start)
        mkdir /var/lock/subsys 2> /dev/null
        touch /var/lock/subsys/listener
        rm /dev/shm 2> /dev/null
        mkdir /dev/shm 2> /dev/null
        mount -t tmpfs shmfs -o size=2048m /dev/shm ;;
    *)
    echo "error: only 'start' command is supported."
    exit 1 ;;
esac
```

Change the permissions of the file `S01shm_load` using the command `chmod 755`.

Now execute the following commands:
```
sudo ln -s /usr/bin/awk /bin/awk 
sudo mkdir /var/lock/subsys 
sudo touch /var/lock/subsys/listener
```

Now, Reboot Your System

## Start Installation

Install the Oracle XE from the DEB package:
```bash
sudo dpkg --install oracle-xe*.deb
```

Configure Oracle:
```
sudo /etc/init.d/oracle-xe configure 
```

Setup environment variables by editing the `~/.bashrc` file:
```
export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
export ORACLE_SID=XE
export NLS_LANG=`$ORACLE_HOME/bin/nls_lang.sh`
export ORACLE_BASE=/u01/app/oracle
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
export PATH=$ORACLE_HOME/bin:$PATH
```
Do not forget to load the changes after changing the `.bashrc` file..

Start the Oracle 11gR2 XE:
```
sudo service oracle-xe start
```

Add user YOURUSERNAME to group dba:
```
sudo usermod -a -G dba YOURUSERNAME
```

## Management

Use the Oracle XE Command Shell.

Start the Oracle XE 11gR2 server:
```
sudo service oracle-xe start
```

Start command line shell as the system admin:
```
sqlplus sys as sysdba
```

Enter the password that you gave while configuring Oracle earlier.
You will now be placed in a SQL environment that only understands SQL commands.

Create a regular user account in Oracle using the SQL command:
```SQL
create user USERNAME identified by PASSWORD;
```

Replace USERNAME and PASSWORD with the username and password of your choice. Please remember this username and password. If you had error executing the above with a message about resetlogs, then execute the following SQL command and try again:
```SQL
alter database open resetlogs;

Grant privileges to the user account using the SQL command:

grant connect, resource to USERNAME;
```

Replace USERNAME and PASSWORD with the username and password of your choice. Please remember this username and password.

Exit the sys admin shell using the SQL command:
```SQL
exit;
```

Start the commandline shell as a regular user:
```
sqlplus
```

Now, you can run SQL commands.


# The End

Nowadays, some other open source RDBs such as MySQL and PostgreSQL are quite popular.
In addition, other NoSQL DBs such as MongoDB, CouchDB, Cassandra and Neo4J are also widely being used.

In many projects for personal or small business, Oracle will not be the first choice.
But it is still necessary to remember how to install an Oracle DB with simple version for testing or learning.
Anyway, Oracle PL/SQL is really powerful.


# References

1. [Database Express Edition Installation Guide](https://docs.oracle.com/cd/E17781_01/install.112/e18802/toc.htm){:target="_blank"}
2. [Ask Ubuntu - How to install Oracle 11gR2 on Ubuntu 14.04?](https://askubuntu.com/questions/566734/how-to-install-oracle-11gr2-on-ubuntu-14-04){:target="_blank"}
3. [Installing Oracle 11g R2 Express Edition on Ubuntu 64-bit](http://meandmyubuntulinux.blogspot.com/2012/05/installing-oracle-11g-r2-express.html){:target="_blank"}
4. [Oracle Database Express Edition (XE) Downloads](https://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html){:target="_blank"}

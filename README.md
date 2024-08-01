### Nagios-Monitoring-Tool
### Author : ✍️ Hackbugs
### CODE USED FOR INSTALLATION
________________________________________
```sh
sudo su
yum install httpd php -y
yum install gcc glibc glibc-common -y
yum install gd gd-devel

adduser -m nagios
passwd nagios

groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache

mkdir ~/downloads
cd ~/downloads

wget http://prdownloads.sourceforge.net/so...
wget http://nagios-plugins.org/download/na...

tar zxvf nagios-4.0.8.tar.gz
cd nagios-4.0.8

./configure --with-command-group=nagioscmd
make all


make install
make install-init
make install-config
make install-commandmode


make install-webconf

htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
service httpd restart


cd ~/downloads
tar zxvf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3

./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install


chkconfig --add nagios
chkconfig nagios on

/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

service nagios start
service httpd restart

`END OF CODE`
```
________________________________________________________________________________________________________________________

 - Daemon start Plugins Service
 - Nagios Plugins - NRPE - Nagios Remote Plugin Executor - this connect with Daemon on server side
 - Nagios Plugins - Check By SSH - installed on Node or clients We also called NRPE agent

 - We access of Nagios or Monitor through Ip-address or access address on webpage on browser
 - Nagios access - 192.28.87.672/Nagios and login with id and password 

### Install to crate environment Nagios

  - httpd, Browser
  - PHP, Dashboard
  - Gcc & GD, complier
  - make file , to build
  - Perl, Script
 
### Introduction to Nagios Continuous Monitoring Tool

**Nagios** is a powerful, open-source monitoring system that enables organizations to identify and resolve IT infrastructure problems before they affect critical business processes. It provides monitoring and alerting services for servers, switches, applications, and services. Nagios was originally designed to run under the Linux operating system but can also run on other Unix variants.

### Key Features of Nagios

1. **Monitoring of Network Services**: HTTP, FTP, SMTP, POP3, SNMP, etc.
2. **Monitoring of Host Resources**: Processor load, disk usage, system logs, etc.
3. **Simple Plugin Design**: Allows users to develop their service checks easily.
4. **Parallelized Service Checks**: Enhances performance and efficiency.
5. **Email and SMS Alerts**: Alerts administrators when issues arise and are resolved.
6. **History and Trending**: Offers data graphing and alert logging capabilities.
7. **Web Interface**: Provides a comprehensive web interface for viewing current status, history, and generating reports.

### How Nagios Works

1. **Plugins**: Nagios uses plugins, which are scripts or binaries that perform checks on the services and host resources. These plugins return the status to Nagios.
2. **Scheduler**: Nagios has an internal scheduler that runs the plugins at specified intervals.
3. **Alerting**: Based on the results from the plugins, Nagios can send alerts via email, SMS, or other methods.
4. **Web Interface**: The results can be viewed in a web interface, which provides various views like the current status, historical logs, and trend graphs.

### Installation and Setup

Here’s a basic guide to installing and setting up Nagios on a Linux system:

#### Prerequisites

- A server running a Linux distribution (e.g., Ubuntu, CentOS).
- Root or sudo access to the server.
- Basic knowledge of the command line.

#### Step-by-Step Installation on Ubuntu

1. **Update the Package List**

   ```bash
   sudo apt-get update
   ```

2. **Install Required Dependencies**

   ```bash
   sudo apt-get install -y autoconf gcc libc6 make wget unzip apache2 apache2-utils php libgd-dev
   ```

3. **Create a Nagios User and Group**

   ```bash
   sudo useradd nagios
   sudo groupadd nagcmd
   sudo usermod -a -G nagcmd nagios
   sudo usermod -a -G nagcmd www-data
   ```

4. **Download and Install Nagios Core**

   ```bash
   cd /tmp
   wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
   tar -zxvf nagios-4.4.6.tar.gz
   cd nagios-4.4.6
   ./configure --with-command-group=nagcmd
   make all
   sudo make install
   sudo make install-init
   sudo make install-config
   sudo make install-commandmode
   sudo make install-webconf
   ```

5. **Install Nagios Plugins**

   ```bash
   cd /tmp
   wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
   tar -zxvf nagios-plugins-2.3.3.tar.gz
   cd nagios-plugins-2.3.3
   ./configure --with-nagios-user=nagios --with-nagios-group=nagios
   make
   sudo make install
   ```

6. **Configure Apache for Nagios**

   ```bash
   sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
   sudo systemctl restart apache2
   ```

7. **Start Nagios**

   ```bash
   sudo systemctl start nagios
   sudo systemctl enable nagios
   ```

8. **Access the Nagios Web Interface**

   Open your web browser and navigate to `http://<server-ip>/nagios` and log in with the username `nagiosadmin` and the password you set up earlier.

### Configuring Nagios

1. **Define Hosts and Services**

   Edit the configuration files located in `/usr/local/nagios/etc/objects/` to define the hosts and services you want to monitor.

2. **Apply Configuration Changes**

   After making changes to the configuration files, check the configuration for errors and then restart Nagios to apply the changes:

   ```bash
   sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
   sudo systemctl restart nagios
   ```

### Conclusion

Nagios is a robust tool for monitoring IT infrastructure, providing essential insights and alerts to maintain system health and uptime. Its flexibility through plugins and comprehensive web interface makes it a popular choice for system administrators. By following the installation and setup guide, you can quickly deploy Nagios and start monitoring your environment effectively.
____________________________________________________________________________________________________4____________________________________________________________________________________________________


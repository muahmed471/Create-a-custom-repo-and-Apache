# Create-a-custom-repo-and-Apache
Setup Repo and Create Apache

Repository is a collection of packages one needs to install to perform a specific task, These tasks could be running a web service or running an application on Linux os.

Server side:
mkdir /admin

mkdir -p /var/www/html/centos/7

Copy the iso with winscp in /admin

cd /admin

ls -ltr

Centos7.iso

df -h

mount -o loop /admin/CentOS-7-x86_64-DVD-2009.iso /mnt

df -h

mkdir /tmp/repo

cd /etc/yum.repos.d

ls -ltr

mv * /tmp/repo

pwd

vi yum.repo

[base]
name=Linux Enterprise Kernel
baseurl=file:///mnt
enabled=1
gpgcheck=0

:wq!

ls -ltr 

yum clean all

yum list

yum install -y createrepo


cd /mnt

cp -rp Packages /var/www/html/centos/7

createrepo /var/www/html/centos/7


Setup a permanent repo baseurl in repo file:

cd /etc/yum.repos.d 

vi yum.repo

[base]
name=Linux Enterprise Kernel
baseurl=file:///var/www/html/centos/7
enabled=1
gpgcheck=0

:wq!

Install Apache & set up http as baseurl in repo file

yum install -y httpd

systemctl start httpd

yum install net-tools

netstat -anp |grep -w 80

cd /var/www/html/centos

ls 7

restorecon -vvv -R 7

ls -ldZ 7

systemctl restart httpd

cd /etc/yum.repos.d 

vi yum.repo

[base]
name=Linux Enterprise Kernel
baseurl=http://192.168.56.8/centos/7
enabled=1
gpgcheck=0

:wq!

systemctl stop firewalld

systemctl disable firewalld

on browser http://192.168.56.8/centos/7

Client side:

mkdir /tmp/repo

cd /etc/yum.repos.d

mv * /tmp/repo

vi yum.repo

[base]
name=Linux Enterprise Kernel
baseurl=http://192.168.56.8/centos/7
enabled=1
gpgcheck=0

:wq!

yum clean all

yum list

Webserver (Apache)

hostnamectl set-hostname client.example.com

yum install -y httpd

cd /var/www/html

vi index.html

<h1>Hello World<br>
<br>Welcome to Hyderabad Tutorials<br>
<br>Apache Webserver<br>

:wq!

cat /var/www/html/index.html

cd /etc/httpd/conf

vi httpd.conf

<VirtualHost *:80>
ServerRoot "/etc/httpd"
ServerAdmin root@localhost
Servername client.example.com:80
DocumentRoot "/var/www/html"
Errorlog "logs/error_log"
LogLevel warn
</VirtualHost>

:wq!

httpd -t  (check httpd config file for any errors)

systemctl stop firewalld

systemctl restart httpd

netstat -anp |grep -w 80

open browser http://192.168.56.7

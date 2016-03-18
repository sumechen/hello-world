1. 删除原有的yum
rpm -qa yum
rpm -e XXXXX --nodeps
rpm -e XXXXX --nodeps
rpm -e XXXXX --nodeps

2. 下载新的OS安装文件, 并安装
export HTTP=http://mirrors.163.com/centos/6/os/x86_64/Packages
wget $HTTP/yum-plugin-fastestmirror-1.1.30-30.el6.noarch.rpm 
wget $HTTP/yum-metadata-parser-1.1.2-16.el6.x86_64.rpm
wget $HTTP/yum-3.2.29-69.el6.centos.noarch.rpm

163yum源文件会变， 可以http://mirrors.163.com/centos/6/os/x86_64/Packages中查找文件的最新名称

安装的时候 这两个需要一起安装, 一个命令， 分开会出错
rpm -ivh yum-plugin-fastestmirror-1.1.30-14.el6.noarch.rpm yum-3.2.29-40.el6.centos.noarch.rpm  

rpm -ivh yum-plugin-fastestmirror-1.1.30-30.el6.noarch.rpm 
rpm --import http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-6 

3. 制作163.repo, 并放在/etc/yum.repo.d, 名称必须与.repo结尾, 从网上下载的带$serverrelease及其他变量， 直接替换, 也可以配置， 配置起来很麻烦
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-6 - Base - 163.com
baseurl=http://mirrors.163.com/centos/6/os/x86_64/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=x86_64 &repo=os
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6

#released updates 
[updates]
name=CentOS-6 - Updates - 163.com
baseurl=http://mirrors.163.com/centos/6/updates/x86_64/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=x86_64 &repo=updates
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6

#additional packages that may be useful
[extras]
name=CentOS-6 - Extras - 163.com
baseurl=http://mirrors.163.com/centos/6/extras/x86_64/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=x86_64 &repo=extras
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-6 - Plus - 163.com
baseurl=http://mirrors.163.com/centos/6/centosplus/x86_64/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=x86_64 &repo=centosplus
gpgcheck=1
enabled=0
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6

#contrib - packages by Centos Users
[contrib]
name=CentOS-6 - Contrib - 163.com
baseurl=http://mirrors.163.com/centos/6/contrib/x86_64/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=x86_64 &repo=contrib
gpgcheck=1
enabled=0
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6


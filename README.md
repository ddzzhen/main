# oneinstack
#来自网址:http://mirrors.linuxeye.com/
菜鸟一枚,向大神致敬!

#############################################################################
yum -y install wget screen python   #for CentOS/Redhat
apt-get -y install wget screen python  #for Debian/Ubuntu
wget http://aliyun-oss.linuxeye.com/oneinstack-full.tar.gz    #阿里云用户下载
wget http://mirrors.linuxeye.com/oneinstack-full.tar.gz    #包含源码，国内外均可下载
wget http://mirrors.linuxeye.com/oneinstack.tar.gz    #不包含源码，建议仅国外主机下载
tar xzf oneinstack-full.tar.gz
cd oneinstack    #如果需要修改目录(安装、数据存储、Nginx日志)，请修改options.conf文件
screen -S oneinstack    #如果网路出现中断，可以执行命令`screen -r oneinstack`重新连接安装窗口
./install.sh     #请勿sh install.sh或者bash install.sh这样执行

#############################################################################


ssh port :default

web server? y

nignx?
apache?
tomcat?
database?
	version of the database?
	password of the database?
php?
opcode cache of the php ?  代码缓存组件,建议y
	建议ZendOpcache

ioncube? PHP加解密组件,建议n

image? 图片处理,建议y ImageMagick

Pure-FTPD? 建议y

phpmyadmin? 建议y

redis? 建议y

memached? 建议n

jemalloc or tcmalloc?  建议y jemalloc

hhvm? 建议n

#################################

添加虚拟主机:

./vhost.sh

	ssl ?  建议 n
	domain 虚拟主机名

	more domain name?  y
		type domainname or IP 
	redirect to?  建议y

	directory for the domain: 绝对路径

	hotlink protection? 防盗链 建议n

	rewrite rule? 建议y
		wordpress
	access_log? 记录日志 y

删除虚拟主机:
./vhost.sh del

管理ftp账号:
./pureftpd_vhost.sh

如何备份:

```
./backup_setup.sh # Set backup options 
./backup.sh # Start backup, You can add cron jobs
# crontab -l
0 1 * * * cd ~/oneinstack;./backup.sh  > /dev/null 2>&1 &
```
####
```
./backup.sh # Start backup, You can add cron jobs
   # crontab -l # Examples 
     0 1 * * * cd ~/oneinstack;./backup.sh  > /dev/null 2>&1 &
```
服务管理:

Nginx/Tengine:
   service nginx {start|stop|status|restart|reload|configtest}
MySQL/MariaDB/Percona:
   service mysqld {start|stop|restart|reload|status}
PHP:
   service php-fpm {start|stop|restart|reload|status}
HHVM:
   service supervisord {start|stop|status|restart|reload}
Apache:
service httpd {start|restart|stop}
Tomcat:
service tomcat {start|stop|status|restart}
Pure-Ftpd:
   service pureftpd {start|stop|restart|status}
Redis:
   service redis-server {start|stop|status|restart|reload}
Memcached:
   service memcached {start|stop|status|restart|reload}

更新版本:
./upgrade.sh

卸载:
./uninstall.sh

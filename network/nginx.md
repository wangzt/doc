# Nginx相关

## Linux中查找nginx安装目录和nginx.conf配置文件目录

1.查看nginx安装目录

在shell中输入命令

`ps -ef | grep nginx`

返回结果

root      1503     1  0 Jan1 ?        00:00:00 nginx: master process /usr/sbin/nginx

2.查看nginx.conf配置文件目录

在shell中输入命令

`nginx -t`

返回结果

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

3.启动nginx服务

输入命令

`nginx -s reload`


## Centos7下开启端口
1. 关闭开启防火墙
>systemctl stop firewalld.service
systemctl start firewalld.service

2. 查看防火墙是否开启的状态，以及开放端口的情况
>systemctl status firewalld.service
sudo firewall-cmd --list-all

3. 通过以下命令开放http 80 端口
>sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --add-port=80/tcp --permanent

4. 然后重启防火墙
>sudo firewall-cmd --reload

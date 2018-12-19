#Redhat安装jenkins

##正常步骤
1、下载并解压tomcat
2、下载jenkins.war放在tomcat/webapps下
3、在tomcat/bin/下执行startup.sh
4、打开浏览器：输入 http:127.0.0.1:8080/jenkins

##如果有问题，可以按照以下步骤排查
1、查看端口是否被占用
netstat -nlp|grep LISTEN

如果8080被占用了，需要修tomcat/conf/server.xml中的8080为没有被使用的

2、查看端口是否开启
/sbin/iptables -L -n

3、开启端口
vi /etc/sysconfig/iptables
加入如下内容
-A INPUT -p tcp -m tcp --dport 8080 -j ACCEPT
然后保存退出，重启服务
/etc/init.d/iptables restart

4、Tomcat下部署Jenkins无法打开（404）的解决办法
查看tomcat下logs目录，localhost.XXX.log
有类似日志：Error configuring application listener of class hudson.WebAppMain
java.lang.UnsupportedClassVersionError: hudson/WebAppMain : Unsupported major.minor version 52.0 (unable to load class hudson.WebAppMain)

表示tomcat使用的jdk版本有问题，可能需要升级
如果有多版本jdk，可以在tomcat/bin/setclasspath.sh中最开始设置
JAVA_HOME=/usr/xxx/jdk8
JRE_HOME=/usr/xxx/jdk8/jre

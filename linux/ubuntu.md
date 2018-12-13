#问题集

##Ubuntu下遇到ld: cannot find -lXX之类的问题，提示找不到相关库文件
###1、如果能上网，最不用废脑子的办法：

$ sudo apt-get install apt-file

$ apt-file update

$ apt-file search libXX.so

apt-file 将列出所有包含libXX.so文件的apt包，

选择相应的包用apt-get安装即可。通常请选择带dev的包安装

###2、不用上网，并且系统里可能有库文件，只是名称不对例如 libXXX.so.1的情况

$ locate libXXX.so  

如果有libXXX.so.1等类似文件，进入文件目录

$ ln -sv libXXX.so.1 libXXX.so

当然，还要检查一下libXXX.so是否在环境变量所指向的目录中，比如/usr /usr/lib/等等


##通常在软件编译时出现的usr/bin/ld: cannot find -lxxx的错误，主要的原因是库文件并没有导入的ld检索目录中。

解决方式：

1。确认库文件是否存在，比如-l123, 在/usr/lib, /usr/local/lib,或者其他自定义的lib下有无lib123.so, 如果只是存在lib123.so.1,

那么可以通过ln -sv lib123.so.1   lib123.so，建立一个连接重建lib123.so.

2。检查/etc/ld.so.conf中的库文件路径是否正确，如果库文件不是使用系统路径，/usr/lib, /usr/local/lib, 那么必须在文件中加入。

3。ldconfig 重建ld.so.cache文件，ld的库文件检索目录存放文件。尤其刚刚编译安装的软件，必须运行ldconfig，才能将新安装的库文件导入ld.so.cache
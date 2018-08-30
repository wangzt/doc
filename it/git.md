#Git使用

##拷贝linux中的ssh key到win10
.ssh/config文件，添加如下内容
```
Host github.com                 
    HostName github.com
    IdentityFile C:\\Users\\popfisher\\.ssh\\id_rsa_github
    PreferredAuthentications publickey
    User username1
```
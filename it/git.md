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

##删除远程分支
git push origin  :branch_name

##远程仓库已经不存在的分支，本地无法删除，可以使用以下命令
git remote prune origin

##查看分支创建时间，在创建分支的目录下
git reflog show --date=iso branch_name

##导出特定用户提交记录到csv
git log --author=wangzhitao --date=iso --pretty=format:'"%ad","%s"' >log.csv
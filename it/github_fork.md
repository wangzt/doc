# github如何实现fork的项目与原项目同步

假设，github上自己的项目 https://github.com/wangzt/engine fork自 https://github.com/flutter/engine， 需要保持同步

１、clone自己的项目到本地
`git clone https://github.com/wangzt/engine.git flutter_engine`

使用  `git remote -v` 查看项目的远程信息，发现结果都是关于我自己主页的，origin是分支名称
```
origin	https://github.com/wangzt/engine.git (fetch)
origin	https://github.com/wangzt/engine.git (push)
```

2、为项目添加远程分支
`git remote add upstream https://github.com/flutter/engine`

其中 upstream是远程分支名，后面的链接是原作者的仓库地址，此时再重新查看项目的远程信息，发现多了upstream的信息，是刚刚添加的原作者的仓库
```
origin	https://github.com/wangzt/engine.git (fetch)
origin	https://github.com/wangzt/engine.git (push)
upstream	https://github.com/flutter/engine (fetch)
upstream	https://github.com/flutter/engine (push)
```

3、如果远程项目进行了更新，我们需要从upstream分支进行拉取，这样本地的代码就和原作者的代码同步了
`git pull upstream master`

4、将本地代码提交到自己主页的分支，即origin上了，这样，我自己主页的项目就和原作者的项目进行了同步
`git push origin master`
# Flutter环境构建

## 前期准备

1. 安装新版本git，>2.13
2. 安装openjdk，>=1.8
3. 国内最好配置较快的源,但是有些包不全，如果有问题，可以去掉，继续使用官方的
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

临时去掉
unset PUB_HOSTED_URL
unset FLUTTER_STORAGE_BASE_URL

## 下载安装Flutter SDK

1. 从flutter的github官方下载源码，https://github.com/flutter/flutter，具体git地址如下
https://github.com/flutter/flutter.git，切换到stable分支
2. 配置flutter到环境变量中
3. 检查Flutter相关资源是否OK 运行：`flutter doctor -v`

## 构建安卓包
在项目目录下，依次运行
`flutter clean`
`flutter build apk`

## 问题集

1. `flutter doctor -v` 发现flutter version是0.0.0-unknown
方法： git版本太老，更新到最新版本的git，删除老git

2. `flutter build apk` 出现
>Git error. Command: git fetch
fatal: 不是一个 git 仓库（或者任何父目录）：.git

方法：使用 `flutter packages -v pub get -v` 检查具体问题原因
一般有两种原因：flutter权限问题，flutter缓存问题（清理 `~/.pub-cache`即可）

3. 安卓flutter混合项目，可能会有gradle相关资源下载失败，可参考安卓端gradle相关问题处理
更换阿里云的源可能会好
maven {url 'https://maven.aliyun.com/repository/public'}
maven {url 'https://maven.aliyun.com/repository/central'}
maven {url 'https://maven.aliyun.com/repository/gradle-plugin'}
maven {url 'https://maven.aliyun.com/repository/google'}
maven {url 'https://maven.aliyun.com/repository/jcenter'}

4. 打release包失败
先尝试`flutter build apk --debug` 看看是否debug包可以,如果可以，可能是lint检查的问题，可以在android/app下面的build.gradle里添加如下配置
```
lintOptions {
    checkReleaseBuilds false
    abortOnError false
}
```


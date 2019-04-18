# Flutter环境构建

## 前期准备

1. 安装新版本git，>2.13
2. 安装openjdk，>=1.8
3. 国内最好配置较快的源,
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

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

2. 安卓flutter混合项目，可能会有gradle相关资源下载失败，可参考安卓端gradle相关问题处理



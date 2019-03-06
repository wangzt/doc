#安卓源码#

1. 查看可切换的分支
在AOSP目录下
```
    cd .repo/manifests
    git branch -a | cut -d / -f 3
```

2. 切换分支(以android-7.0.0_r1为例)
```
    repo init -u https://android.googlesource.com/platform/manifest -b android-7.0.0_r1
```

3. 同步代码
```
    repo sync
```

4. 如果本地有变化，同步失败，先强制回退，再切换
```
    repo forall -c git reset --hard
    repo init -u https://android.googlesource.com/platform/manifest -b android-7.0.0_r1
    repo sync
```
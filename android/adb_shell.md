1、查看当前活跃的activity栈
adb shell dumpsys activity activities | sed -En -e '/Running activities/,/Run #0/p'

2、查看特定应用启动的service
adb shell dumpsys activity s packageName

3、查询某个app的进程状态
adb shell dumpsys activity p packageName

4、android log输出量巨大，特别是通信系统的log，因此，android把log输出到不同的缓冲区中，目前定义了四个log缓冲区：

1）Radio：输出通信系统的log

2）System：输出系统组件的log

3）Event：输出event模块的log

4）Main：所有java层的log，遗迹不属于上面3层的log

缓冲区主要给系统组件使用，一般的应用不需要关心，应用的log都输出到main缓冲区中

默认log输出（不指定缓冲区的情况下）是输出System和Main缓冲区的log

实例：

```
adb logcat –b radio
adb logcat –b system
adb logcat –b events
adb logcat –b main
```

```
//将缓冲区的log打印到屏幕并退出
adb logcat -d 
//清除缓冲区log（testCase运行前可以先清除一下）
adb logcat -c
//打印缓冲区大小并退出
adb logcat -g
//输出log
adb logcat -f /data/local/tmp/log.txt -n 10 -r 1
```
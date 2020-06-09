1、查看当前活跃的activity栈
adb shell dumpsys activity activities | sed -En -e '/Running activities/,/Run #0/p'

2、查看特定应用启动的service
adb shell dumpsys activity s packageName

2、查询某个app的进程状态
adb shell dumpsys activity p packageName
1、查看当前活跃的activity栈
adb shell dumpsys activity activities | sed -En -e '/Running activities/,/Run #0/p'
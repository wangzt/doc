#小技巧

##Dialog Activity
* 如果设置了 getWindow().setLayout(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT); 则windowCloseOnTouchOutside 不起作用

##查看当前运行的activity
* adb shell dumpsys activity activities | sed -En -e '/Running activities/,/Run #0/p'

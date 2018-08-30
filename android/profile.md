#性能优化

#cpu性能
1. 查看当前线程使用情况

adb shell top -m 10 -t -d 2

表示前10个线程，2s更新一次
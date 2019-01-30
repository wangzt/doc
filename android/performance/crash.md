#Android 崩溃

**Android 中有两种崩溃:** Java 崩溃和 Native 崩溃。
**Java 崩溃就是在 Java 代码中，出现了未捕获异常，导致程序异常退出。**
**Native 崩溃一般都是因为在 Native 代码中访问非法地址，也可能是地址对齐出现问题，或者出现程序主动调用 abort ，这些都会产生相应的 signal 信号，导致程序异常退出。**




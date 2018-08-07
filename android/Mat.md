#MAT内存检测

##Retained Heap
Retained size是该对象自己的shallow size，加上从该对象能直接或间接访问到对象的shallow size之和。换句话说，retained size是该对象被GC之后所能回收到内存的总和。
相对于shallow heap，RetainedHeap可以更精确的反映一个对象实际占用的大小

##Retained Set
当X被回收时那些将被GC回收的对象集合。
比如: 一个ArrayList持有100,000个对象，每一个占用16 bytes，移除这些ArrayList可以释放16 x 100,000 + X，X代表ArrayList的shallow大小。相对于shallow heap，RetainedHeap可以更精确的反映一个对象实际占用的大小。

##Heap Dump
heap dump是特定时间点，java进程的内存快照。有不同的格式来存储这些数据，总的来说包含了快照被触发时java对象和类在heap中的情况。由于快照只是一瞬间的事情，所以heap dump中无法包含一个对象在何时、何地（哪个方法中）被分配这样的信息。

##Dominator Tree视图
Dominator Tree：对象之间dominator关系树。如果从GC Root到达Y的的所有path都经过X，那么我们称X dominates Y，或者X是Y的Dominator

##Path to GC Roots视图
查看一个对象到GC Roots的引用链
通常在排查内存泄漏的时候，我们会选择exclude all phantom/weak/soft etc.references,
意思是查看排除虚引用/弱引用/软引用等的引用链，因为被虚引用/弱引用/软引用的对象可以直接被GC给回收，我们要看的就是某个对象否还存在Strong 引用链（在导出HeapDump之前要手动出发GC来保证），如果有，则说明存在内存泄漏，然后再去排查具体引用。

##查看当前Object所有引用,被引用的对象：

List objects with （以Dominator Tree的方式查看）

incoming references 引用到该对象的对象
outcoming references 被该对象引用的对象

Show objects by class （以class的方式查看）

incoming references 引用到该对象的对象
outcoming references 被该对象引用的对象

##如何分析内存泄漏?
切记在导出prof文件前，先手动出发一次GC，这样可以确保只保存那些无法回收的对象内存快照 ，另外Android Studio提供自动转换
步骤：
1. 查找目标类
如果在开发过程中，你的目标很明确，比如就是查找自己负责的Activity，那么通过包名或者Class筛选，OQL搜索都可以快速定位到
OQL：
点击OQL图标,在窗口输入 select * from instanceof android.app.Activity 并按Ctrl + F5或者!按钮执行

2. Paths to GC Roots：exclude all phantom/weak/soft etc.references
查看一个对象到RC Roots是否存在引用链。要将虚引用/弱引用/软引用等排除，因为被虚引用/弱引用/软引用的对象可以直接被GC给回收

3. 分析具体的引用为何没有被释放，并进行修复
通过OQL快速定位未使用的集合
* 通过OQL查询empty并且未修改过的集合
```
select * from java.util.ArrayList where size=0 and modCount=0
类似的 
select * from java.util.HashMap where size=0 and modCount=0
select * from java.util.Hashtable where count=0 and modCount=0
```

* 查看使用activity实例
```
select * from instanceof android.app.Activity
select * from "packageName.main.activity.*"
```
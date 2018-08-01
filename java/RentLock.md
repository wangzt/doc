#可重入锁

##Java中常用可重入锁
* Syncnized
* ReentrantLock

##java中实现原子操作的类
* AtomicIntegerFieldUpdater:原子更新整型的字段的更新器
* AtomicLongFieldUpdater：原子更新长整型字段的更新器
* AtomicStampedReference:原子更新带有版本号的引用类型。该类将整型数值与引用关联起来，可用于原子的更新数据和数据的版本号，可以解决使用CAS进行原子更新时可能出现的ABA问题。
* AtomicReference ：原子更新引用类型
* AtomicReferenceFieldUpdater ：原子更新引用类型里的字段
* AtomicMarkableReference：原子更新带有标记位的引用类型。可以原子更新一个布尔类型的标记位和应用类型
* AtomicIntegerArray ：原子更新整型数组里的元素
* AtomicLongArray :原子更新长整型数组里的元素
* AtomicReferenceArray : 原子更新引用类型数组的元素
* AtomicBooleanArray ：原子更新布尔类型数组的元素
* AtomicBoolean ：原子更新布尔类型
* AtomicInteger： 原子更新整型
* AtomicLong: 原子更新长整型

[百度](https://www.baidu.com)

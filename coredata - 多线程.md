# CoreData - 并发

---
by Rusher @ 2013-07-25


不要阻塞主线程，这应该是GUI的编程里的最基本的原则了。所以，我们需要在UI所在的主线程之外，建立其他线程，在上面完成网络数据的加载，存储任务，然后在主线程上更新UI。使用CoreData作为数据存取面临的一个问题是，`NSManageObjectContext`不是线程安全的，。你要在线程上建立一个context，多出的managedObject，那再另外的线程上就不能使用，managedObject必需和获取它的context在同一个线程上使用。 最常用的解决方法是：在主线程建立一个`NSManageObjectContext`实例负责读取信息,在子线程中再建立一个`NSManageObjectContext`实例，负责数据的更新。多个`NSManagedObjectContext`公用一个``



[^1]: [Apple Developer Doc: Concurrency with Core Data](https://developer.apple.com/library/ios/#documentation/Cocoa/Conceptual/CoreData/Articles/cdConcurrency.html#//apple_ref/doc/uid/TP40003385-SW1)

[^2]: [Apple Sample Code: ThreadedCoreData](https://developer.apple.com/library/ios/#samplecode/ThreadedCoreData/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010723)
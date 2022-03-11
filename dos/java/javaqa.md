# dos
## java
### QA
#### p1
##### Multithreading
- What do you mean by Multithreading? Why is it important?
  Multithreading means multiple threads and is considered one of the most important features of Java. As the name suggests, it is the ability of a CPU to execute multiple threads independently at the same time but share the process resources simultaneously. Its main purpose is to provide simultaneous execution of multiple threads to utilize the CPU time as much as possible. It is a Java feature where one can subdivide the specific program into two or more threads to make the execution of the program fast and easy.
- Multithreading Interview Questions in Java for Freshers
1. What are the benefits of using Multithreading?
   There are various benefits of multithreading as given below:

Allow the program to run continuously even if a part of it is blocked.
Improve performance as compared to traditional parallel programs that use multiple processes.
Allows to write effective programs that utilize maximum CPU time
Improves the responsiveness of complex applications or programs.
Increase use of CPU resources and reduce costs of maintenance.
Saves time and parallelism tasks.
If an exception occurs in a single thread, it will not affect other threads as threads are independent.
Less resource-intensive than executing multiple processes at the same time.
2. What is Thread in Java?
   Threads are basically the lightweight and smallest unit of processing that can be managed independently by a scheduler. Threads are referred to as parts of a process that simply let a program execute efficiently with other parts or threads of the process at the same time. Using threads, one can perform complicated tasks in the easiest way. It is considered the simplest way to take advantage of multiple CPUs available in a machine. They share the common address space and are independent of each other.

3. What are the two ways of implementing thread in Java?
   There are basically two ways of implementing thread in java as given below:

Extending the Thread class
Example:

class MultithreadingDemo extends Thread
{   
public void run()
{   
System.out.println("My thread is in running state.");    
}
public static void main(String args[])
{   
MultithreadingDemoobj=new MultithreadingDemo();  
obj.start();  
}  
}
Output:

My thread is in running state.
Implementing Runnable interface in Java
Example:

class MultithreadingDemo implements Runnable
{  
public void run()
{  
System.out.println("My thread is in running state.");  
}  
public static void main(String args[])
{  
MultithreadingDemo obj=new MultithreadingDemo();   
Threadtobj =new Thread(obj);       tobj.start();  
}   
}
Output:

My thread is in running state.

4. What's the difference between thread and process?
   Thread: It simply refers to the smallest units of the particular process. It has the ability to execute different parts (referred to as thread) of the program at the same time.

Process: It simply refers to a program that is in execution i.e., an active program. A process can be handled using PCB (Process Control Block).


Thread	Process
It is a subset of a subunit of a process.	It is a program in execution containing multiple threads.
In this, inter-thread communication is faster, less expensive, easy and efficient because threads share the same memory address of the process they belong to. 	In this, inter-process communication is slower, expensive, and complex because each process has different memory space or address.,
These are easier to create, lightweight, and have less overhead. 	These are difficult to create, heavyweight, and have more overhead.
It requires less time for creation, termination, and context switching.	It requires more time for creation, termination, and context switching.
Processes with multiple threads use fewer resources.	Processes without threads use more resources.
Threads are parts of a process, so they are dependent on each other but each thread executes independently.	Processes are independent of each other.
There is a need for synchronization in threads to avoid unexpected scenarios or problems.	There is no need for synchronization in each process.
They share data and information with each other. 	They do not share data with each other.
5. What’s the difference between class lock and object lock?
   Class Lock: In java, each and every class has a unique lock usually referred to as a class level lock. These locks are achieved using the keyword ‘static synchronized’ and can be used to make static data thread-safe. It is generally used when one wants to prevent multiple threads from entering a synchronized block.

Example:

public class ClassLevelLockExample  
{    
public void classLevelLockMethod()  
{       
synchronized (ClassLevelLockExample.class)  
{         
//DO your stuff here       
}    
}
}
Object Lock: In java, each and every object has a unique lock usually referred to as an object-level lock. These locks are achieved using the keyword ‘synchronized’ and can be used to protect non-static data. It is generally used when one wants to synchronize a non-static method or block so that only the thread will be able to execute the code block on a given instance of the class.

Example:

public class ObjectLevelLockExample  
{    
public void objectLevelLockMethod()  
{   
synchronized (this)  
{     
//DO your stuff here   
}
}
}
6. What's the difference between User thread and Daemon thread?
   User and Daemon are basically two types of thread used in Java by using a ‘Thread Class’.

User Thread (Non-Daemon Thread): In Java, user threads have a specific life cycle and its life is independent of any other thread. JVM (Java Virtual Machine) waits for any of the user threads to complete its tasks before terminating it. When user threads are finished, JVM terminates the whole program along with associated daemon threads.

Daemon Thread: In Java, daemon threads are basically referred to as a service provider that provides services and support to user threads. There are basically two methods available in thread class for daemon thread: setDaemon() and isDaemon().

User Thread vs Daemon Thread

User Thread	Daemon Thread
JVM waits for user threads to finish their tasks before termination. 	JVM does not wait for daemon threads to finish their tasks before termination.
These threads are normally created by the user for executing tasks concurrently. 	These threads are normally created by JVM.
They are used for critical tasks or core work of an application. 	They are not used for any critical tasks but to do some supporting tasks.
These threads are referred to as high-priority tasks, therefore are required for running in the foreground. 	These threads are referred to as low priority threads, therefore are especially required for supporting background tasks like garbage collection, releasing memory of unused objects, etc.
7. How can we create daemon threads?
   We can create daemon threads in java using the thread class setDaemon(true). It is used to mark the current thread as daemon thread or user thread. isDaemon() method is generally used to check whether the current thread is daemon or not. If the thread is a daemon, it will return true otherwise it returns false.  
   Example:   
   Program to illustrate the use of setDaemon() and isDaemon() method.

public class DaemonThread extends Thread
{
public DaemonThread(String name){
super(name);
}
public void run()
{  
// Checking whether the thread is Daemon or not
if(Thread.currentThread().isDaemon())
{  
System.out.println(getName() + " is Daemon thread");  
}    
else
{  
System.out.println(getName() + " is User thread");  
}  
}   
public static void main(String[] args)
{  
DaemonThread t1 = new DaemonThread("t1");
DaemonThread t2 = new DaemonThread("t2");
DaemonThread t3 = new DaemonThread("t3");  
// Setting user thread t1 to Daemon
t1.setDaemon(true);       
// starting first 2 threads  
t1.start();  
t2.start();   
// Setting user thread t3 to Daemon
t3.setDaemon(true);  
t3.start();         
}  
}
Output:

t1 is Daemon thread
t3 is Daemon thread
t2 is User thread
But one can only call the setDaemon() method before start() method otherwise it will definitely throw IllegalThreadStateException as shown below:

public class DaemonThread extends Thread
{
public void run()
{
System.out.println("Thread name: " + Thread.currentThread().getName());
System.out.println("Check if its DaemonThread: "  
+ Thread.currentThread().isDaemon());
}
public static void main(String[] args)
{
DaemonThread t1 = new DaemonThread();
DaemonThread t2 = new DaemonThread();
t1.start();         
// Exception as the thread is already started
t1.setDaemon(true);
t2.start();
}
}
Output:

Thread name: Thread-0
Check if its DaemonThread: false
8. What are the wait() and sleep() methods?
   wait(): As the name suggests, it is a non-static method that causes the current thread to wait and go to sleep until some other threads call the notify () or notifyAll() method for the object’s monitor (lock). It simply releases the lock and is mostly used for inter-thread communication. It is defined in the object class, and should only be called from a synchronized context.

Example:

synchronized(monitor)
{
monitor.wait();       Here Lock Is Released by Current Thread  
}
sleep(): As the name suggests, it is a static method that pauses or stops the execution of the current thread for some specified period. It doesn’t release the lock while waiting and is mostly used to introduce pause on execution. It is defined in thread class, and no need to call from a synchronized context.

Example:

synchronized(monitor)
{
Thread.sleep(1000);     Here Lock Is Held by The Current Thread
//after 1000 milliseconds, the current thread will wake up, or after we call that is interrupt() method
}
9. What’s the difference between notify() and notifyAll()?
   notify(): It sends a notification and wakes up only a single thread instead of multiple threads that are waiting on the object’s monitor.


notifyAll(): It sends notifications and wakes up all threads and allows them to compete for the object's monitor instead of a single thread.


10. Why wait(), notify(), and notifyAll() methods are present in Object class?
    We know that every object has a monitor that allows the thread to hold a lock on the object. But the thread class doesn't contain any monitors. Thread usually waits for the object’s monitor (lock) by calling the wait() method on an object, and notify other threads that are waiting for the same lock using notify() or notifyAll() method.  Therefore, these three methods are called on objects only and allow all threads to communicate with each that are created on that object.

11. What is Runnable and Callable Interface? Write the difference between them.
    Both the interfaces are generally used to encapsulate tasks that are needed to be executed by another thread. But there are some differences between them as given below:

Running Interface: This interface is basically available in Java right from the beginning. It is simply used to execute code on a concurrent thread.  
Callable Interface: This interface is basically a new one that was introduced as a part of the concurrency package. It addresses the limitation of runnable interfaces along with some major changes like generics, enum, static imports, variable argument method, etc. It uses generics to define the return type of object.

public interface Runnable  
{   
public abstract void run();
}  
public interface Callable<V>  
{    
V call() throws Exception;  
}
Runnable Interface vs Callable Interface

Runnable Interface	Callable Interface
It does not return any result and therefore, cannot throw a checked exception. 	It returns a result and therefore, can throw an exception.
It cannot be passed to invokeAll method. 	It can be passed to invokeAll method.
It was introduced in JDK 1.0.	It was introduced in JDK 5.0, so one cannot use it before Java 5.
It simply belongs to Java.lang.	It simply belongs to java.util.concurrent.
It uses the run() method to define a task.	It uses the call() method to define a task.
To use this interface, one needs to override the run() method. 	To use this interface, one needs to override the call() method.
12. What is the start() and run() method of Thread class?
    start(): In simple words, the start() method is used to start or begin the execution of a newly created thread. When the start() method is called, a new thread is created and this newly created thread executes the task that is kept in the run() method. One can call the start() method only once.

run(): In simple words, the run() method is used to start or begin the execution of the same thread. When the run() method is called, no new thread is created as in the case of the start() method. This method is executed by the current thread. One can call the run() method multiple times.

13. Explain thread pool?
    A Thread pool is simply a collection of pre-initialized or worker threads at the start-up that can be used to execute tasks and put back in the pool when completed. It is referred to as pool threads in which a group of fixed-size threads is created.  By reducing the number of application threads and managing their lifecycle, one can mitigate the issue of performance using a thread pool. Using threads, performance can be enhanced and better system stability can occur. To create the thread pools, java.util.concurrent.Executors class usually provides factory methods.

14. What’s the purpose of the join() method?
    join() method is generally used to pause the execution of a current thread unless and until the specified thread on which join is called is dead or completed. To stop a thread from running until another thread gets ended, this method can be used. It joins the start of a thread execution to the end of another thread’s execution. It is considered the final method of a thread class.

15. What do you mean by garbage collection?
    Garbage collection is basically a process of managing memory automatically. It uses several GC algorithms among which the popular one includes Mark and Sweep. The process includes three phases i.e., marking, deletion, and compaction/copying. In simple words, a garbage collector finds objects that are no longer required by the program and then delete or remove these unused objects to free up the memory space.

16. Explain the meaning of the deadlock and when it can occur?
    Deadlock, as the name suggests, is a situation where multiple threads are blocked forever. It generally occurs when multiple threads hold locks on different resources and are waiting for other resources to complete their task.


The above diagram shows a deadlock situation where two threads are blocked forever.  Thread 1 is holding Object 1 but needs object 2 to complete processing whereas Thread 2 is holding Object 2 but needs object 1 first. In such conditions, both of them will hold lock forever and will never complete tasks.

17. Explain volatile variables in Java?
    A volatile variable is basically a keyword that is used to ensure and address the visibility of changes to variables in multithreaded programming. This keyword cannot be used with classes and methods, instead can be used with variables. It is simply used to achieve thread-safety. If you mark any variable as volatile, then all the threads can read its value directly from the main memory rather than CPU cache, so that each thread can get an updated value of the variable.

18. How do threads communicate with each other?
    Threads can communicate using three methods i.e., wait(), notify(), and notifyAll().

19. Can two threads execute two methods (static and non-static concurrently)?
    Yes, it is possible. If both the threads acquire locks on different objects, then they can execute concurrently without any problem.

20. What is the purpose of the finalize() method?
    Finalize() method is basically a method of Object class specially used to perform cleanup operations on unmanaged resources just before garbage collection. It is not at all intended to be called a normal method. After the complete execution of finalize() method, the object gets destroyed automatically.

Multithreading Interview Questions in Java for Experienced
21. What is the synchronization process? Why use it?
    Synchronization is basically a process in java that enables a simple strategy for avoiding thread interference and memory consistency errors. This process makes sure that resource will be only used one thread at a time when one thread tries to access a shared resource. It can be achieved in three different ways as given below:

By the synchronized method
By synchronized block
By static synchronization
Syntax:

synchronized (object)
{        
//statement to be synchronized
}
22. What is synchronized method and synchronized block? Which one should be preferred?
    Synchronized Method: In this method, the thread acquires a lock on the object when they enter the synchronized method and releases the lock either normally or by throwing an exception when they leave the method.  No other thread can use the whole method unless and until the current thread finishes its execution and release the lock. It can be used when one wants to lock on the entire functionality of a particular method.

Synchronized Block: In this method, the thread acquires a lock on the object between parentheses after the synchronized keyword, and releases the lock when they leave the block. No other thread can acquire a lock on the locked object unless and until the synchronized block exists. It can be used when one wants to keep other parts of the programs accessible to other threads.

Synchronized blocks should be preferred more as it boosts the performance of a particular program. It only locks a certain part of the program (critical section) rather than the entire method and therefore leads to less contention.

23. What is thread starvation?
    Thread starvation is basically a situation or condition where a thread won’t be able to have regular access to shared resources and therefore is unable to proceed or make progress. This is because other threads have high priority and occupy the resources for too long. This usually happens with low-priority threads that do not get CPU for its execution to carry on.


24. What is Livelock? What happens when it occurs?
    Similar to deadlock, livelock is also another concurrency problem. In this case, the state of threads changes between one another without making any progress. Threads are not blocked but their execution is stopped due to the unavailability of resources.

25. What is BlockingQueue?
    BlockingQueue basically represents a queue that is thread-safe. Producer thread inserts resource/element into the queue using put() method unless it gets full and consumer thread takes resources from the queue using take() method until it gets empty. But if a thread tries to dequeue from an empty queue, then a particular thread will be blocked until some other thread inserts an item into the queue, or if a thread tries to insert an item into a queue that is already full, then a particular thread will be blocked until some threads take away an item from the queue.


Example:

package org.arpit.java2blog;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class BlockingQueuePCExample {

public static void main(String[] args) {

       BlockingQueue<String> queue=new ArrayBlockingQueue<>(5); 
       Producer producer=new Producer(queue); 
       Consumer consumer=new Consumer(queue); 
       Thread producerThread = new Thread(producer); 
       Thread consumerThread = new Thread(consumer); 
 
       producerThread.start(); 
       consumerThread.start(); 

}

static class Producer implements Runnable {

       BlockingQueue<String> queue=null; 
 
       public Producer(BlockingQueue queue) { 
           super(); 
           this.queue = queue; 
       } 
 
       @Override 
       public void run() { 
 
               try { 
                   System.out.println("Producing element 1"); 
                   queue.put("Element 1"); 
                   Thread.sleep(1000); 
                   System.out.println("Producing element 2"); 
                   queue.put("Element 2"); 
                   Thread.sleep(1000); 
                   System.out.println("Producing element 3"); 
                   queue.put("Element 3"); 
               } catch (InterruptedException e) { 
 
                   e.printStackTrace(); 
               } 
       } 
}

static class Consumer implements Runnable {

       BlockingQueue<String> queue=null; 
 
       public Consumer(BlockingQueue queue) { 
           super(); 
           this.queue = queue; 
       } 
 
       @Override 
       public void run() { 
 
           while(true) 
           { 
               try { 
                   System.out.println("Consumed "+queue.take()); 
               } catch (InterruptedException e) { 
                   e.printStackTrace(); 
               } 
           } 
       } 

}
}
Output:

Producing element 1
Consumed Element 1
Producing element 2
Consumed Element 2
Producing element 3
Consumed Element 3
26. Can you start a thread twice?
    No, it's not at all possible to restart a thread once a thread gets started and completes its execution. Thread only runs once and if you try to run it for a second time, then it will throw a runtime exception i.e., java.lang.IllegalThreadStateException.

Example:

public class TestThreadTwice1 extends Thread{   
public void run(){   
System.out.println(" thread is executing now........");   
}   
public static void main(String args[]){   
TestThreadTwice1 t1=new TestThreadTwice1();   
t1.start();   
t1.start();   
}   
}   
Output:

thread is executing now........
Exception in thread "main" java.lang.IllegalThreadStateException
27. Explain context switching.
    Context switching is basically an important feature of multithreading. It is referred to as switching of CPU from one thread or process to another one. It allows multiple processes to share the same CPU. In context switching, the state of thread or process is stored so that the execution of the thread can be resumed later if required.

28. What is CyclicBarrier and CountDownLatch?
    CyclicBarrier and CountDownLatch, both are required for managing multithreaded programming. But there is some difference between them as given below:

CyclicBarrier: It is a tool to synchronize threads processing using some algorithm. It enables a set of threads to wait for each other till they reach a common execution point or common barrier points, and then let them further continue execution. One can reuse the same CyclicBarrier even if the barrier is broken by setting it.

CountDownLatch: It is a tool that enables main threads to wait until mandatory operations are performed and completed by other threads. In simple words, it makes sure that a thread waits until the execution in another thread completes before it starts its execution. One cannot reuse the same CountDownLatch once the count reaches 0.


29. What do you mean by inter-thread communication?
    Inter-thread communication, as the name suggests, is a process or mechanism using which multiple threads can communicate with each other. It is especially used to avoid thread polling in java and can be obtained using wait(), notify(), and notifyAll() methods.

30. What is Thread Scheduler and Time Slicing?
    Thread Scheduler: It is a component of JVM that is used to decide which thread will execute next if multiple threads are waiting to get the chance of execution. By looking at the priority assigned to each thread that is READY, the thread scheduler selects the next run to execute. To schedule the threads, it mainly uses two mechanisms: Preemptive Scheduling and Time slicing scheduling.

Time Slicing: It is especially used to divide CPU time and allocate them to active threads. In this, each thread will get a predefined slice of time to execute. When the time expires, a particular thread has to wait till other threads get their chances to use their time in a round-robin fashion. Every running thread will get executed for a fixed time period.

31. What is a shutdown hook?
    A shutdown hook is simply a thread that is invoked implicitly before JVM shuts down. It is one of the most important features of JVM because it provides the capacity to do resource cleanup or save application state JVM shuts down.  By calling the halt(int) method of the Runtime class, the shutdown hook can be stopped. Using the following method, one can add a shutdown hook.

public void addShutdownHook(Thread hook){}     
Runtime r=Runtime.getRuntime();   
r.addShutdownHook(new MyThread());
32. What is busy spinning?
    Busy Spinning, also known as Busy-waiting, is a technique in which one thread waits for some condition to happen, without calling wait or sleep methods and releasing the CPU. In this condition, one can pause a thread by making it run an empty loop for a certain time period, and it does not even give CPY control. Therefore, it is used to preserve CPU caches and avoid the cost of rebuilding cache.

33. What is ConcurrentHashMap and Hashtable? In java, why is ConcurrentHashMap considered faster than Hashtable?
    ConcurrentHashMap: It was introduced in Java 1.5 to store data using multiple buckets. As the name suggests, it allows concurrent read and writes operations to the map. It only locks a certain portion of the map while doing iteration to provide thread safety so that other readers can still have access to the map without waiting for iteration to complete.

Hashtable: It is a thread-safe legacy class that was introduced in old versions of java to store key or value pairs using a hash table.  It does not provide any lock-free read, unlike ConcurrentHashMap. It just locks the entire map while doing iteration.

ConcurrentHashMap and Hashtable, both are thread-safe but ConcurrentHashMap generally avoids read locks and improves performance, unlike Hashtable. ConcurrentHashMap also provides lock-free reads, unlike Hashtable. Therefore, ConcurrentHashMap is considered faster than Hashtable especially when the number of readers is more as compared to the number of writers.

34. Explain thread priority.
    Thread priority simply means that threads with the highest priority will get a chance for execution prior to low-priority threads. One can specify the priority but it's not necessary that the highest priority thread will get executed before the lower-priority thread. Thread scheduler assigns processor to thread on the basis of thread priority. The range of priority changes between 1-10 from lowest priority to highest priority.


35. What do you mean by the ThreadLocal variable in Java?
    ThreadLocal variables are special kinds of variables created and provided by the Java ThreadLocal class. These variables are only allowed to be read and written by the same thread. Two threads cannot be able to see each other’s ThreadLocal variable, so even if they will execute the same code, then there won't be any race condition and the code will be thread-safe.

Example:

public class ThreadLocalExp   
{   
public static class MyRunnable implements Runnable    
{   
private ThreadLocal<Integer> threadLocal =   
new ThreadLocal<Integer>();   
@Override   
public void run() {   
threadLocal.set( (int) (Math.random() * 50D) );   
try    
{   
Thread.sleep(1000);   
} catch (InterruptedException e) {   
}   
System.out.println(threadLocal.get());   
}   
}   
public static void main(String[] args)    
{   
MyRunnable runnableInstance = new MyRunnable();    
Thread t1 = new Thread(runnableInstance);   
Thread t2 = new Thread(runnableInstance);   
// this will call run() method    
t1.start();   
t2.start();   
}   
}
Output:

10
33
10 33
36. What is semaphore?
    Semaphore is regarded as a thread synchronization construct that is usually required to control and manage the access to the shared resource using counters. It simply sets the limit of the thread. The semaphore class is defined within the package java.util.concurrent and can be used to send signals between threads to avoid missed signals or to guard critical sections. It can also be used to implement resource pools or bounded collection.

37. Explain Thread Group. Why should we not use it?
    ThreadGroup is a class that is used to create multiple groups of threads in a single object. This group of threads is present in the form of three structures in which every thread group has a parent except the initial thread. Thread groups can contain other thread groups also. A thread is only allowed to have access to information about its own thread group, not other thread groups.

Previously in the old version of Java, the only functionality that did not work without a thread group was uncaughtException( Thread t, Throwable e). But now in Java 5 versions, there is Thread.setUncaughtExceptionHandler(UncaughtExceptionHandler). So now even that works without thread groups and therefore, there is no need to use thread groups.

t1.setUncaughtExceptionHandler(new UncaughtExceptionHandler()
{
@Override  
public void uncaughtException(Thread t, Throwable e)  
{  
System.out.println("exception occured:"+e.getMessage());
}  
};
38. What is the ExecutorService interface?
    ExecutorService interface is basically a sub-interface of Executor interface with some additional methods or features that help in managing and controlling the execution of threads. It enables us to execute tasks asynchronously on threads.


Example:

import java.util.concurrent.ExecutorService;   
import java.util.concurrent.Executors;   
import java.util.concurrent.TimeUnit;

public class TestThread {   
public static void main(final String[] arguments) throws InterruptedException {   
ExecutorService e = Executors.newSingleThreadExecutor();

     try {   
       e.submit(new Thread());   
        System.out.println("Shutdown executor");   
        e.shutdown();   
        e.awaitTermination(5, TimeUnit.SECONDS);   
} catch (InterruptedException ex) {   
System.err.println("tasks interrupted");   
} finally {

        if (!e.isTerminated()) {   
           System.err.println("cancel non-finished tasks");   
     }   
        e.shutdownNow();   
        System.out.println("shutdown finished");   
}   
}

static class Task implements Runnable {

     public void run() {   
          
        try {   
        Long duration = (long) (Math.random() * 20);   
           System.out.println("Running Task!");   
           TimeUnit.SECONDS.sleep(duration);   
     } catch (InterruptedException ex) {   
           ex.printStackTrace();   
     }   
}   
}          
}   
Output:

Shutdown executor
shutdown finished
39. What will happen if we don’t override the thread class run() method?
    Nothing will happen as such if we don’t override the run() method. The compiler will not show any error. It will execute the run() method of thread class and we will just don’t get any output because the run() method is with an empty implementation.

Example:

class MyThread extends Thread {
//don't override run() method
}
public class DontOverrideRun {
public static void main(String[] args) {
System.out.println("Started Main.");
MyThread thread1=new MyThread();
thread1.start();
System.out.println("Ended Main.");
}
}
Output:

Started Main.
Ended Main.
40. What is the lock interface? Why is it better to use a lock interface rather than a synchronized block.?
    Lock interface was introduced in Java 1.5 and is generally used as a synchronization mechanism to provide important operations for blocking.

Advantages of using Lock interface over Synchronization block:

Methods of Lock interface i.e., Lock() and Unlock() can be called in different methods. It is the main advantage of a lock interface over a synchronized block because the synchronized block is fully contained in a single method.  
Lock interface is more flexible and makes sure that the longest waiting thread gets a fair chance for execution, unlike the synchronization block.
41. Is it possible to call the run() method directly to start a new thread?
    No, it's not possible at all. You need to call the start method to create a new thread otherwise run method won't create a new thread. Instead, it will execute in the current thread.

42. Is it possible that each thread can have its stack in multithreaded programming?
    Of course, it is possible. In multithreaded programming, each thread maintains its own separate stack area in memory because of which every thread is independent of each other rather than dependent.

Conclusion
43. Conclusion
    Overall, multithreading is a very essential part of Java and modern software development. It is very helpful in making the program more efficient and also reduces the usage of storage resources. In this article, we have discussed important interview questions related to multithreading along with answers that were asked mostly in the Interviews and will help you to crack your interviews.

Recommended Tutorials:
Practice
Java Developer Skills

#### p1
##### HashMap
- 1.：HashMap 的数据结构？
  A：哈希表结构（链表散列：数组+链表）实现，结合数组和链表的优点。当链表长度超过 8 时，链表转换为红黑树。

transient Node<K,V>\[\] table;
- 2.：HashMap 的工作原理？
HashMap 底层是 hash 数组和单向链表实现，数组中的每个元素都是链表，由 Node 内部类（实现 Map.Entry接口）实现，HashMap 通过 put & get 方法存储和获取。

存储对象时，将 K/V 键值传给 put() 方法：

①、调用 hash(K) 方法计算 K 的 hash 值，然后结合数组长度，计算得数组下标；

②、调整数组大小（当容器中的元素个数大于 capacity * loadfactor 时，容器会进行扩容resize 为 2n）；

③、i.如果 K 的 hash 值在 HashMap 中不存在，则执行插入，若存在，则发生碰撞；

ii.如果 K 的 hash 值在 HashMap 中存在，且它们两者 equals 返回 true，则更新键值对；

iii. 如果 K 的 hash 值在 HashMap 中存在，且它们两者 equals 返回 false，则插入链表的尾部（尾插法）或者红黑树中（树的添加方式）。

（JDK 1.7 之前使用头插法、JDK 1.8 使用尾插法）（注意：当碰撞导致链表大于 TREEIFY_THRESHOLD = 8 时，就把链表转换成红黑树）

获取对象时，将 K 传给 get() 方法：①、调用 hash(K) 方法（计算 K 的 hash 值）从而获取该键值所在链表的数组下标；②、顺序遍历链表，equals()方法查找相同 Node 链表中 K 值对应的 V 值。

hashCode 是定位的，存储位置；equals是定性的，比较两者是否相等。

- 3.当两个对象的 hashCode 相同会发生什么？
因为 hashCode 相同，不一定就是相等的（equals方法比较），所以两个对象所在数组的下标相同，"碰撞"就此发生。又因为 HashMap 使用链表存储对象，这个 Node 会存储到链表中。

- 4.你知道 hash 的实现吗？为什么要这样实现？
JDK 1.8 中，是通过 hashCode() 的高 16 位异或低 16 位实现的：(h = k.hashCode()) ^ (h >>> 16)，主要是从速度，功效和质量来考虑的，减少系统的开销，也不会造成因为高位没有参与下标的计算，从而引起的碰撞。

- 5.为什么要用异或运算符？
保证了对象的 hashCode 的 32 位值只要有一位发生改变，整个 hash() 返回值就会改变。尽可能的减少碰撞。

- 6.HashMap 的 table 的容量如何确定？loadFactor 是什么？该容量如何变化？这种变化会带来什么问题？
①、table 数组大小是由 capacity 这个参数确定的，默认是16，也可以构造时传入，最大限制是1<<30；

②、loadFactor 是装载因子，主要目的是用来确认table 数组是否需要动态扩展，默认值是0.75，比如table 数组大小为 16，装载因子为 0.75 时，threshold 就是12，当 table 的实际大小超过 12 时，table就需要动态扩容；

③、扩容时，调用 resize() 方法，将 table 长度变为原来的两倍（注意是 table 长度，而不是 threshold）

④、如果数据很大的情况下，扩展时将会带来性能的损失，在性能要求很高的地方，这种损失很可能很致命。

- 7.HashMap中put方法的过程？
答：“调用哈希函数获取Key对应的hash值，再计算其数组下标；

如果没有出现哈希冲突，则直接放入数组；如果出现哈希冲突，则以链表的方式放在链表后面；

如果链表长度超过阀值( TREEIFY THRESHOLD==8)，就把链表转成红黑树，链表长度低于6，就把红黑树转回链表;

如果结点的key已经存在，则替换其value即可；

如果集合中的键值对大于12，调用resize方法进行数组扩容。”

- 8.数组扩容的过程？
创建一个新的数组，其容量为旧数组的两倍，并重新计算旧数组中结点的存储位置。结点在新数组中的位置只有两种，原下标位置或原下标+旧数组的大小。

- 9.拉链法导致的链表过深问题为什么不用二叉查找树代替，而选择红黑树？为什么不一直使用红黑树？
之所以选择红黑树是为了解决二叉查找树的缺陷，二叉查找树在特殊情况下会变成一条线性结构（这就跟原来使用链表结构一样了，造成很深的问题），遍历查找会非常慢。推荐：面试问红黑树，我脸都绿了。

而红黑树在插入新数据后可能需要通过左旋，右旋、变色这些操作来保持平衡，引入红黑树就是为了查找数据快，解决链表查询深度的问题，我们知道红黑树属于平衡二叉树，但是为了保持“平衡”是需要付出代价的，但是该代价所损耗的资源要比遍历线性链表要少，所以当长度大于8的时候，会使用红黑树，如果链表长度很短的话，根本不需要引入红黑树，引入反而会慢。

- 10.说说你对红黑树的见解？
每个节点非红即黑
根节点总是黑色的
如果节点是红色的，则它的子节点必须是黑色的（反之不一定）
每个叶子节点都是黑色的空节点（NIL节点）
从根节点到叶节点或空子节点的每条路径，必须包含相同数目的黑色节点（即相同的黑色高度）
- 11.jdk8中对HashMap做了哪些改变？
在java 1.8中，如果链表的长度超过了8，那么链表将转换为红黑树。（桶的数量必须大于64，小于64的时候只会扩容）

发生hash碰撞时，java 1.7 会在链表的头部插入，而java 1.8会在链表的尾部插入

在java 1.8中，Entry被Node替代(换了一个马甲。

- 12.HashMap，LinkedHashMap，TreeMap 有什么区别？
LinkedHashMap 保存了记录的插入顺序，在用 Iterator 遍历时，先取到的记录肯定是先插入的；遍历比 HashMap 慢；

TreeMap 实现 SortMap 接口，能够把它保存的记录根据键排序（默认按键值升序排序，也可以指定排序的比较器）

- 13.HashMap & TreeMap & LinkedHashMap 使用场景？
一般情况下，使用最多的是 HashMap。

HashMap：在 Map 中插入、删除和定位元素时；

TreeMap：在需要按自然顺序或自定义顺序遍历键的情况下；

LinkedHashMap：在需要输出的顺序和输入的顺序相同的情况下。

- 14.HashMap 和 HashTable 有什么区别？
①、HashMap 是线程不安全的，HashTable 是线程安全的；

②、由于线程安全，所以 HashTable 的效率比不上 HashMap；

③、HashMap最多只允许一条记录的键为null，允许多条记录的值为null，而 HashTable不允许；

④、HashMap 默认初始化数组的大小为16，HashTable 为 11，前者扩容时，扩大两倍，后者扩大两倍+1；

⑤、HashMap 需要重新计算 hash 值，而 HashTable 直接使用对象的 hashCode

- 15.Java 中的另一个线程安全的与 HashMap 极其类似的类是什么？同样是线程安全，它与 HashTable 在线程同步上有什么不同？
ConcurrentHashMap 类（是 Java并发包 java.util.concurrent 中提供的一个线程安全且高效的 HashMap 实现）。

HashTable 是使用 synchronize 关键字加锁的原理（就是对对象加锁）；

而针对 ConcurrentHashMap，在 JDK 1.7 中采用 分段锁的方式；JDK 1.8 中直接采用了CAS（无锁算法）+ synchronized。

- 16.HashMap & ConcurrentHashMap 的区别？
除了加锁，原理上无太大区别。另外，HashMap 的键值对允许有null，但是ConCurrentHashMap 都不允许。

- 17.为什么 ConcurrentHashMap 比 HashTable 效率要高？
HashTable 使用一把锁（锁住整个链表结构）处理并发问题，多个线程竞争一把锁，容易阻塞；

ConcurrentHashMap

JDK 1.7 中使用分段锁（ReentrantLock + Segment + HashEntry），相当于把一个 HashMap 分成多个段，每段分配一把锁，这样支持多线程访问。锁粒度：基于 Segment，包含多个 HashEntry。
JDK 1.8 中使用 CAS + synchronized + Node + 红黑树。锁粒度：Node（首结点）（实现 Map.Entry）。锁粒度降低了。
- 18.针对 ConcurrentHashMap 锁机制具体分析（JDK 1.7 VS JDK 1.8）
JDK 1.7 中，采用分段锁的机制，实现并发的更新操作，底层采用数组+链表的存储结构，包括两个核心静态内部类 Segment 和 HashEntry。

①、Segment 继承 ReentrantLock（重入锁） 用来充当锁的角色，每个 Segment 对象守护每个散列映射表的若干个桶；

②、HashEntry 用来封装映射表的键-值对；

③、每个桶是由若干个 HashEntry 对象链接起来的链表

Image
JDK 1.8 中，采用Node + CAS + Synchronized来保证并发安全。取消类 Segment，直接用 table 数组存储键值对；当 HashEntry 对象组成的链表长度超过 TREEIFY_THRESHOLD 时，链表转换为红黑树，提升性能。底层变更为数组 + 链表 + 红黑树。

Image
- 19.ConcurrentHashMap 在 JDK 1.8 中，为什么要使用内置锁 synchronized 来代替重入锁 ReentrantLock？
①、粒度降低了；

②、JVM 开发团队没有放弃 synchronized，而且基于 JVM 的 synchronized 优化空间更大，更加自然。

③、在大量的数据操作下，对于 JVM 的内存压力，基于 API 的 ReentrantLock 会开销更多的内存。

- 20.ConcurrentHashMap 简单介绍？
①、重要的常量：

private transient volatile int sizeCtl;

当为负数时，-1 表示正在初始化，-N 表示 N - 1 个线程正在进行扩容；

当为 0 时，表示 table 还没有初始化；

当为其他正数时，表示初始化或者下一次进行扩容的大小。

②、数据结构：

Node 是存储结构的基本单元，继承 HashMap 中的 Entry，用于存储数据；

TreeNode 继承 Node，但是数据结构换成了二叉树结构，是红黑树的存储结构，用于红黑树中存储数据；

TreeBin 是封装 TreeNode 的容器，提供转换红黑树的一些条件和锁的控制。

③、存储对象时（put() 方法）：

如果没有初始化，就调用 initTable() 方法来进行初始化；

如果没有 hash 冲突就直接 CAS 无锁插入；

如果需要扩容，就先进行扩容；

如果存在 hash 冲突，就加锁来保证线程安全，两种情况：一种是链表形式就直接遍历到尾端插入，一种是红黑树就按照红黑树结构插入；

如果该链表的数量大于阀值 8，就要先转换成红黑树的结构，break 再一次进入循环

如果添加成功就调用 addCount() 方法统计 size，并且检查是否需要扩容。

④、扩容方法 transfer()：默认容量为 16，扩容时，容量变为原来的两倍。

helpTransfer()：调用多个工作线程一起帮助进行扩容，这样的效率就会更高。

⑤、获取对象时（get()方法）：

计算 hash 值，定位到该 table 索引位置，如果是首结点符合就返回；

如果遇到扩容时，会调用标记正在扩容结点 ForwardingNode.find()方法，查找该结点，匹配就返回；

以上都不符合的话，就往下遍历结点，匹配就返回，否则最后就返回 null。

- 21.ConcurrentHashMap 的并发度是什么？
程序运行时能够同时更新 ConccurentHashMap 且不产生锁竞争的最大线程数。默认为 16，且可以在构造函数中设置。

当用户设置并发度时，ConcurrentHashMap 会使用大于等于该值的最小2幂指数作为实际并发度（假如用户设置并发度为17，实际并发度则为32）





### references
#### links
- <https://mp.weixin.qq.com/s/-e_x6P4ZTFMHkz3EWLvpSg>
- <https://www.interviewbit.com/multithreading-interview-questions>
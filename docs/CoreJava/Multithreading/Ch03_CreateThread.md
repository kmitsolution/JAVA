## How to create thread
There are two ways to create a thread:

1. By extending Thread class<br />
2. By implementing Runnable interface.<br />
### Thread class:
Thread class provide constructors and methods to create and perform operations on a thread.Thread class extends Object class and implements Runnable interface.

#### Commonly used Constructors of Thread class:
<ul>
  <li>Thread()</li>
  <li>Thread(String name)</li>
  <li>Thread(Runnable r)</li>
  <li>Thread(Runnable r,String name)</li>
  </ul>
  
### Commonly used methods of Thread class:
<ul>
 
<li>public void run(): is used to perform action for a thread.</li>
<li>public void start(): starts the execution of the thread.</li>JVM calls the run() method on the thread.</li>
<li>public void sleep(long miliseconds): Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds.</li>
<li>public void join(): waits for a thread to die.</li>
<li>public void join(long miliseconds): waits for a thread to die for the specified miliseconds.</li>
<li>public int getPriority(): returns the priority of the thread.</li>
<li>public int setPriority(int priority): changes the priority of the thread.</li>
<li>public String getName(): returns the name of the thread.</li>
<li>public void setName(String name): changes the name of the thread.</li>
<li>public Thread currentThread(): returns the reference of currently executing thread.</li>
<li>public int getId(): returns the id of the thread.</li>
<li>public Thread.</li>State getState(): returns the state of the thread.</li>
<li>public boolean isAlive(): tests if the thread is alive.</li>
<li>public void yield(): causes the currently executing thread object to temporarily pause and allow other threads to execute.</li>
<li>public void suspend(): is used to suspend the thread(depricated).</li>
<li>public void resume(): is used to resume the suspended thread(depricated).</li>
<li>public void stop(): is used to stop the thread(depricated).</li>
<li>public boolean isDaemon(): tests if the thread is a daemon thread.</li>
<li>public void setDaemon(boolean b): marks the thread as daemon or user thread.</li>
<li>public void interrupt(): interrupts the thread.</li>
<li>public boolean isInterrupted(): tests if the thread has been interrupted.</li>
<li>public static boolean interrupted(): tests if the current thread has been interrupted.</li>
</ul>

## Runnable interface:
The Runnable interface should be implemented by any class whose instances are intended to be executed by a thread. Runnable interface have only one method named run().

public void run(): is used to perform action for a thread.

### Starting a thread:
start() method of Thread class is used to start a newly created thread. It performs following tasks:

A new thread starts(with new callstack).

The thread moves from New state to the Runnable state.

When the thread gets a chance to execute, its target run() method will run.

### Java Thread Example by extending Thread class
```java
class Multi extends Thread{  
public void run(){  
System.out.println("thread is running...");  
}  
public static void main(String args[]){  
Multi t1=new Multi();  
t1.start();  
 }  
}  
```

### Java Thread Example by implementing Runnable interface
```java
class Multi3 implements Runnable{  
public void run(){  
System.out.println("thread is running...");  
}  
  
public static void main(String args[]){  
Multi3 m1=new Multi3();  
Thread t1 =new Thread(m1);  
t1.start();  
 }  
}  
```

If you are not extending the Thread class,your class object would not be treated as a thread object.So you need to explicitely create Thread class object.We are passing the object of your class that implements Runnable so that your class run() method may execute.

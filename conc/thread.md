./[curric](/curric)/[Concurrency](/curric/conc)/[Threads](/curric/conc/thread)/
# Threads (The Java Approach)
Multithreading is a Java feature that allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part of such program is called a thread.

There are three different types of Threads.

- Native Threads
    - Native Threads are Threads that, once created, are handled by the underlying operating system (OS) more commonly known as Kernel Threads. An upside to Kernel Threads is that when a Kernel Thread is blocked, other Kernel Threads can continue execution. 
- Green Threads
    - Green Threads are threads that are scheduled by a runtime library or virtual machine (VM) instead of natively by the underlying OS. Green threads emulate multithreaded environments without relying on any native OS abilities, and they are managed in user space instead of kernel space, enabling them to work in environments that do not have native thread support. In Java 1.1, green threads were the only threading model used by the Java virtual machine (JVM), at least on Solaris. As green threads have some limitations compared to native threads, subsequent Java versions dropped them in favor of native threads.
- Daemon Threads
    - Daemon thread is a low priority thread that runs in background to perform tasks such as garbage collection. They can not prevent the JVM from exiting when all the user threads finish their execution. JVM terminates itself when all user threads finish their execution. If JVM finds running daemon thread, it terminates the thread and after that shutdown itself. JVM does not care whether Daemon thread is running or not. It is an utmost low priority thread. An example of a Daemon Thread is Java Garbage Collection.

## Creating and Starting Threads in Java
Threads are apart of the Java Standard Library in java.lang. To import threads, use `import java.lang.Thread;`

To create Threads, invoke the Thread constructor with the new keyword. There are 8 different Thread constructors.

- `Thread()`
    - Allocates a new Thread object with an empty Runnable target.
- `Thread(Runnable target)`
    - Allocates a new Thread object with a target Runnable.
- `Thread(Runnable target, String name)`
    - Allocates a new Thread object with a target Runnable and with the replacement name.
- `Thread(String name)`
    - Allocates a new Thread object with an empty Runnable target with the replacement name.
- `Thread(ThreadGroup group, Runnable target)`
    - Allocates a new Thread object and ties it to the ThreadGroup with a target Runnable.
- `Thread(ThreadGroup group, Runnable target, String name)`
    - Allocates a new Thread object so that it has target as its run object, has the specified name as its name, and belongs to the thread group referred to by group.
- `Thread(ThreadGroup group, Runnable target, String name, long stackSize)`
    - Allocates a new Thread object so that it has target as its run object, has the specified name as its name, and belongs to the thread group referred to by group, and has the specified stack size.
- `Thread(ThreadGroup group, String name)`
    - Allocates a new Thread object and belongs to the ThreadGroup and with the replacement name.

The most common Thread constructor that you will use it the `Thread(Runnable Thread)`

In these next example, we will create a new thread that will print the current Thread's name and ID.

Here we extend the Thread class to create our custom Thread.
```java
import java.lang.Thread;

class ThreadDemo extends Thread {
  public void run() {
    System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
  }
}

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      ThreadDemo t = new ThreadDemo();
      // we call the default constructor 
      // we dont need to supply a Runnable object as
      // run function is already defined inside ThreadDemo
      // and that function will be the target function
      // that will be called when the Thread starts
      t.start();
    }
  }
}
```
Output (all will look relatively like this)
```
Name: Thread-6, ID: 16
Name: Thread-4, ID: 14
Name: Thread-2, ID: 12
Name: Thread-5, ID: 15
Name: Thread-1, ID: 11
Name: Thread-7, ID: 17
Name: Thread-3, ID: 13
Name: Thread-0, ID: 10
```

Here we implement the Runnable Interface to achieve the same output
```java
import java.lang.Thread;
import java.lang.Runnable;

class RunnableDemo implements Runnable {
  public void run() {
    System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
  }
}

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread(new RunnableDemo());
      // here we supply a Runnable in the one args constructor
      // the run function defined in the RunnableDemo class
      // will be used as the target run function called
      // when the thread is started
      t.start();
    }
  }
}
```

We can also use an anonymous class
```java
import java.lang.Thread;

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread() {
        public void run() {
          System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId());
        }
      };
      // here we create an anonymous thread class that 
      // overrides the run function
      // this run function will be used as the target function
      // when the Thread is started
      t.start();
    }
  }
}
```

Lastly, we can also use lambda syntax to create a new Thread
```java
import java.lang.Thread;

class Main {
  public static void main(String[] args) {
    int n = 8; // number of threads
    for (int i = 0; i < n; i++) {
      Thread t = new Thread(
        () -> System.out.println("Name: " + Thread.currentThread().getName() + ", ID: " + Thread.currentThread().getId())
      );
      // the lambda supplied is a SAM type 
      // of the functional interface Runnable
      // and the lambda function is the run function
      // that will be used as the target function by the thread when started
      t.start();
    }
  }
}
```

All of these examples are valid methods of creating new threads. However, some are sytactically easier than others. (_cough cough ~~lambda~~ cough cough_)
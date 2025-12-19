# Step 21: Multithreading Basics

## What is Multithreading?

**Multithreading** is a Java feature that allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part is called a **thread**.

### Key Concepts:
- **Process**: Independent program in execution (has its own memory)
- **Thread**: Lightweight sub-process, smallest unit of processing (shares memory)
- **Multitasking**: Multiple tasks at once
- **Multithreading**: Multiple threads within a single process

### Benefits:
- Better CPU utilization
- Improved responsiveness
- Resource sharing
- Parallel execution

---

## Thread Lifecycle

```
NEW → RUNNABLE → RUNNING → TERMINATED
         ↑           ↓
         ←  BLOCKED/WAITING
```

1. **NEW**: Thread created but not started
2. **RUNNABLE**: Ready to run, waiting for CPU
3. **RUNNING**: Executing
4. **BLOCKED/WAITING**: Waiting for resource or other thread
5. **TERMINATED**: Completed execution

---

## Creating Threads

### Method 1: Extending Thread Class

```java
class MyThread extends Thread {
    private String threadName;
    
    public MyThread(String name) {
        this.threadName = name;
    }
    
    @Override
    public void run() {
        System.out.println(threadName + " starting...");
        for (int i = 1; i <= 5; i++) {
            System.out.println(threadName + ": " + i);
            try {
                Thread.sleep(500);  // Sleep for 500ms
            } catch (InterruptedException e) {
                System.out.println(threadName + " interrupted");
            }
        }
        System.out.println(threadName + " terminating.");
    }
}

public class ThreadExtendExample {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread("Thread-1");
        MyThread thread2 = new MyThread("Thread-2");
        
        thread1.start();  // Starts the thread
        thread2.start();
        
        System.out.println("Main thread continues...");
    }
}
```

### Method 2: Implementing Runnable Interface (Preferred)

```java
class MyRunnable implements Runnable {
    private String threadName;
    
    public MyRunnable(String name) {
        this.threadName = name;
    }
    
    @Override
    public void run() {
        System.out.println(threadName + " starting...");
        for (int i = 1; i <= 5; i++) {
            System.out.println(threadName + ": " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println(threadName + " interrupted");
            }
        }
        System.out.println(threadName + " terminating.");
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Thread thread1 = new Thread(new MyRunnable("Thread-1"));
        Thread thread2 = new Thread(new MyRunnable("Thread-2"));
        
        thread1.start();
        thread2.start();
        
        System.out.println("Main thread continues...");
    }
}
```

### Method 3: Using Lambda Expression (Java 8+)

```java
public class LambdaThreadExample {
    public static void main(String[] args) {
        // Lambda for Runnable
        Thread thread1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread-1: " + i);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        
        Thread thread2 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread-2: " + i);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        
        thread1.start();
        thread2.start();
    }
}
```

---

## Thread Methods

```java
public class ThreadMethodsExample {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            System.out.println("Thread name: " + Thread.currentThread().getName());
            System.out.println("Thread ID: " + Thread.currentThread().getId());
            System.out.println("Thread priority: " + Thread.currentThread().getPriority());
            System.out.println("Is alive: " + Thread.currentThread().isAlive());
            
            for (int i = 1; i <= 3; i++) {
                System.out.println("Count: " + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        
        // Setting thread properties
        thread.setName("MyWorkerThread");
        thread.setPriority(Thread.MAX_PRIORITY);  // 1-10, default 5
        
        System.out.println("=== Before start() ===");
        System.out.println("Is alive: " + thread.isAlive());
        
        thread.start();
        
        System.out.println("\n=== After start() ===");
        System.out.println("Is alive: " + thread.isAlive());
        
        // Join - wait for thread to complete
        try {
            thread.join();  // Main thread waits for thread to finish
            System.out.println("\n=== After thread completion ===");
            System.out.println("Is alive: " + thread.isAlive());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Main thread ends.");
    }
}
```

---

## Synchronization

**Synchronization** controls access to shared resources by multiple threads to prevent data inconsistency.

```java
class Counter {
    private int count = 0;
    
    // Without synchronization - race condition
    public void increment() {
        count++;
    }
    
    // With synchronization - thread-safe
    public synchronized void synchronizedIncrement() {
        count++;
    }
    
    public int getCount() {
        return count;
    }
}

public class SynchronizationExample {
    public static void main(String[] args) {
        Counter counter = new Counter();
        
        // Create 1000 threads, each incrementing counter 1000 times
        Thread[] threads = new Thread[1000];
        
        for (int i = 0; i < 1000; i++) {
            threads[i] = new Thread(() -> {
                for (int j = 0; j < 1000; j++) {
                    counter.synchronizedIncrement();
                }
            });
            threads[i].start();
        }
        
        // Wait for all threads to complete
        for (Thread thread : threads) {
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        
        System.out.println("Final count: " + counter.getCount());
        System.out.println("Expected: 1000000");
        // Without synchronization, result would be less than 1000000
    }
}
```

### Synchronized Block

```java
class BankAccount {
    private double balance = 1000;
    
    public void withdraw(double amount) {
        synchronized(this) {  // Synchronized block
            if (balance >= amount) {
                System.out.println(Thread.currentThread().getName() + 
                                   " is withdrawing " + amount);
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                balance -= amount;
                System.out.println(Thread.currentThread().getName() + 
                                   " completed. Balance: " + balance);
            } else {
                System.out.println(Thread.currentThread().getName() + 
                                   " - Insufficient funds");
            }
        }
    }
    
    public double getBalance() {
        return balance;
    }
}

public class SynchronizedBlockExample {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        
        Runnable task = () -> {
            account.withdraw(600);
        };
        
        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");
        
        t1.start();
        t2.start();
        
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Final balance: " + account.getBalance());
    }
}
```

---

## Inter-Thread Communication

```java
class SharedResource {
    private int data;
    private boolean hasData = false;
    
    public synchronized void produce(int value) {
        while (hasData) {
            try {
                wait();  // Wait until data is consumed
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.data = value;
        hasData = true;
        System.out.println("Produced: " + value);
        notify();  // Notify consumer
    }
    
    public synchronized int consume() {
        while (!hasData) {
            try {
                wait();  // Wait until data is produced
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        hasData = false;
        System.out.println("Consumed: " + data);
        notify();  // Notify producer
        return data;
    }
}

class Producer implements Runnable {
    private SharedResource resource;
    
    public Producer(SharedResource resource) {
        this.resource = resource;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            resource.produce(i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Consumer implements Runnable {
    private SharedResource resource;
    
    public Consumer(SharedResource resource) {
        this.resource = resource;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            resource.consume();
            try {
                Thread.sleep(150);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ProducerConsumerExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        
        Thread producer = new Thread(new Producer(resource));
        Thread consumer = new Thread(new Consumer(resource));
        
        producer.start();
        consumer.start();
    }
}
```

---

## 2025 Interview Questions

**Q1: What is the difference between process and thread?**
**A:**
- **Process**: Independent program, separate memory, heavyweight
- **Thread**: Sub-process, shared memory, lightweight

**Q2: What are the two ways to create a thread?**
**A:**
1. Extend Thread class
2. Implement Runnable interface (preferred - allows multiple inheritance)

**Q3: What is the difference between start() and run()?**
**A:**
- `start()`: Creates new thread and calls run() method
- `run()`: Executes in the same thread (no new thread created)

**Q4: What is synchronization?**
**A:** Mechanism to control access to shared resources by multiple threads, preventing data inconsistency and race conditions.

**Q5: What is the difference between synchronized method and synchronized block?**
**A:**
- **Synchronized method**: Locks entire method
- **Synchronized block**: Locks only specific code section (better performance)

**Q6: What are wait(), notify(), and notifyAll()?**
**A:**
- `wait()`: Releases lock and waits
- `notify()`: Wakes up one waiting thread
- `notifyAll()`: Wakes up all waiting threads

**Q7: What is a deadlock?**
**A:** Situation where two or more threads are blocked forever, waiting for each other to release resources.

**Q8: What is thread priority?**
**A:** Determines the order of thread execution. Range: 1 (MIN) to 10 (MAX), default 5 (NORM).

**Q9: What is the difference between sleep() and wait()?**
**A:**
- `sleep()`: Doesn't release lock, specified time
- `wait()`: Releases lock, until notify/notifyAll

**Q10: What is join() method?**
**A:** Makes current thread wait until the thread on which join() is called completes execution.

---

## Key Takeaways

✅ Multithreading allows concurrent execution
✅ Implement Runnable interface (preferred over extending Thread)
✅ Use start() to create new thread, not run()
✅ Synchronization prevents race conditions
✅ wait/notify for inter-thread communication
✅ join() waits for thread completion
✅ Thread-safe code is crucial in multithreading

---

**🎉 Congratulations! You've completed the Java Learning Roadmap! 🎉**

**Next Steps:**
- Practice building projects using all concepts
- Explore Spring Framework for backend development
- Learn Design Patterns
- Study Data Structures & Algorithms
- Master JUnit for testing

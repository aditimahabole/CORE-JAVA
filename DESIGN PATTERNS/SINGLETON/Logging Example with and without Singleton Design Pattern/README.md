Let's simulate **multiple threads writing concurrently** to a log file — first **without** Singleton (which causes issues), and then **with** Singleton (which behaves correctly).

---

## ❌ Case 1: Without Singleton (Problematic Logging)

Each thread creates its own `Logger` instance → multiple file writers → unexpected behavior.

### `LoggerWithoutSingleton.java`

```java
import java.io.FileWriter;
import java.io.IOException;

public class LoggerWithoutSingleton {
    private FileWriter writer;

    public LoggerWithoutSingleton() {
        try {
            writer = new FileWriter("log.txt", true); // opens file in append mode
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public void log(String message) {
        try {
            writer.write(message + "\n");
            writer.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### `Main.java`

```java
public class Main {
    public static void main(String[] args) {
        Runnable task = () -> {
            LoggerWithoutSingleton logger = new LoggerWithoutSingleton();
            for (int i = 0; i < 5; i++) {
                logger.log(Thread.currentThread().getName() + " logs " + i);
            }
        };

        Thread t1 = new Thread(task, "T1");
        Thread t2 = new Thread(task, "T2");
        Thread t3 = new Thread(task, "T3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### ⚠️ Issues

* File may get locked or partially written.
* Data could be lost or out of order.
* Multiple `FileWriter`s = resource overhead.

---

## ✅ Case 2: With Singleton (Safe Logging)

### `LoggerSingleton.java`

```java
import java.io.FileWriter;
import java.io.IOException;

public class LoggerSingleton {
    private static LoggerSingleton instance;
    private FileWriter writer;

    private LoggerSingleton() {
        try {
            writer = new FileWriter("log.txt", true);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static synchronized LoggerSingleton getInstance() {
        if (instance == null) {
            instance = new LoggerSingleton();
        }
        return instance;
    }

    public synchronized void log(String message) {
        try {
            writer.write(message + "\n");
            writer.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### `Main.java`

```java
public class Main {
    public static void main(String[] args) {
        Runnable task = () -> {
            LoggerSingleton logger = LoggerSingleton.getInstance();
            for (int i = 0; i < 5; i++) {
                logger.log(Thread.currentThread().getName() + " logs " + i);
            }
        };

        Thread t1 = new Thread(task, "T1");
        Thread t2 = new Thread(task, "T2");
        Thread t3 = new Thread(task, "T3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### ✅ Output

* Only **one FileWriter** is used.
* All threads **safely share** the logger.
* Clean, ordered log entries.

---


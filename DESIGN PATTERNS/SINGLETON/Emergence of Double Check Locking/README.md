### Singleton Design Pattern

# 🧠 Singleton Design Pattern in Java – Logger Example

The **Singleton pattern** ensures that **only one instance** of a class is created throughout the application.

---

## 🚀 Why Singleton?

Imagine a class like `Logger` that writes to a file.

If every thread creates its own `Logger`, it:
- Corrupts the log file
- Wastes memory
- Behaves unpredictably

✅ The solution? Singleton!
Ensure only **one object** exists and is shared globally.

---

## 🧱 Code Example (Thread-safe with `synchronized`)

```java
public class Logger {
    private static Logger instance;

    private Logger() {}

    public static synchronized Logger getInstance() {
        if (instance == null) {
            instance = new Logger();
        }
        return instance;
    }
}

````

---

![image](https://github.com/user-attachments/assets/1629a59c-34e1-432f-97c7-a3e20617ca28)

## 🎭 Multithreading Story Time

A human is watching a multithreaded drama with 3 threads: `t1`, `t2`, and `t3`.

Here’s what happens:

1. 🧵 `t1` comes first and tries to get the `Logger` instance.
2. 🔒 `getInstance()` is `synchronized`, so only `t1` enters.
3. 🤔 It checks `instance == null` → Yes!
4. 🛠️ Creates the instance.
5. 🏃 Leaves the method and releases the lock.

Now the competition begins! 🏁

6. 🧵 `t2` and `t3` are waiting outside. `t3` gets lucky and enters next.
7. 🧵 `t3` enters `getInstance()` (has the lock now).
8. ❌ Checks `instance == null` → No, it's already created!
9. ✅ Returns the existing instance.
10. 🧵 `t2` finally enters and does the same.

---

## 👀 The Human Thinks...

> "Okay, locking works. Only one instance was created. But...
> after the first object is created, why are `t2` and `t3` **waiting** just to read it?
> That’s a waste of performance!"

💡 And boom! The **Double-Checked Locking** idea is born 💥

---

## 🛡️ What is Double-Checked Locking?

```java
public class Logger {
    private static volatile Logger instance;

    private Logger() {}

    public static Logger getInstance() {
        if (instance == null) {                  // First check (no locking)
            synchronized (Logger.class) {
                if (instance == null) {          // Second check (with locking)
                    instance = new Logger();
                }
            }
        }
        return instance;
    }
}
```

✅ Now:

* Only the **first thread** locks and creates the instance.
* Others just **read** it without waiting!

Let’s break down this line:

```java
synchronized (Logger.class)
```

### ✅ What does this mean?

It means:

> Lock the **`Logger` class object**, so that **only one thread** can execute the code inside the synchronized block **at a time**.

---

### 🔍 Let's Understand Step-by-Step

#### 1. **`synchronized` block**

```java
synchronized (someObject) {
    // critical section
}
```

This tells Java:

* "Before entering this block, **get a lock** on `someObject`."
* "If another thread has already locked it, **wait** until it is released."
* "Once inside, **no other thread** can enter any other block locked on the **same object**."

---

#### 2. **What is `Logger.class`?**

* In Java, every class (like `Logger`) has a **Class object** associated with it.
* `Logger.class` is a **reference to that Class object**.
* So, `synchronized (Logger.class)` means:

  * Lock the **class-level lock**, **not object-level**.

---

### ✅ Why are we locking on `Logger.class`?

Because:

* The `instance` variable is **static** (belongs to the class, not any object)
* So, we lock the **class itself** (`Logger.class`) to make sure **only one thread** can create the instance

---

### 🧠 What if we used `this` instead of `Logger.class`?

You **cannot** use `this` in a static method because `this` refers to an object, and static methods **don’t belong to any object**.

---

### ✅ Final Recap

```java
synchronized (Logger.class)
```

Means:

* Lock the `Logger` **class-level monitor**
* Only one thread can enter that block at a time
* It ensures that **instance is created only once**, even in multithreaded access

Let me explain clearly what I meant when I said:

> "Every class in Java has a **Class object** associated with it."

---

### ✅ What is a `Class` object in Java?

In Java, **everything is an object** — even **classes themselves** are represented as objects of type `java.lang.Class`.

#### Example:

```java
Logger.class
```

This returns an object of type `Class<Logger>`, which **represents the `Logger` class itself** in memory.

---

### ✅ When is the `Class` object created?

When you first **load** a class (like `Logger`) into memory (e.g., the first time you use `Logger` in your code), the Java Virtual Machine (JVM) automatically creates a **`Class` object** for it.

* This object holds **metadata** about the class: its name, methods, fields, etc.
* It is **shared** across the entire application.
* There is **only one `Class` object** per loaded class.

---

### ✅ Why is this useful?

You can use it to:

* Lock the class itself (like `synchronized(Logger.class)`)
* Use **reflection** to inspect the class at runtime
* Get the class name, methods, fields, etc.

---

### ✅ Small Example:

```java
Class<?> c = Logger.class;
System.out.println(c.getName());   // Output: Logger
```

Here, `Logger.class` gives you the **Class object** that describes the Logger class.

---

### ✅ Summary:

| Concept        | Description                                          |
| -------------- | ---------------------------------------------------- |
| `Logger.class` | A reference to the `Class` object for `Logger`       |
| Class object   | Created by JVM when the class is loaded              |
| Purpose        | Lets you access class metadata or use it for locking |

---



---

## ✅ Summary

| Feature                  | Before (Synchronized Only) | After (Double-Checked Locking) |
| ------------------------ | -------------------------- | ------------------------------ |
| Thread-safe              | ✅                          | ✅                              |
| Performance (after init) | ❌ Slower                   | ✅ Faster                       |
| Multiple instance risk   | ❌ Possible (w/o sync)      | ✅ Handled properly             |

---


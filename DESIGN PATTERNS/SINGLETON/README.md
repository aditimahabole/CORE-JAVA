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

---

## ✅ Summary

| Feature                  | Before (Synchronized Only) | After (Double-Checked Locking) |
| ------------------------ | -------------------------- | ------------------------------ |
| Thread-safe              | ✅                          | ✅                              |
| Performance (after init) | ❌ Slower                   | ✅ Faster                       |
| Multiple instance risk   | ❌ Possible (w/o sync)      | ✅ Handled properly             |

---


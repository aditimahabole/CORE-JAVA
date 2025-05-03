###☕ What is the Singleton Pattern?

+ The Singleton Pattern ensures that only one object (instance) of a class is ever created — and that this one object is shared globally across your application.

👷 Basic Structure of Singleton in Java
```
public class Singleton {
    private static Singleton instance;     // 1️⃣ Static instance of the class

    private Singleton() {}                 // 2️⃣ Private constructor

    public static Singleton getInstance() {// 3️⃣ Public static method to access instance
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
### 🔍 Why These Keywords?

private Singleton()

Prevents others from using new Singleton() outside the class.

🔒 Forces access only through getInstance().

❌ If constructor is not private, anyone can do:
Singleton s = new Singleton(); → Multiple objects → Defeats purpose!

static Singleton instance

Belongs to the class, not objects.

We need a shared copy across all accesses.

❌ If not static, each call to getInstance() will have no access to previous instances.

public static Singleton getInstance()

Global access point.

static because we want to call it without creating an object.

🧵 Problem: Multithreading without Synchronization

```
public static Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton(); // Thread may be interrupted here
    }
    return instance;
}
```
❌ What Can Go Wrong?
Imagine two threads T1 and T2:

Both enter getInstance() at the same time

Both see instance == null

Both create a new Singleton

❌ Now two instances exist! ❌

This breaks the whole idea of Singleton.

🛡️ Solution 1: Add synchronized
```
public static synchronized Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton();
    }
    return instance;
}
```
✅ Pros
Thread-safe

Only one thread can enter the method at a time

❌ Cons
Performance penalty: Even after the object is created, all threads must wait their turn to enter the method.

Useless locking once the instance is available!

💡 Solution 2: Double-Checked Locking

```
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {                   // First check (no locking)
            synchronized (Singleton.class) {
                if (instance == null) {           // Second check (with locking)
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
✅ Why This is Smart
First check: Avoids locking after instance is created.

Lock is applied only during first creation.

Best of both worlds: Thread-safety + Performance.

volatile is used to ensure proper visibility of instance across threads.

📝 Summary Table
Feature	Without Sync	Synchronized Method	Double-Checked Locking
Thread-Safe	❌	✅	✅
Performance	✅ (fast but risky)	❌ (slow for all)	✅ (fast after creation)
Multiple instance risk	✅	❌	❌
Best Practice	❌	😐 (simple but costly)	✅ (recommended)


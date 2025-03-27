# **📌 Strings and Immutable Concepts in Java**  

Strings are one of the most **commonly used** data types in Java. Understanding their behavior is **crucial** for interviews, especially **immutability, memory management, and performance optimizations**.  

---

# **1️⃣ Why is String Immutable in Java?**  
📌 **Definition:** A string is **immutable**, meaning once created, its value **cannot be changed**. If we modify a string, **a new object is created** instead of modifying the existing one.  

### **🔹 Why did Java make Strings immutable?**  
✅ **1. Security** – Prevents modification of sensitive data like **passwords, usernames, database URLs, and class loading paths**.  
✅ **2. String Pool Optimization** – Saves memory by **reusing** strings instead of creating duplicates.  
✅ **3. Thread Safety** – No need for synchronization, making **String inherently thread-safe**.  
✅ **4. HashCode Caching** – Since the value **never changes**, the `hashCode` is cached for performance in HashMap/HashSet.  
✅ **5. Class Loading Stability** – Since **String literals** are used for loading classes, they should not be modified to prevent security risks.  

---

### **🔹 How does String immutability work?**  
1️⃣ **String objects are stored in the String Pool**  
2️⃣ **Any modification creates a new object** instead of changing the existing one.  

#### **Example:**
```java
public class StringImmutableExample {
    public static void main(String[] args) {
        String s1 = "Hello";
        s1 = s1 + " World";  // Creates a NEW object "Hello World"
        System.out.println(s1);
    }
}
```
➡️ The original `"Hello"` remains unchanged; instead, `"Hello World"` is stored as a **new object**.  

---

# **2️⃣ String vs. StringBuilder vs. StringBuffer**  
### **🔹 Key Differences**
| Feature | **String** | **StringBuilder** | **StringBuffer** |
|---------|-----------|-----------------|----------------|
| **Mutability** | ❌ Immutable | ✅ Mutable | ✅ Mutable |
| **Thread-Safety** | ✅ Yes (Immutable) | ❌ No | ✅ Yes (Synchronized) |
| **Performance** | ❌ Slower (Creates new object) | ✅ Faster (No sync overhead) | ⚠️ Slower than `StringBuilder` (sync overhead) |
| **Use Case** | Constant data (Passwords, Configs) | Single-threaded operations | Multi-threaded operations |

---

### **🔹 When to Use Which?**
✅ **String** → When immutability is needed (e.g., **Constants, Keys, Passwords**)  
✅ **StringBuilder** → When frequent modifications occur in a **single-threaded** application (e.g., **JSON/XML parsing, Dynamic SQL queries**)  
✅ **StringBuffer** → When frequent modifications occur in a **multi-threaded** environment (e.g., **Logging in concurrent systems**)  

---

### **🔹 Example: Performance Comparison**
#### **🔹 Using String (Slow, Creates New Object)**
```java
public class StringTest {
    public static void main(String[] args) {
        String s = "Java";
        for (int i = 0; i < 10000; i++) {
            s = s + " Rocks";  // Creates new object each time ❌
        }
    }
}
```
➡️ **Bad performance** due to excessive object creation.  

#### **🔹 Using StringBuilder (Fast, Uses Same Object)**
```java
public class StringBuilderTest {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Java");
        for (int i = 0; i < 10000; i++) {
            sb.append(" Rocks");  // Uses same object ✅
        }
    }
}
```
➡️ **Much faster**, avoids unnecessary object creation.  

---

# **3️⃣ How Does intern() Method Work in String Pool?**
📌 **Definition:**  
The `intern()` method ensures that **identical string literals share the same memory location** in the **String Pool**, avoiding duplicate objects.  

### **🔹 How String Pool Works**
1️⃣ **Before Java 7** → String Pool was part of **Permanent Generation (PermGen)**  
2️⃣ **After Java 7** → String Pool moved to **Heap memory (MetaSpace in Java 8+)**  

---

### **🔹 Example: Without `intern()` (Two Objects Created)**
```java
public class StringInternExample {
    public static void main(String[] args) {
        String s1 = new String("Hello");  // Heap Memory
        String s2 = "Hello";  // String Pool
        System.out.println(s1 == s2);  // ❌ False (Different memory locations)
    }
}
```
➡️ **`s1` and `s2` are different objects**, so `==` returns `false`.  

---

### **🔹 Example: With `intern()` (One Object Reused)**
```java
public class StringInternExample {
    public static void main(String[] args) {
        String s1 = new String("Hello").intern();  // Moved to String Pool
        String s2 = "Hello";  // Already in String Pool
        System.out.println(s1 == s2);  // ✅ True (Same memory location)
    }
}
```
➡️ **`intern()` forces `s1` to use the existing `"Hello"` in the String Pool**, so `==` returns `true`.  

---

# **🔹 Frequently Asked Interview Questions**
### **✅ Why is String immutable in Java?**
📌 **To ensure security, performance optimization, caching, and thread safety.**  

### **✅ What is the difference between String, StringBuilder, and StringBuffer?**
📌 **String is immutable, StringBuilder is fast but not thread-safe, StringBuffer is synchronized but slower.**  

### **✅ How does Java optimize memory with Strings?**
📌 **Java uses the String Pool to store literals, reducing memory usage.**  

### **✅ What is the `intern()` method and why is it useful?**
📌 **It moves a string to the String Pool to enable memory reuse and save space.**  

### **✅ Why is String used in HashMap keys?**
📌 **Because String is immutable, its hashcode never changes, ensuring consistency in key lookups.**  

---

# **🚀 Summary**
✅ **String is immutable for security, caching, and performance reasons**  
✅ **StringBuilder is the best choice for frequent modifications in a single thread**  
✅ **StringBuffer is useful in multi-threaded environments**  
✅ **`intern()` helps in memory optimization by reusing string literals**  


---
#### Q When the memory is created in heap and when in string pool and how did you said this line :
"hello" inside new String() is also placed in the String Pool, but it was already there due to s3, so it reuses it.
s3 code was written after s2 so what is exactly happening here


Great question! Let's break this down step by step to understand when **String objects** are created in the **Heap** vs. the **String Pool**, and what happens when `new String("hello")` is used.

---

## **1️⃣ When is memory created in Heap vs. String Pool?**
### **🔹 String Pool (Method Area / Intern Pool)**
- **String literals (directly assigned using `" "` syntax) are automatically stored in the String Pool**.
- If the same literal already exists, Java **reuses it instead of creating a new one**.
- Example:
  ```java
  String s1 = "hello";  // Stored in String Pool
  String s2 = "hello";  // Points to the same "hello" in String Pool (NO new object)
  ```

### **🔹 Heap Memory**
- If you create a `String` using **`new String("text")`**, a **new object is always created in Heap**, even if the same text exists in the String Pool.
- Example:
  ```java
  String s3 = new String("hello");  // 🆕 New object in Heap
  ```

---

## **2️⃣ Analyzing Your Code in Detail**
```java
public class WithoutIntern {
    public static void main(String[] args) {
        String s1 = new String("hello");  // 🆕 Creates object in Heap, and "hello" goes to String Pool if not already present
        String s2 = new String("hello");  // 🆕 Creates another object in Heap, reuses "hello" from String Pool
        String s3 = "hello";  // 📌 Uses "hello" from String Pool
        String s4 = "hello";  // 📌 Uses same "hello" from String Pool (same as s3)

        System.out.println(s1 == s2);  // ❌ False (Heap objects are different)
        System.out.println(s1.equals(s2));  // ✅ True (Same content)
    }
}
```

### **🔍 Step-by-step Execution**
1️⃣ **`String s1 = new String("hello");`**
   - `"hello"` **goes to the String Pool** (if not already present).
   - A **new "hello" object is created in Heap** and `s1` refers to it.

2️⃣ **`String s2 = new String("hello");`**
   - `"hello"` **already exists in the String Pool**, so it is reused internally.
   - But a **new "hello" object is still created in Heap** for `s2`.

3️⃣ **`String s3 = "hello";`**
   - `"hello"` **already exists in the String Pool**, so `s3` **points to the same object in the String Pool**.

4️⃣ **`String s4 = "hello";`**
   - `"hello"` **already exists in the String Pool**, so `s4` **also points to the same object in the String Pool**.

---

## **3️⃣ Answering Your Doubt: What happens if s3 is declared after s2?**
You asked:
> `"hello" inside new String() is also placed in the String Pool, but it was already there due to s3, so it reuses it."`
> But s3 was written after s2 in the code, so what is happening?

**👉 Important Point:**  
- Even though `s3` is written **after** `s1` and `s2`, the **String Pool is populated whenever a `String` literal is first encountered in the entire program**.
- So, **when `new String("hello")` is executed in `s1`**, Java internally ensures that `"hello"` is in the **String Pool**.

So effectively, **before `s3` is executed, the String Pool already contains `"hello"` due to the earlier `"hello"` in `new String("hello")`**.

---

## **4️⃣ Summary**
| Code | Where is Memory Created? |
|------|--------------------------|
| `String s1 = new String("hello");` | **Heap (new object)** + `"hello"` added to **String Pool** (if not already there) |
| `String s2 = new String("hello");` | **Heap (new object)**, **String Pool reused** |
| `String s3 = "hello";` | **Uses existing `"hello"` from String Pool** |
| `String s4 = "hello";` | **Reuses `"hello"` from String Pool** |

### **🔹 Key Takeaways**
✔ **String literals are automatically stored in the String Pool.**  
✔ **Using `new String("text")` always creates a new object in Heap** but still uses the String Pool internally.  
✔ **Order of declaration in code does not matter**—the String Pool is managed automatically whenever a literal is encountered.  

Let me know if anything is unclear! 🚀

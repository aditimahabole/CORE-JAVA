### **1. What is Java, and why is it called a platform-independent language?**  
**Java** is a high-level, **object-oriented** programming language developed by **Sun Microsystems** (now owned by Oracle). It is designed to be **simple, secure, and portable** across different computing environments.  

#### **Why is Java platform-independent?**  
Java is called **platform-independent** because of its **"Write Once, Run Anywhere" (WORA)** capability. This is achieved through the use of the **Java Virtual Machine (JVM)**.  

- In languages like C or C++, the code is compiled directly into **machine code**, which runs only on a specific OS.  
- In Java, the code is first compiled into **bytecode (.class file)**, which is not tied to any specific platform.  
- The **JVM (Java Virtual Machine)** interprets and runs this bytecode on any operating system (Windows, Linux, macOS) as long as a JVM is installed.  

Thus, Java programs can run on different platforms **without modification**, making Java platform-independent.  

---

### **2. Explain JVM, JRE, and JDK.**  
These three components form the **Java runtime environment**.  

#### **1️⃣ JVM (Java Virtual Machine)**  
- JVM is a program that **executes Java bytecode**.  
- It provides features like **memory management (Garbage Collection), Just-In-Time (JIT) compilation**, and security.  
- **JVM is platform-specific**, meaning there are different JVMs for Windows, macOS, and Linux.  

#### **2️⃣ JRE (Java Runtime Environment)**  
- JRE includes the **JVM + necessary libraries** required to run Java applications.  
- **It does NOT contain tools for development (like compilers).**  
- If you only want to **run** Java programs (not develop), installing **JRE** is enough.  

#### **3️⃣ JDK (Java Development Kit)**  
- JDK = **JRE + development tools (compiler, debugger, JavaDocs, etc.)**  
- It contains everything needed for **writing, compiling, and running** Java programs.  
- To develop Java applications, you need **JDK**.  

📌 **Summary:**  
| Component | Contains | Used for |  
|-----------|------------|------------|  
| **JVM** | Runs bytecode | Running Java applications |  
| **JRE** | JVM + Libraries | Running Java applications (without development tools) |  
| **JDK** | JRE + Compiler + Tools | Developing and running Java applications |  

---

### **3. What is the difference between JDK 8 and JDK 17?**  

| Feature | JDK 8 | JDK 17 |  
|---------|------|------|  
| **Release Year** | 2014 | 2021 |  
| **Support** | Long-Term Support (LTS) | LTS version (Recommended for production) |  
| **Lambda Expressions** | Introduced in JDK 8 | Available |  
| **Stream API** | Introduced | Enhanced performance |  
| **Date & Time API** | New `java.time` package introduced | Available |  
| **Switch Expressions** | Not available | Introduced (`switch` can return values) |  
| **Records** | Not available | Introduced (Used for immutable data) |  
| **Sealed Classes** | Not available | Introduced (Restricts which classes can extend a class) |  
| **Performance** | Good | Improved Garbage Collection, lower memory usage |  

✅ **JDK 17 is more efficient, secure, and feature-rich**, making it a better choice for new projects.  

---

### **4. What are wrapper classes, and why are they needed?**  

A **wrapper class** is a class that **converts primitive data types (int, double, char, etc.) into objects**.  

#### **Example of Wrapper Classes**  
| Primitive Type | Wrapper Class |  
|--------------|--------------|  
| `int` | `Integer` |  
| `char` | `Character` |  
| `boolean` | `Boolean` |  
| `double` | `Double` |  

#### **Why do we need Wrapper Classes?**  
1️⃣ **Collections require objects** – Java **Collections (ArrayList, HashMap, etc.)** store objects, not primitives.  
```java
ArrayList<Integer> list = new ArrayList<>();
list.add(10);  // int is automatically converted to Integer
```
2️⃣ **Utility Methods** – Wrapper classes provide useful methods.  
```java
int num = Integer.parseInt("123");  // Converts String to int
```
3️⃣ **Null Values Support** – Unlike primitive types, wrapper classes can store `null`.  
```java
Integer x = null;  // Valid
int y = null;  // ❌ Compilation error
```
4️⃣ **Type Conversion** – Convert between types easily.  
```java
double d = Double.valueOf("3.14");  // String to double
```

---

### **5. Explain Autoboxing and Unboxing.**  
**Autoboxing and Unboxing** deal with the conversion between **primitive types** and **wrapper objects**.  

#### **Autoboxing (Primitive → Wrapper)**  
Java **automatically converts** a primitive data type into its corresponding wrapper class object.  
```java
int num = 10;
Integer obj = num;  // Autoboxing: int → Integer
```

#### **Unboxing (Wrapper → Primitive)**  
Java **automatically converts** a wrapper object into its corresponding primitive type.  
```java
Integer obj = 20;
int num = obj;  // Unboxing: Integer → int
```

#### **Example of Both**
```java
public class AutoboxingUnboxingExample {
    public static void main(String[] args) {
        // Autoboxing
        Integer a = 100;  // int → Integer
        Double b = 5.5;   // double → Double
        
        // Unboxing
        int c = a;  // Integer → int
        double d = b;  // Double → double
        
        System.out.println("Autoboxed: " + a + ", " + b);
        System.out.println("Unboxed: " + c + ", " + d);
    }
}
```

📌 **Why is this useful?**  
- **Reduces manual conversion** (no need to use `new Integer()` or `.intValue()`).  
- **Improves code readability and maintainability**.  

---

### **Summary**  
✅ **Java is platform-independent** because of JVM and bytecode.  
✅ **JVM runs Java programs, JRE includes JVM + libraries, JDK includes JRE + development tools**.  
✅ **JDK 17 has better performance, security, and features compared to JDK 8**.  
✅ **Wrapper classes convert primitive types into objects** and are needed for **collections, null support, and utility methods**.  
✅ **Autoboxing and Unboxing** allow automatic conversion between primitive and wrapper types.  


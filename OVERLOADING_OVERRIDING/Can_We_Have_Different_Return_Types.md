### **Overloading: Can We Have Different Return Types?**  
No, **method overloading** is **not possible** with only a **different return type** in Java.  

#### **Why?**
When you call a method, the compiler identifies the method based on its **name and parameters (method signature)**. The return type is **not** part of the method signature in overloading.  

#### **Example (Invalid Overloading – Different Return Type)**
```java
class Test {
    int add(int a, int b) {
        return a + b;
    }

    // ❌ ERROR: Overloading is not allowed with only a different return type
    double add(int a, int b) {  
        return a + b;
    }
}
```
🔴 **Compilation Error**: The compiler cannot differentiate between these two methods because their **parameters are the same**, and Java does **not consider return type for method overloading**.

---

### **Correct Method Overloading**
To overload a method, the **method signature must be different**. This can be done by:
✅ Changing the **number** of parameters  
✅ Changing the **type** of parameters  
✅ Changing the **order** of parameters  

#### **Example (Valid Overloading)**
```java
class Test {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {  // ✅ Different parameter type
        return a + b;
    }

    int add(int a, int b, int c) {  // ✅ Different number of parameters
        return a + b + c;
    }
}
```
✔ **This is valid overloading** because parameters differ in type or count.

---

### **Overriding: Can We Have Different Return Types?**
Yes, **method overriding allows different return types** under a condition:  
- The return type in the child class should be a **subclass** of the return type in the parent class.  
- This is known as **covariant return type**.

#### **Example (Valid Overriding with Different Return Type)**
```java
class Parent {
    Number getNumber() {  // Parent method returns Number
        return 10;
    }
}

class Child extends Parent {
    @Override
    Integer getNumber() {  // Child method returns Integer (which is a subclass of Number)
        return 20;
    }
}
```
✔ **This is valid** because `Integer` is a subclass of `Number`.  

---

### **Invalid Overriding (Completely Different Return Type)**
If the child class tries to return a completely different type that is not a subclass of the parent's return type, it will cause an **error**.

```java
class Parent {
    String getMessage() {
        return "Hello";
    }
}

class Child extends Parent {
    // ❌ ERROR: Different return type that is not a subclass of String
    Integer getMessage() {  
        return 100;
    }
}
```
🔴 **Compilation Error**: `Integer` is not a subclass of `String`.

---

### **Key Differences Between Overloading & Overriding**
| Feature          | Overloading | Overriding |
|-----------------|------------|------------|
| Where?         | Same class  | Parent-Child classes (Inheritance) |
| Method Name    | Same        | Same |
| Parameters     | **Must be different** | **Must be the same** |
| Return Type    | Not considered for overloading | Can be different **only if covariant (subclass)** |
| Access Modifiers | Can be anything | Cannot be **more restrictive** than the parent |
| Static Methods | Can be overloaded | **Cannot be overridden**, only hidden |

---

### **Final Answer**
✅ **Overloading does not work with just a different return type.**  
✅ **Overriding allows different return types if the return type is a subclass (covariant return type).**  


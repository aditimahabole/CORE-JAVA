# Object-Oriented Programming (OOP) vs Procedural Programming

## Procedural Programming
- Divided into **functions**.
- **No proper data hiding** (data is accessible everywhere).
- Functions and data are **tightly coupled**.
- Focuses on **functions**, and data moves freely.

### Example:
```c
int speed = 0;
void increaseSpeed() {
    speed += 10;
}
```
- Here, `speed` is globally accessible, which is not secure.

## Object-Oriented Programming (OOP)
- Divided into **objects**.
- Provides **data hiding**.
- Focuses on **data** rather than functions.

### Example:
```java
class Car {
    private int speed = 0;
    
    void increaseSpeed() {
        speed += 10;
    }
}
```
- Here, `speed` is private and can only be modified by class methods.

---
## Objects & Classes

### **Objects**
- An **object** has **properties (state)** and **behavior (functions)**.
- Example: **Car**
  - **Properties**: Color, Type, Brand
  - **Behavior**: Apply Brake, Drive, Increase Speed

### **Class**
- A **blueprint** or **template** from which objects are created.
- Defines **properties** and **behaviors**.
- Many objects can be created from a class.

### Example:
```java
class Car {
    String color;
    String brand;
    
    void drive() {
        System.out.println("Car is driving");
    }
}
```

---
## OOP Pillars

### **1. Data Abstraction**
- Hides internal implementation and shows only essential functionality.
- Achieved through **interfaces** and **abstract classes**.
- **Example:** ATM Machine (you enter a PIN, but don’t see the internal process).

#### **Why Data Abstraction?**
✅ Protects sensitive data from unauthorized access.
✅ Simplifies interactions with clear interfaces.
✅ Improves security and maintainability.

#### **Example:**
```java
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark!");
    }
}
```
- The user does not need to know how `makeSound()` is implemented.

---
### **2. Data Encapsulation**
- Also called **Data Hiding**.
- Bundles **data and functions** into a single unit.
- Achieved using **public, private, protected** access specifiers.

#### **Why Data Encapsulation?**
❌ No protection if data is not encapsulated.
❌ Hard to debug if data can be modified anywhere.
❌ No validation, so invalid data can be assigned.

#### **Advantages:**
✅ Prevents unauthorized access.
✅ Ensures only valid data is stored.
✅ Makes maintenance easier.
✅ Hides complexity.

#### **Example:**
```java
class Person {
    private int age;
    
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        } else {
            System.out.println("Age must be positive");
        }
    }
    
    public int getAge() {
        return age;
    }
}
```
- **Only valid ages** can be set, preventing invalid data.

---
## Summary
| Feature              | Procedural Programming  | OOP                 |
|----------------------|------------------------|----------------------|
| **Division**        | Functions               | Objects             |
| **Data Hiding**     | No                      | Yes                 |
| **Focus**           | Functions               | Data & Functions    |
| **Security**        | Low                     | High                |
| **Example**         | `int speed;`            | `private int speed;` |

---

## 🚀 Conclusion
Object-Oriented Programming (OOP) provides **better security, maintainability, and scalability** compared to procedural programming. **Encapsulation and Abstraction** help in keeping the data safe and ensuring only valid data is used.

Understanding these OOP concepts will make you a **better software developer**! 🚀

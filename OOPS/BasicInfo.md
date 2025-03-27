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



# Object-Oriented Programming (OOP) Concepts

## 3. Inheritance
Inheritance allows a class (**child class**) to reuse properties and behaviors from another class (**parent class**). This helps avoid code duplication and promotes **code reusability**.

### How to Implement Inheritance?
- **Using `extends` keyword** (for classes)
- **Using interfaces** (for multiple inheritance)

### **Types of Inheritance in Java**
1. **Single-level Inheritance**: A child class inherits from one parent class.
2. **Multi-level Inheritance**: A class inherits from another child class, forming a chain.
3. **Hierarchical Inheritance**: Multiple child classes inherit from a single parent class.
4. **Multiple Inheritance (Not allowed in Java with classes)**: Java doesn’t support multiple inheritance with classes to avoid the **diamond problem**.
   - ✅ **Solution**: Use **interfaces** instead of classes for multiple inheritance.

### **Example (Enterprise Level: Employee Management System)**
```java
// Parent class
class Employee {
    String name;
    double salary;
    
    void showDetails() {
        System.out.println("Employee: " + name + ", Salary: " + salary);
    }
}

// Child class inheriting Employee
class Manager extends Employee {
    int teamSize;
    
    void showManagerDetails() {
        System.out.println("Manager: " + name + " manages a team of " + teamSize);
    }
}
```
🔹 **Use Case:** HR applications where a `Manager` class inherits common attributes from an `Employee` class.

### **Advantages of Inheritance**
- ✅ **Code Reusability** – Avoids duplicate code.
- ✅ **Polymorphism Support** – Allows overriding methods.
- ✅ **Better Maintainability** – Easier to update common logic.

---

## 4. Polymorphism
Polymorphism means **one method behaving differently** based on the situation. It allows flexibility and improves code readability.

### **Types of Polymorphism in Java**
1. **Compile-time Polymorphism (Method Overloading)**
   - Same method name, but different parameters (different number or types of arguments).
   - Happens in the **same class**.

#### **Example (Enterprise Level: Payment Processing System)**
```java
class PaymentProcessor {
    void processPayment(double amount) {
        System.out.println("Processing payment of Rs." + amount);
    }
    
    void processPayment(double amount, String currency) {
        System.out.println("Processing payment of " + amount + " in " + currency);
    }
}
```
🔹 **Use Case:** In an e-commerce platform, a method can process payments in different currencies.

2. **Runtime Polymorphism (Method Overriding)**
   - Same method name and parameters in a **parent and child class**.
   - Happens in **different (inherited) classes**.

#### **Example (Enterprise Level: Logging System)**
```java
class Logger {
    void log(String message) {
        System.out.println("Logging: " + message);
    }
}

class FileLogger extends Logger {
    @Override
    void log(String message) {
        System.out.println("Writing to file: " + message);
    }
}
```
🔹 **Use Case:** A logging framework where different loggers write logs to console, file, or database.

### **Key Differences Between Overloading & Overriding**
| Feature          | Overloading | Overriding |
|-----------------|------------|------------|
| Where?         | Same class  | Parent-Child classes (Inheritance) |
| Parameters     | **Must be different** | **Must be the same** |
| Return Type    | Can be different | Can be different **only if covariant (subclass)** |
| Access Modifiers | Can be anything | Cannot be **more restrictive** than the parent |
| Static Methods | Can be overloaded | Cannot be overridden |

---

## **Relationships in Java**
### **1. IS-A Relationship (Inheritance)**
- When one class **inherits** another, it forms an **IS-A** relationship.
- **Example:** `Manager IS-A Employee` because the `Manager` class extends `Employee`.

### **2. HAS-A Relationship (Composition & Aggregation)**
- **Aggregation (Weak Relationship)**: One object contains another, but both can exist independently.
  - **Example:** A `School` has many `Classrooms`, but deleting a `Classroom` doesn’t delete the `School`.

```java
class School {
    String name;
}

class Classroom {
    School school; // Aggregation (weak relation)
}
```

- **Composition (Strong Relationship)**: If one object is deleted, the other gets deleted too.
  - **Example:** A `Car` has an `Engine`. If the car is destroyed, its engine is too.

```java
class Engine {
    void start() {
        System.out.println("Engine starting...");
    }
}

class Car {
    private Engine engine = new Engine(); // Composition (strong relation)
    void startCar() {
        engine.start();
    }
}
```

🔹 **Use Case:** In a banking application, an **Account** can exist without a **Transaction**, but a **Transaction** cannot exist without an **Account**.

---

### **Conclusion**
- **Inheritance** helps in code reuse and structuring applications.
- **Polymorphism** makes the system flexible by allowing multiple behaviors for the same function.
- **IS-A and HAS-A relationships** define class interactions and are crucial for designing scalable enterprise applications.





### **OOP Concepts in Java**  

Object-Oriented Programming (OOP) is a programming model that organizes software design around **objects**. Java follows **four key OOP principles**:  

---

## **1. Abstraction**  
### **Definition:**  
Hiding implementation details and exposing only essential features.  

### **Example (Enterprise-Level 🚀):**  
🔹 **Payment Processing System** – You can have a `Payment` interface with methods like `processPayment()`. Different classes like `CreditCardPayment`, `UPIPayment`, and `PayPalPayment` implement this method differently.  

```java
interface Payment {
    void processPayment(double amount);
}

class CreditCardPayment implements Payment {
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment of $" + amount);
    }
}
```
➡️ The user only calls `processPayment()`, without knowing **how** it's processed internally.  

---

## **2. Encapsulation**  
### **Definition:**  
Wrapping **data (variables)** and **methods** into a single unit (class) and restricting direct access.  

### **Example (Enterprise-Level 🚀):**  
🔹 **Bank Account Management** – Prevents unauthorized changes to sensitive data like balance.  

```java
class BankAccount {
    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```
➡️ The **balance** variable is private, so direct access is not allowed.  

---

## **3. Inheritance**  
### **Definition:**  
One class acquires the properties of another class, promoting **code reuse**.  

### **Example (Enterprise-Level 🚀):**  
🔹 **Employee Management System** – `Employee` class can be a parent, and `Manager`, `Developer`, `Intern` can extend it.  

```java
class Employee {
    String name;
    double salary;
    
    void work() {
        System.out.println(name + " is working");
    }
}

class Manager extends Employee {
    void manageTeam() {
        System.out.println(name + " is managing the team");
    }
}
```
➡️ **Avoids code duplication** – `Manager` inherits `work()` method instead of writing it again.  

---

## **4. Polymorphism**  
### **Definition:**  
One method behaves differently based on the object that calls it.  

### **Example (Enterprise-Level 🚀):**  
🔹 **Notification System** – A `sendNotification()` method can send notifications via **email, SMS, or push notification**.  

```java
class Notification {
    void sendNotification() {
        System.out.println("Sending notification");
    }
}

class EmailNotification extends Notification {
    void sendNotification() {
        System.out.println("Sending Email");
    }
}

class SMSNotification extends Notification {
    void sendNotification() {
        System.out.println("Sending SMS");
    }
}
```
➡️ The **same method name (`sendNotification()`) behaves differently** depending on the object type.  

---

# **Method Overloading vs. Method Overriding**
| Feature | **Method Overloading** | **Method Overriding** |
|---------|-------------------|-------------------|
| **Definition** | Same method name but **different parameters** in the same class | Same method name & parameters, but **different implementation** in child class |
| **Compile-time or Runtime?** | **Compile-time polymorphism** | **Runtime polymorphism** |
| **Inheritance Needed?** | ❌ No | ✅ Yes |
| **Example** | Multiple `add()` methods with different parameter types | `withdraw()` method in `BankAccount` overridden in `SavingsAccount` |

### **Enterprise Example 🚀**  
🔹 **Method Overloading – Logging System**  
```java
class Logger {
    void log(String message) {
        System.out.println("Message: " + message);
    }

    void log(String message, int errorCode) {
        System.out.println("Error " + errorCode + ": " + message);
    }
}
```
➡️ **Different versions** of `log()` allow logging with/without an error code.  

🔹 **Method Overriding – Payment Gateway**  
```java
class Payment {
    void processPayment() {
        System.out.println("Processing generic payment");
    }
}

class CardPayment extends Payment {
    @Override
    void processPayment() {
        System.out.println("Processing card payment");
    }
}
```
➡️ The **child class provides its own implementation** of `processPayment()`.  

---

# **What is Dynamic Method Dispatch?**  
📌 **Definition:**  
It is **runtime polymorphism**, where method calls are resolved at runtime based on the actual object.  

### **Enterprise Example 🚀**  
🔹 **Cloud Storage Services (AWS, Google Drive, Dropbox)**  
```java
class CloudStorage {
    void uploadFile() {
        System.out.println("Uploading file to cloud");
    }
}

class AWSStorage extends CloudStorage {
    void uploadFile() {
        System.out.println("Uploading file to AWS S3");
    }
}

class GoogleDriveStorage extends CloudStorage {
    void uploadFile() {
        System.out.println("Uploading file to Google Drive");
    }
}

public class Main {
    public static void main(String[] args) {
        CloudStorage storage = new AWSStorage();
        storage.uploadFile();  // Calls AWSStorage's uploadFile()
        
        storage = new GoogleDriveStorage();
        storage.uploadFile();  // Calls GoogleDriveStorage's uploadFile()
    }
}
```
➡️ Even though `storage` is of type `CloudStorage`, the method called is based on the **actual object type** (`AWSStorage` or `GoogleDriveStorage`).  

---

# **Why Use Interfaces Instead of Abstract Classes?**  
| Feature | **Interface** | **Abstract Class** |
|---------|-------------|----------------|
| **Multiple Inheritance** | ✅ Allowed | ❌ Not Allowed |
| **Default Implementation** | ❌ No (Only method signatures) | ✅ Yes (Can have concrete methods) |
| **When to Use?** | Use when **multiple classes** need to follow a **contract** | Use when **some methods should be common**, but **some should be overridden** |

### **Enterprise Example 🚀**  
🔹 **Interface – Payment Gateway API** (Supports multiple payment providers)  
```java
interface PaymentGateway {
    void processPayment(double amount);
}

class PayPal implements PaymentGateway {
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment of $" + amount);
    }
}

class Stripe implements PaymentGateway {
    public void processPayment(double amount) {
        System.out.println("Processing Stripe payment of $" + amount);
    }
}
```
➡️ **Allows multiple providers to follow the same contract** without forcing a hierarchy.  

---

# **Can a Class Extend Multiple Classes in Java?**  
📌 **No, Java does not support multiple inheritance with classes** because it can cause **ambiguity** (diamond problem).  

🔹 **Example of Problem in C++ (not in Java):**  
```cpp
class A {
    void show() { cout << "Class A"; }
};
class B {
    void show() { cout << "Class B"; }
};
class C : public A, public B {
    // Ambiguity! Which show() to call?
};
```
➡️ **Java avoids this issue** by **allowing multiple interfaces but not multiple class inheritance**.  

✅ **Solution in Java:** Use **interfaces** instead of multiple inheritance.  
```java
interface A { void show(); }
interface B { void show(); }

class C implements A, B {
    public void show() {
        System.out.println("Resolved show() method");
    }
}
```
➡️ No ambiguity, **clean structure**.  

---

## **🚀 Conclusion**
✅ **Abstraction** – Hides details, exposes only necessary parts (Example: Payment APIs)  
✅ **Encapsulation** – Protects data inside a class (Example: Bank Accounts)  
✅ **Inheritance** – Code reuse (Example: Employee Hierarchy)  
✅ **Polymorphism** – Same method behaves differently (Example: Notifications)  
✅ **Interfaces > Abstract Classes** – Supports multiple inheritance, flexibility  
✅ **Dynamic Method Dispatch** – Runtime polymorphism for flexible object behavior  

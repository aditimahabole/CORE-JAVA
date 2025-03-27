### **Java Variables**  

#### **What is a Variable?**  
- A **variable** is a **container** that holds a value in memory.  
- The syntax to declare a variable:  
  ```java
  DataType variableName = value;
  ```
  Example:  
  ```java
  int a = 5;
  ```

#### **Java is a Statically Typed Language**  
- Java requires you to **explicitly declare the data type** of a variable.  
- Once assigned, a variable **can only store values of that type**.  
  ```java
  int num = 10;   // ✅ Correct
  num = "Hello";  // ❌ Error: Type mismatch
  ```

#### **Java is a Strongly Typed Language**  
- Each **data type has a defined size and range**.  
- You **cannot assign values beyond the range** without explicit conversion.  
  ```java
  byte b = 128;  // ❌ Compilation error: Value out of range
  ```
- However, **type casting** can bypass this (but may lead to unexpected results).
  ```java
  byte b = (byte) 128;  // ✅ Compiles, but value becomes -128 due to overflow
  ```

#### **Variable Naming Rules**  
- **Case-sensitive** (`myVariable` and `MyVariable` are different).  
- Can contain **letters, digits, and Unicode characters**.  
- **Allowed starting characters:**  
  - A **letter** (a-z, A-Z)  
  - A **dollar sign ($)**  
  - An **underscore (_)**
- ❌ **Cannot use Java reserved keywords** (`class`, `new`, `while`, etc.).  
  ```java
  int class = 10;  // ❌ Compilation error
  ```

#### **Naming Conventions**  
- **Use camelCase** for variable names.  
  ```java
  boolean isNullOrNotNull;
  ```
- **Use uppercase for constants**.  
  ```java
  final int MAX_LIMIT = 100;
  ```

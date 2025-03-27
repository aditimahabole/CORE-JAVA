# Java Overview

## Java: Platform-Independent Language
- Java follows the **Write Once, Run Anywhere (WORA)** principle.
- It is an **Object-Oriented Programming (OOP)** language.
- Java code is **platform-independent**, meaning the same code can run on different operating systems without modification.

## Java Virtual Machine (JVM)
- JVM stands for **Java Virtual Machine**.
- It is an **abstract machine** (not physically present).
- Java programs go through the following process:
  1. **Java Source Code** (`.java` file) → **Compiler** (`javac`) → **Bytecode** (`.class` file)
  2. Bytecode is platform-independent.
  3. **JVM reads Bytecode** → Converts it to **Machine Code** → CPU executes it.
- **JVM ensures portability** by interpreting bytecode according to the underlying operating system.
- **JVM is platform-dependent**, but **Java code remains platform-independent**.
- JVM has a **JIT (Just-In-Time) Compiler**:
  - Converts bytecode to machine code at runtime for better performance.
  - JVM can read and execute any valid bytecode.

## Java Runtime Environment (JRE)
- JRE = **JVM + Core Class Libraries**.
- If we have **only JRE**, we can **run Java programs** but cannot develop them.
- We cannot have only JVM; JRE is required as it includes **JVM + Libraries**.

## Java Development Kit (JDK)
- JDK = **JRE + Compiler + Debugger + Development Tools**.
- Allows writing, compiling, and debugging Java programs.
- Includes **javac (Java Compiler)**, which converts `.java` files to `.class` files.
- **JDK contains JRE**, allowing both execution and development of Java applications.

## JVM, JDK, and JRE Comparison
| Component | Contains | Usage |
|-----------|---------|-------|
| **JVM**  | Executes Bytecode | Runs Java programs |
| **JRE**  | JVM + Class Libraries | Runs Java programs using standard libraries |
| **JDK**  | JRE + Compiler + Debugger | Develops and runs Java programs |

## Java Editions
1. **Java Standard Edition (JSE)**:
   - Core Java features, used for general-purpose development.
2. **Java Enterprise Edition (JEE) / Jakarta EE**:
   - JSE + **Transactional APIs** (Rollback, Commit), Servlets, JSP, Persistence APIs.
3. **Java Micro Edition (JME)**:
   - API for mobile applications.

## Java Program Structure
### Rules:
1. **File Name = Class Name** (if public class is present).
2. Only **one public class per file**.
3. A class can contain:
   - Variables
   - Methods
   - Constructors
   - Nested Classes
4. **`main()` method** is the entry point of the program:
   ```java
   public static void main(String[] args) {
       // Code execution starts here
   }
   ```

### Explanation of `main()` Method:
- `public` → Accessible from anywhere.
- `static` → Can be called **without creating an object**.
- `void` → Does not return any value.
- **JVM calls the `main` method automatically** when the program starts.
- If `main` is **not static**, an object of the class must be created to call it, which JVM avoids.

## Compiling and Running Java Programs
### Steps:
1. **Compile the program**:
   ```sh
   javac Filename.java
   ```
2. **Run the program**:
   ```sh
   java Filename
   ```
3. If changes are made to the code, **recompile before running**; otherwise, the old output will be displayed:
   ```sh
   javac Filename.java
   java Filename
   ```

## Additional Notes
- If we have only **JVM**, we cannot run Java programs because JVM alone does not include the necessary class libraries.
- If we have **JRE**, we can run Java programs (since it includes **JVM + standard libraries**) but **cannot compile new code**.
- JDK provides everything needed for Java development, including compilation, debugging, and execution (JRE + compiler + development tools).


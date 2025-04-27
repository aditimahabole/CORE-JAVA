Perfect — let's look at **dependency injection** using the same `UserManager` and `UserDB` example from earlier.

---

### 💡 **What Is Dependency Injection (DI)?**
Instead of creating dependencies (like `UserDB`) **inside** a class, you **inject** them from the outside — usually via constructor, setter, or a framework like Spring.

---

### ✅ Java Example with Constructor Injection

```java
// Interface (Abstraction)
public interface UserRepository {
    void saveUser(String username);
}
```

```java
// Concrete implementation
public class UserDB implements UserRepository {
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}
```

```java
// Another implementation
public class AnotherUserDB implements UserRepository {
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to AnotherUserDB");
    }
}
```

```java
// UserManager using Dependency Injection
public class UserManager {
    private UserRepository userRepo;

    // 🔑 Constructor Injection
    public UserManager(UserRepository userRepo) {
        this.userRepo = userRepo;
    }

    public void createUser(String username) {
        userRepo.saveUser(username);
    }
}
```

---

### 🧪 How to Use It

```java
public class Main {
    public static void main(String[] args) {
        // Inject UserDB
        UserRepository db = new UserDB();
        UserManager manager1 = new UserManager(db);
        manager1.createUser("Alice");

        // Inject AnotherUserDB
        UserRepository anotherDb = new AnotherUserDB();
        UserManager manager2 = new UserManager(anotherDb);
        manager2.createUser("Bob");
    }
}
```

---

### 🧠 Why Use Dependency Injection?

- **Loose Coupling** – `UserManager` doesn’t care which DB it's using.
- **Easier to Test** – You can inject mock or fake DBs for unit testing.
- **Swappable Implementations** – No need to modify `UserManager` if DB changes.

---

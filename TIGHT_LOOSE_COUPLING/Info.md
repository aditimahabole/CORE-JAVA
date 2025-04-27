Let's go step by step to show what **tight coupling** looks like between `UserManager` and `UserDB`, and how that causes problems if you want to switch to another DB.

---

### 🔒 **Tightly Coupled Example**

```java
// This is your database class
public class UserDB {
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}

// This is your tightly coupled user manager
public class UserManager {
    private UserDB userDB = new UserDB();  // 👈 direct instantiation (tight coupling)

    public void createUser(String username) {
        userDB.saveUser(username);  // UserManager depends directly on UserDB
    }
}
```

#### ❌ Problem:
If you want to use a **different database**, like `AnotherUserDB`, you have to **modify** `UserManager` itself — which breaks the **Open/Closed Principle** (open for extension, closed for modification).

---

### 😵‍💫 Trying to switch to another DB in tight coupling:

```java
public class AnotherUserDB {
    public void save(String username) {
        System.out.println("Saving " + username + " to AnotherUserDB");
    }
}

// But now UserManager doesn't work unless you change it manually:
public class UserManager {
    private AnotherUserDB anotherDB = new AnotherUserDB();  // 🔧 Had to change here

    public void createUser(String username) {
        anotherDB.save(username);  // 🔧 Also had to change method
    }
}
```

---

### ✅ **Better Way: Loose Coupling using Interface**

To solve this, you can introduce an **interface** or abstraction:

```java
// Define a contract
public interface UserRepository {
    void saveUser(String username);
}

// One implementation
public class UserDB implements UserRepository {
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}

// Another implementation
public class AnotherUserDB implements UserRepository {
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to AnotherUserDB");
    }
}

// UserManager is now loosely coupled
public class UserManager {
    private UserRepository userRepo;  // 👈 depends on abstraction

    public UserManager(UserRepository repo) {
        this.userRepo = repo;  // inject dependency
    }

    public void createUser(String username) {
        userRepo.saveUser(username);  // calls interface method
    }
}
```

### ✅ Usage:
```java
UserRepository db = new UserDB();
UserManager manager = new UserManager(db);
manager.createUser("alice");

// Switch to another DB
UserRepository anotherDb = new AnotherUserDB();
UserManager manager2 = new UserManager(anotherDb);
manager2.createUser("bob");
```


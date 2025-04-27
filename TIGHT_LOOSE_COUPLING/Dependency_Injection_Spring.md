Awesome! Let’s see how **Dependency Injection works in Spring Boot** using `@Autowired` and some Spring magic 💫

---

### 🌱 Spring Boot Example (using your `UserManager` and `UserDB` idea)

#### 🧱 Step 1: Create the Interface

```java
public interface UserRepository {
    void saveUser(String username);
}
```

---

#### 🧱 Step 2: Create Implementations

```java
import org.springframework.stereotype.Repository;

@Repository  // Tells Spring this is a bean to inject
public class UserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}
```

```java
import org.springframework.stereotype.Repository;

@Repository
public class AnotherUserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to AnotherUserDB");
    }
}
```

---

#### 🧱 Step 3: Create `UserManager` and Inject the Dependency

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service  // Marks this as a service component
public class UserManager {

    private final UserRepository userRepo;

    // 🔥 Constructor-based Dependency Injection
    @Autowired
    public UserManager(UserRepository userRepo) {
        this.userRepo = userRepo;
    }

    public void createUser(String username) {
        userRepo.saveUser(username);
    }
}
```

---

#### 🧱 Step 4: Run It from a CommandLineRunner

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootProjectApplication implements CommandLineRunner {

    @Autowired
    private UserManager userManager;

    public static void main(String[] args) {
        SpringApplication.run(SpringBootProjectApplication.class, args);
    }

    @Override
    public void run(String... args) throws Exception {
        userManager.createUser("Alice");
    }
}
```

---

### 🧠 Which `UserRepository` Gets Injected?

If you have **multiple implementations** (`UserDB` and `AnotherUserDB`), Spring will throw an error unless you:

1. Use `@Primary` on one of them:
```java
@Repository
@Primary
public class UserDB implements UserRepository {
    // ...
}
```

2. Or use `@Qualifier` to specify which one you want:
```java
@Autowired
public UserManager(@Qualifier("userDB") UserRepository repo) {
    this.userRepo = repo;
}
```

> Spring uses the bean name (usually class name with lowercase first letter) like `"userDB"` or `"anotherUserDB"`.

---

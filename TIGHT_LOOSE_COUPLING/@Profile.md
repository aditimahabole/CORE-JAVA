Perfect! Let's now explore how to use **Spring Profiles** (`@Profile`) to **switch DB implementations automatically** based on the environment — like `dev`, `prod`, `test`, etc.

This is super useful when you want different behaviors for **local dev**, **production**, or **mock databases** for **testing**.

---

## 🧩 Step-by-Step: Using `@Profile` for DB Switching

---

### 🧱 Step 1: Add Profiles to Your Implementations

#### `UserDB.java` (for `dev` profile)
```java
@Repository
@Profile("dev")
public class UserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to DEV DB (UserDB)");
    }
}
```

#### `AnotherUserDB.java` (for `prod` profile)
```java
@Repository
@Profile("prod")
public class AnotherUserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to PROD DB (AnotherUserDB)");
    }
}
```

> You can also create one for `test` if needed, e.g. `MockUserDB`.

---

### 🛠️ Step 2: Configure the Active Profile

In `application.properties` (or `application.yml`), set the active profile:

```properties
spring.profiles.active=dev
```

Or for production:

```properties
spring.profiles.active=prod
```

---

### ✅ Step 3: Leave `UserManager` Clean and Simple

```java
@Service
public class UserManager {

    private final UserRepository userRepo;

    @Autowired
    public UserManager(UserRepository userRepo) {
        this.userRepo = userRepo;
    }

    public void createUser(String username) {
        userRepo.saveUser(username);
    }
}
```

Spring will automatically inject the correct `UserRepository` implementation **based on the active profile**.

---

### 🧪 How to Run with Different Profiles

1. **Default way**: Set it in `application.properties`

2. **Command line**:
```bash
./mvnw spring-boot:run -Dspring-boot.run.profiles=prod
```

3. **VM Option in IDE** (e.g. IntelliJ):
```
-Dspring.profiles.active=prod
```

---

### 🧠 Bonus: application-{profile}.properties

You can also have separate config files like:

- `application-dev.properties`
- `application-prod.properties`
- `application-test.properties`

Spring will automatically pick the correct file based on the active profile.

--

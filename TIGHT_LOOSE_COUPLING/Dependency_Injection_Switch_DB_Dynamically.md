Awesome! Let's now make it so you can **switch between `UserDB` and `AnotherUserDB` dynamically**, using either:

- ✅ **application.properties** (Spring config)
- ✅ or using a **runtime toggle (manually or with a flag)**

---

## 🔧 Option 1: **Switch via `application.properties`**

---

### 💡 Step 1: Update your `UserRepository` Implementations

#### `UserDB.java`
```java
@Repository("userDB")
public class UserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}
```

#### `AnotherUserDB.java`
```java
@Repository("anotherUserDB")
public class AnotherUserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to AnotherUserDB");
    }
}
```

---

### 🛠️ Step 2: Add to `application.properties`

```properties
app.db.type=userDB
```

---

### 🧠 Step 3: Configure `UserManager` to Use the Config

```java
@Service
public class UserManager {

    private final UserRepository userRepo;

    @Autowired
    public UserManager(
            @Value("${app.db.type}") String dbType,
            @Qualifier("userDB") UserRepository userDB,
            @Qualifier("anotherUserDB") UserRepository anotherDB
    ) {
        if (dbType.equals("anotherUserDB")) {
            this.userRepo = anotherDB;
        } else {
            this.userRepo = userDB;
        }
    }

    public void createUser(String username) {
        userRepo.saveUser(username);
    }
}
```

---

Now you can just change `app.db.type=userDB` or `anotherUserDB` in `application.properties` without touching your code! 🎉

---

## 🧪 Option 2: Switch DB at Runtime via API (Optional)

Let’s say you want to **switch DBs while the app is running**.

You could modify `UserManager` like this:

```java
@Service
public class UserManager {

    private UserRepository userRepo;

    @Autowired
    public UserManager(@Qualifier("userDB") UserRepository userDB) {
        this.userRepo = userDB;  // default
    }

    @Autowired
    private Map<String, UserRepository> allRepos;

    public void setRepo(String repoName) {
        this.userRepo = allRepos.get(repoName);
    }

    public void createUser(String username) {
        userRepo.saveUser(username);
    }
}
```

And in your controller:

```java
@PostMapping("/set-db")
public String switchDb(@RequestParam String dbName) {
    userManager.setRepo(dbName);
    return "Switched to: " + dbName;
}
```

---

### 🔁 Example Usage:
1. POST `/api/users/set-db?dbName=anotherUserDB`
2. Then POST `/api/users?username=bob`

---

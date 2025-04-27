Nice! Let’s add a simple **REST API layer** on top of our `UserManager`, so you can test it using **Postman or a browser**.

---

### ✅ Final Structure Overview:

```
src/
├── controller/
│   └── UserController.java
├── service/
│   └── UserManager.java
├── repository/
│   ├── UserRepository.java
│   ├── UserDB.java
│   └── AnotherUserDB.java
└── SpringBootProjectApplication.java
```

---

### 🧱 Step 1: `UserRepository.java` (Interface)
```java
package com.example.repository;

public interface UserRepository {
    void saveUser(String username);
}
```

---

### 🧱 Step 2: Implementations

#### `UserDB.java`
```java
package com.example.repository;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Repository;

@Repository
@Primary  // 👈 Makes this the default
public class UserDB implements UserRepository {
    @Override
    public void saveUser(String username) {
        System.out.println("Saving " + username + " to UserDB");
    }
}
```

#### `AnotherUserDB.java`
```java
package com.example.repository;

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

### 🧱 Step 3: `UserManager.java` (Service Layer)

```java
package com.example.service;

import com.example.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

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

---

### 🧱 Step 4: `UserController.java` (REST Controller)

```java
package com.example.controller;

import com.example.service.UserManager;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserManager userManager;

    @Autowired
    public UserController(UserManager userManager) {
        this.userManager = userManager;
    }

    @PostMapping
    public String createUser(@RequestParam String username) {
        userManager.createUser(username);
        return "User " + username + " created successfully!";
    }
}
```

---

### 🚀 Step 5: `SpringBootProjectApplication.java`

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootProjectApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringBootProjectApplication.class, args);
    }
}
```

---

### 🧪 Test with Postman

- **URL**: `http://localhost:8080/api/users?username=alice`
- **Method**: `POST`

You should see:
```
User alice created successfully!
```
And in the console:
```
Saving alice to UserDB
```

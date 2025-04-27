

Instead of directly creating database objects like:

```java
UserDB udb = new UserDB();
OtherDB odb = new OtherDB();
```

We create an **interface** that defines common functions both databases should have.

Then, we make both `UserDB` and `OtherDB` **implement** that interface.  
This way, they follow the same structure.

Now, instead of using `UserDB` or `OtherDB` directly, we use a variable of the **interface type**, like:

```java
Database db = new UserDB(); // or new OtherDB();
```

We then **inject** this `db` object into `UserManager`.

So now, `UserManager` works with the interface, and it doesn’t care which actual database it's using.  
It just calls the methods from the interface, and whichever database you gave it will handle the work.

---



![image](https://github.com/user-attachments/assets/3bbb2bb5-3ae6-4bda-a9ac-64206d22fcd4)

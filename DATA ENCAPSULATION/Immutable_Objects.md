### **Real-Life Example with a Mutable Field (List)**
Let's consider a **school class (Classroom) with a list of students**.  

#### **🚨 Case 1: No Encapsulation (Bad Practice)**
```java
import java.util.List;

public class Classroom {
    public List<String> students;  // ❌ Exposed List

    public Classroom(List<String> students) {
        this.students = students;  // ❌ Directly storing reference
    }
}
```
Now, imagine this code:

```java
List<String> studentList = new ArrayList<>();
studentList.add("Alice");
studentList.add("Bob");

Classroom myClassroom = new Classroom(studentList);
System.out.println(myClassroom.students);  // Output: [Alice, Bob]

// Outside code modifies the list
studentList.add("Charlie");  // ❌ Unintended modification

System.out.println(myClassroom.students);  // Output: [Alice, Bob, Charlie] ❌ Changed!
```

- Since we **passed the original list reference**, the list inside `Classroom` **gets modified outside**.  
- Someone **outside** the `Classroom` class **added "Charlie"**, but it **changed the internal list** as well.
- This is dangerous because the classroom should control which students are added!  

---

#### **✅ Case 2: Encapsulation (Good Practice)**
```java
import java.util.ArrayList;
import java.util.List;

public class Classroom {
    private List<String> students;  // ✅ Private List

    public Classroom(List<String> students) {
        this.students = new ArrayList<>(students); // ✅ Copying the list
    }

    public List<String> getStudents() {
        return new ArrayList<>(students); // ✅ Returning a copy
    }

    public void addStudent(String student) {
        students.add(student); // ✅ Controlled modification
    }
}
```

Now, let’s see what happens:

```java
List<String> studentList = new ArrayList<>();
studentList.add("Alice");
studentList.add("Bob");

Classroom myClassroom = new Classroom(studentList);
System.out.println(myClassroom.getStudents());  // Output: [Alice, Bob]

// Outside code tries to modify the list
List<String> retrievedStudents = myClassroom.getStudents();
retrievedStudents.add("Charlie");  // ❌ This modifies only the copy, not the original list!

System.out.println(myClassroom.getStudents());  // Output: [Alice, Bob] ✅ Unchanged!
```

### **🚀 What Happens in Memory?**
1. **Original List (Box A)**
   ```
   studentList --> ["Alice", "Bob"] (Box A)
   ```
2. **Inside Constructor**
   ```
   this.students --> new ArrayList<>(students) 
                  --> ["Alice", "Bob"] (Box B) ✅ Separate copy
   ```
3. **Calling `getStudents()`**
   ```
   getStudents() returns new ArrayList<>(students)
                --> ["Alice", "Bob"] (Box C) ✅ Another copy
   ```
4. **Modifying Box C (`retrievedStudents.add("Charlie")`)**
   ```
   Box C --> ["Alice", "Bob", "Charlie"] ✅ Modified
   Box B (inside Classroom) --> ["Alice", "Bob"] ✅ Unchanged!
   ```

---

### **Why Is This Important?**
✅ Prevents **unauthorized modifications** from outside the class.  
✅ Ensures that only the **Classroom** can manage student additions.  
✅ Avoids **unexpected bugs**, keeping internal data safe.  

---

### **🎯 Real-World Example**
- Imagine a **school** that keeps a list of students **secure in a database**.
- If **everyone** could modify that list **directly**, students could be **added/removed without approval**.  
- Instead, the school **controls who can be added/removed**, just like we control list access in our class.  

That’s why **we don’t expose Box B directly** but instead **return a copy** of the list. 😊

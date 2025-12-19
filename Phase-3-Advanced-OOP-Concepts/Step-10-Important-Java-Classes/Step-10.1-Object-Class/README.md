# Step 10.1: Object Class

## Overview
The `Object` class is the root of the Java class hierarchy. Every class in Java directly or indirectly inherits from Object. Understanding Object class methods is crucial for proper Java programming.

## Key Concepts

### Important Methods of Object Class
1. `toString()` - String representation of object
2. `equals(Object obj)` - Compare objects for equality
3. `hashCode()` - Returns hash code value
4. `getClass()` - Returns runtime class
5. `clone()` - Creates copy of object
6. `finalize()` - Called by garbage collector (deprecated in Java 9)
7. `wait()`, `notify()`, `notifyAll()` - Thread synchronization

---

## Code Examples

### Example 1: toString() Method
```java
class Student {
    private String name;
    private int age;
    private double gpa;
    
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Override toString() for meaningful representation
    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + ", gpa=" + gpa + "}";
    }
}

public class ToStringDemo {
    public static void main(String[] args) {
        Student s1 = new Student("Alice", 20, 3.8);
        
        // Without overriding toString()
        // Output: Student@hashcode
        
        // With overriding toString()
        System.out.println(s1);  // Automatically calls toString()
        System.out.println(s1.toString());  // Explicit call
    }
}
```

**Output**:
```
Student{name='Alice', age=20, gpa=3.8}
Student{name='Alice', age=20, gpa=3.8}
```

### Example 2: equals() and hashCode()
```java
import java.util.Objects;

class Employee {
    private int id;
    private String name;
    private double salary;
    
    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }
    
    // Override equals() - defines object equality
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;  // Same reference
        if (obj == null || getClass() != obj.getClass()) return false;
        
        Employee employee = (Employee) obj;
        return id == employee.id &&
               Double.compare(employee.salary, salary) == 0 &&
               Objects.equals(name, employee.name);
    }
    
    // Override hashCode() - must override when overriding equals()
    @Override
    public int hashCode() {
        return Objects.hash(id, name, salary);
    }
    
    @Override
    public String toString() {
        return "Employee{id=" + id + ", name='" + name + "', salary=" + salary + "}";
    }
}

public class EqualsHashCodeDemo {
    public static void main(String[] args) {
        Employee e1 = new Employee(101, "John", 50000);
        Employee e2 = new Employee(101, "John", 50000);
        Employee e3 = new Employee(102, "Jane", 55000);
        
        // Without overriding equals() - compares references
        // System.out.println(e1 == e2);  // false (different objects)
        
        // With overriding equals() - compares content
        System.out.println("e1.equals(e2): " + e1.equals(e2));  // true
        System.out.println("e1.equals(e3): " + e1.equals(e3));  // false
        
        // hashCode()
        System.out.println("\nHash codes:");
        System.out.println("e1.hashCode(): " + e1.hashCode());
        System.out.println("e2.hashCode(): " + e2.hashCode());  // Same as e1
        System.out.println("e3.hashCode(): " + e3.hashCode());  // Different
        
        // Contract: If equals() returns true, hashCode() must be same
        if (e1.equals(e2)) {
            System.out.println("\ne1 equals e2, hash codes match: " + 
                             (e1.hashCode() == e2.hashCode()));
        }
    }
}
```

### Example 3: getClass() and clone()
```java
class Book implements Cloneable {
    private String title;
    private String author;
    private double price;
    
    public Book(String title, String author, double price) {
        this.title = title;
        this.author = author;
        this.price = price;
    }
    
    // Override clone() for object copying
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
    
    public void setPrice(double price) {
        this.price = price;
    }
    
    @Override
    public String toString() {
        return "Book{title='" + title + "', author='" + author + "', price=" + price + "}";
    }
}

public class GetClassCloneDemo {
    public static void main(String[] args) {
        try {
            Book book1 = new Book("Java Programming", "James Gosling", 45.99);
            
            // getClass() - returns runtime class
            System.out.println("Class name: " + book1.getClass().getName());
            System.out.println("Simple name: " + book1.getClass().getSimpleName());
            System.out.println("Package: " + book1.getClass().getPackage());
            
            // clone() - creates shallow copy
            Book book2 = (Book) book1.clone();
            System.out.println("\nOriginal: " + book1);
            System.out.println("Cloned: " + book2);
            
            // Modify cloned object
            book2.setPrice(39.99);
            System.out.println("\nAfter modifying clone:");
            System.out.println("Original: " + book1);
            System.out.println("Cloned: " + book2);
            
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

---

## Interview Questions (2025)

### Q1: Why should we override equals() and hashCode() together?
**Answer**:
The contract between `equals()` and `hashCode()` states:
- If two objects are equal (equals() returns true), they must have the same hash code
- If hashCode() is same, objects may or may not be equal

**Problem without overriding both**:
```java
class Person {
    String name;
    
    @Override
    public boolean equals(Object obj) {
        Person p = (Person) obj;
        return this.name.equals(p.name);
    }
    // hashCode() NOT overridden - uses default (based on memory address)
}

Person p1 = new Person("John");
Person p2 = new Person("John");

p1.equals(p2);  // true
p1.hashCode() == p2.hashCode();  // false! Violation!
```

**Impact on Collections**:
```java
Set<Person> set = new HashSet<>();
set.add(p1);
set.contains(p2);  // false! Should be true
// HashMap, HashSet rely on hashCode() for bucketing
```

**Correct implementation**:
```java
@Override
public int hashCode() {
    return Objects.hash(name);
}
```

### Q2: What is the difference between == and equals()?
**Answer**:

**== operator**:
- Compares references (memory addresses)
- For primitives, compares values
- Cannot be overridden

**equals() method**:
- Compares object content (if overridden)
- Default implementation (from Object class) uses ==
- Can be overridden for custom equality

```java
String s1 = new String("Hello");
String s2 = new String("Hello");
String s3 = s1;

System.out.println(s1 == s2);        // false (different objects)
System.out.println(s1 == s3);        // true (same reference)
System.out.println(s1.equals(s2));   // true (same content)

Integer i1 = 100;
Integer i2 = 100;
System.out.println(i1 == i2);        // true (Integer caching)

Integer i3 = 200;
Integer i4 = 200;
System.out.println(i3 == i4);        // false (outside cache range)
System.out.println(i3.equals(i4));   // true
```

### Q3: What is the purpose of toString() method?
**Answer**:
`toString()` returns a string representation of the object. Used for debugging, logging, and displaying object state.

**Default implementation** (from Object class):
```
ClassName@hashcode
```

**Why override?**
```java
class Product {
    String name;
    double price;
    
    // Without override
    // Output: Product@15db9742 (not useful)
    
    @Override
    public String toString() {
        return "Product{name='" + name + "', price=" + price + "}";
    }
}

Product p = new Product();
System.out.println(p);  // Calls toString() automatically
```

**Best practices**:
- Include all important fields
- Use meaningful format
- Don't include sensitive data (passwords)

---

## Practice Exercises

1. Create a `Car` class and override `equals()`, `hashCode()`, and `toString()`
2. Demonstrate the difference between shallow and deep copy using `clone()`
3. Test the behavior of `equals()` and `==` with String objects

---

## Next Step
Continue to **Step 10.2: String Class** to learn about string manipulation.

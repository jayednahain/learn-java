# Step 7: Classes & Objects in Java

## What are Classes and Objects?

### Class
A **class** is a blueprint or template for creating objects. It defines the structure (data) and behavior (methods) that objects of that type will have.

Think of a class as a cookie cutter - it defines the shape and pattern.

### Object
An **object** is an instance of a class. It's a real entity created from the class blueprint with actual values.

Think of an object as the actual cookie made from the cookie cutter.

---

## Key Concepts

### 1. **Creating a Class**
```java
public class ClassName {
    // Instance variables (data/properties)
    // Constructors
    // Methods (behavior)
}
```

### 2. **Creating Objects (Instantiation)**
```java
ClassName objectName = new ClassName();
```

### 3. **Constructors**
- Special method used to initialize objects
- Same name as the class
- No return type (not even void)
- Types:
  - **Default constructor**: No parameters
  - **Parameterized constructor**: Takes parameters
  - **Constructor overloading**: Multiple constructors with different parameters

### 4. **`this` Keyword**
- Refers to the current object
- Used to differentiate instance variables from parameters
- Can call other constructors in the same class

### 5. **Instance vs Class Variables**
- **Instance variables**: Each object has its own copy
- **Class variables (static)**: Shared by all objects of the class

---

## Examples

### Example 1: Simple Class with Constructor

```java
public class Car {
    // Instance variables
    String brand;
    String model;
    int year;
    
    // Default constructor
    public Car() {
        brand = "Unknown";
        model = "Unknown";
        year = 0;
    }
    
    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;  // 'this' refers to instance variable
        this.model = model;
        this.year = year;
    }
    
    // Method to display car information
    public void displayInfo() {
        System.out.println("Brand: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Year: " + year);
    }
    
    public static void main(String[] args) {
        // Creating objects using different constructors
        Car car1 = new Car(); // Using default constructor
        Car car2 = new Car("Toyota", "Camry", 2024); // Using parameterized constructor
        
        System.out.println("Car 1:");
        car1.displayInfo();
        
        System.out.println("\nCar 2:");
        car2.displayInfo();
    }
}
```

**Output:**
```
Car 1:
Brand: Unknown
Model: Unknown
Year: 0

Car 2:
Brand: Toyota
Model: Camry
Year: 2024
```

---

### Example 2: Constructor Overloading and `this` Keyword

```java
public class BankAccount {
    private String accountNumber;
    private String accountHolder;
    private double balance;
    
    // Constructor 1: Only account number
    public BankAccount(String accountNumber) {
        this.accountNumber = accountNumber;
        this.accountHolder = "Anonymous";
        this.balance = 0.0;
    }
    
    // Constructor 2: Account number and holder name
    public BankAccount(String accountNumber, String accountHolder) {
        this(accountNumber); // Calling another constructor
        this.accountHolder = accountHolder;
    }
    
    // Constructor 3: All parameters
    public BankAccount(String accountNumber, String accountHolder, double balance) {
        this(accountNumber, accountHolder); // Calling another constructor
        this.balance = balance;
    }
    
    public void deposit(double amount) {
        this.balance += amount;
        System.out.println("Deposited: $" + amount);
    }
    
    public void displayAccountInfo() {
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Account Holder: " + accountHolder);
        System.out.println("Balance: $" + balance);
    }
    
    public static void main(String[] args) {
        BankAccount acc1 = new BankAccount("ACC001");
        BankAccount acc2 = new BankAccount("ACC002", "John Doe");
        BankAccount acc3 = new BankAccount("ACC003", "Jane Smith", 5000.0);
        
        System.out.println("Account 1:");
        acc1.displayAccountInfo();
        
        System.out.println("\nAccount 2:");
        acc2.displayAccountInfo();
        
        System.out.println("\nAccount 3:");
        acc3.displayAccountInfo();
        
        acc2.deposit(1000);
        System.out.println("\nAfter deposit:");
        acc2.displayAccountInfo();
    }
}
```

**Output:**
```
Account 1:
Account Number: ACC001
Account Holder: Anonymous
Balance: $0.0

Account 2:
Account Number: ACC002
Account Holder: John Doe
Balance: $0.0

Account 3:
Account Number: ACC003
Account Holder: Jane Smith
Balance: $5000.0

Deposited: $1000.0

After deposit:
Account Number: ACC002
Account Holder: John Doe
Balance: $1000.0
```

---

### Example 3: Instance vs Static Variables

```java
public class Student {
    // Instance variables - unique for each student
    String name;
    int rollNumber;
    
    // Static variable - shared by all students
    static String schoolName = "ABC High School";
    static int totalStudents = 0;
    
    // Constructor
    public Student(String name, int rollNumber) {
        this.name = name;
        this.rollNumber = rollNumber;
        totalStudents++; // Increment for each new student
    }
    
    // Instance method
    public void displayStudentInfo() {
        System.out.println("Name: " + name);
        System.out.println("Roll Number: " + rollNumber);
        System.out.println("School: " + schoolName);
    }
    
    // Static method
    public static void displaySchoolInfo() {
        System.out.println("School Name: " + schoolName);
        System.out.println("Total Students: " + totalStudents);
    }
    
    public static void main(String[] args) {
        Student s1 = new Student("Alice", 101);
        Student s2 = new Student("Bob", 102);
        Student s3 = new Student("Charlie", 103);
        
        System.out.println("Student 1:");
        s1.displayStudentInfo();
        
        System.out.println("\nStudent 2:");
        s2.displayStudentInfo();
        
        System.out.println("\nSchool Information:");
        Student.displaySchoolInfo(); // Called using class name
        
        // Changing static variable affects all objects
        Student.schoolName = "XYZ International School";
        
        System.out.println("\nAfter changing school name:");
        s1.displayStudentInfo();
        s3.displayStudentInfo();
    }
}
```

**Output:**
```
Student 1:
Name: Alice
Roll Number: 101
School: ABC High School

Student 2:
Name: Bob
Roll Number: 102
School: ABC High School

School Information:
School Name: ABC High School
Total Students: 3

After changing school name:
Name: Alice
Roll Number: 101
School: XYZ International School
Name: Charlie
Roll Number: 103
School: XYZ International School
```

---

## Interview Questions (2025)

### Question 1: What is the difference between a class and an object? Can you have a class without objects?

**Answer:**

| Aspect | Class | Object |
|--------|-------|--------|
| **Definition** | Blueprint/Template | Instance of a class |
| **Memory** | No memory allocated | Memory allocated when created |
| **Existence** | Logical entity | Physical entity |
| **Creation** | Declared using `class` keyword | Created using `new` keyword |
| **Example** | Car (blueprint) | myCar (actual car) |

**Yes, you can have a class without creating objects:**
- Utility classes with only static methods (e.g., `Math`, `Arrays`)
- Classes used only for inheritance
- Singleton pattern (controlled object creation)

**Example:**
```java
public class MathUtils {
    // Private constructor prevents object creation
    private MathUtils() {}
    
    public static int add(int a, int b) {
        return a + b;
    }
}

// Usage: MathUtils.add(5, 3) - No object needed!
```

---

### Question 2: What happens if you don't define a constructor in your class?

**Answer:**
If you don't define any constructor, **Java automatically provides a default no-argument constructor** that initializes instance variables to their default values:
- Numeric types: 0
- boolean: false
- Objects: null

**Example:**
```java
public class Person {
    String name;
    int age;
    // No constructor defined
}

// Java provides:
// public Person() {
//     // Instance variables initialized to defaults
//     // name = null, age = 0
// }

public class Main {
    public static void main(String[] args) {
        Person p = new Person(); // Works! Uses default constructor
        System.out.println(p.name); // Output: null
        System.out.println(p.age);  // Output: 0
    }
}
```

**Important:** Once you define ANY constructor (even parameterized), Java will NOT provide the default constructor.

```java
public class Person {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// This will cause ERROR:
Person p = new Person(); // Compilation error! No default constructor
```

---

### Question 3: Explain the use of `this` keyword with examples.

**Answer:**
The `this` keyword refers to the current object. It has multiple uses:

**1. Differentiate instance variables from parameters:**
```java
public class Employee {
    String name;
    
    public Employee(String name) {
        this.name = name; // this.name = instance variable, name = parameter
    }
}
```

**2. Call one constructor from another (constructor chaining):**
```java
public class Box {
    int length, width, height;
    
    public Box() {
        this(0, 0, 0); // Calls parameterized constructor
    }
    
    public Box(int length, int width, int height) {
        this.length = length;
        this.width = width;
        this.height = height;
    }
}
```

**3. Pass current object as a parameter:**
```java
public class Button {
    public void click() {
        EventHandler handler = new EventHandler();
        handler.handle(this); // Passing current Button object
    }
}
```

**4. Return current object:**
```java
public class Calculator {
    int result = 0;
    
    public Calculator add(int value) {
        result += value;
        return this; // Method chaining
    }
    
    public Calculator multiply(int value) {
        result *= value;
        return this;
    }
}

// Usage:
Calculator calc = new Calculator();
calc.add(5).multiply(2).add(3); // Method chaining
```

---

### Question 4: What is the difference between instance variables and static variables?

**Answer:**

| Feature | Instance Variables | Static Variables |
|---------|-------------------|------------------|
| **Keyword** | No keyword | `static` keyword |
| **Memory** | Separate copy for each object | Single copy shared by all objects |
| **Access** | Through object | Through class name (recommended) |
| **Initialization** | When object is created | When class is loaded |
| **Lifetime** | Until object exists | Until program ends |
| **Use Case** | Object-specific data | Shared data across all objects |

**Example:**
```java
public class Counter {
    int instanceCount = 0;      // Instance variable
    static int staticCount = 0; // Static variable
    
    public Counter() {
        instanceCount++;
        staticCount++;
    }
    
    public void display() {
        System.out.println("Instance: " + instanceCount + ", Static: " + staticCount);
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        c1.display(); // Instance: 1, Static: 1
        
        Counter c2 = new Counter();
        c2.display(); // Instance: 1, Static: 2
        
        Counter c3 = new Counter();
        c3.display(); // Instance: 1, Static: 3
        
        c1.display(); // Instance: 1, Static: 3 (static shared!)
    }
}
```

**When to use static:**
- Constants (e.g., `static final double PI = 3.14159`)
- Counters (tracking total objects created)
- Utility methods that don't depend on object state
- Configuration values shared across all instances

---

### Question 5: Can constructors be private? If yes, why would you make a constructor private?

**Answer:**
**Yes, constructors can be private.** This is used in several design patterns:

**1. Singleton Pattern (Only one instance allowed):**
```java
public class Database {
    private static Database instance = null;
    
    // Private constructor prevents external instantiation
    private Database() {
        System.out.println("Database connection created");
    }
    
    // Public method to get the single instance
    public static Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }
}

// Usage:
Database db1 = Database.getInstance();
Database db2 = Database.getInstance(); // Same instance as db1
// Database db = new Database(); // ERROR! Constructor is private
```

**2. Factory Method Pattern:**
```java
public class Employee {
    private String name;
    private String type;
    
    // Private constructor
    private Employee(String name, String type) {
        this.name = name;
        this.type = type;
    }
    
    // Factory methods
    public static Employee createEngineer(String name) {
        return new Employee(name, "Engineer");
    }
    
    public static Employee createManager(String name) {
        return new Employee(name, "Manager");
    }
}

// Usage:
Employee eng = Employee.createEngineer("John");
Employee mgr = Employee.createManager("Jane");
```

**3. Utility Class (Only static methods):**
```java
public class MathUtility {
    // Private constructor prevents instantiation
    private MathUtility() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    public static int square(int x) {
        return x * x;
    }
}
```

**Reasons to use private constructor:**
- Control object creation (Singleton)
- Prevent instantiation (Utility classes)
- Force users to use factory methods
- Implement design patterns

---

## Practice Exercises

1. Create a `Book` class with properties (title, author, ISBN, price) and demonstrate constructor overloading
2. Create a `Circle` class with static variable for PI and calculate area/circumference
3. Implement a simple `ShoppingCart` class that tracks total items using a static variable
4. Create a `Person` class and demonstrate method chaining using `this` keyword
5. Implement a Singleton pattern for a `Logger` class

---

## Key Takeaways

✅ Class is a blueprint, object is an instance of the class  
✅ Constructors initialize objects and have the same name as the class  
✅ `this` keyword refers to the current object  
✅ Instance variables are unique to each object  
✅ Static variables are shared by all objects of the class  
✅ Java provides a default constructor if you don't define any  
✅ Private constructors are used for Singleton and Utility classes  
✅ Constructor chaining improves code reusability  

**Next Step:** Move to [Step 8.1: Encapsulation](../Step-8.1-Encapsulation/) to learn about protecting your data!

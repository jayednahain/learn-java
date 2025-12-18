# Step 8.1: Encapsulation - Data Hiding in Java

## What is Encapsulation?

**Encapsulation** is the bundling of data (variables) and methods that operate on that data within a single unit (class), while restricting direct access to some of the object's components. It's one of the four fundamental OOP principles.

### Simple Explanation
Think of encapsulation like a **capsule** 💊 - the medicine (data) is protected inside, and you can only access it through the proper interface (methods).

**Real-world analogy:** An ATM machine
- You can't directly access the cash inside (private data)
- You must use the interface - buttons, card reader (public methods)
- The internal mechanism is hidden from you (implementation details)

---

## Key Concepts

### 1. **Access Modifiers**

Java provides four access modifiers to control visibility:

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| **public** | ✅ | ✅ | ✅ | ✅ |
| **protected** | ✅ | ✅ | ✅ | ❌ |
| **default** (no modifier) | ✅ | ✅ | ❌ | ❌ |
| **private** | ✅ | ❌ | ❌ | ❌ |

### 2. **Getters and Setters**
- **Getter (accessor)**: Retrieves the value of a private variable
- **Setter (mutator)**: Sets/modifies the value of a private variable

### 3. **Why Encapsulation Matters**
✅ **Data Protection**: Prevent unauthorized access and modification  
✅ **Flexibility**: Change implementation without affecting other code  
✅ **Validation**: Control how data is set (e.g., age can't be negative)  
✅ **Read-Only/Write-Only**: Create read-only or write-only properties  
✅ **Maintainability**: Easier to modify and maintain code  

---

## Examples

### Example 1: Basic Encapsulation with Getters and Setters

```java
public class Person {
    // Private instance variables - cannot be accessed directly
    private String name;
    private int age;
    private String email;
    
    // Constructor
    public Person(String name, int age, String email) {
        this.name = name;
        setAge(age);  // Using setter for validation
        this.email = email;
    }
    
    // Getter for name
    public String getName() {
        return name;
    }
    
    // Setter for name
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name;
        } else {
            System.out.println("Invalid name!");
        }
    }
    
    // Getter for age
    public int getAge() {
        return age;
    }
    
    // Setter for age with validation
    public void setAge(int age) {
        if (age > 0 && age < 150) {
            this.age = age;
        } else {
            System.out.println("Invalid age! Must be between 1 and 149");
        }
    }
    
    // Getter for email
    public String getEmail() {
        return email;
    }
    
    // Setter for email with validation
    public void setEmail(String email) {
        if (email != null && email.contains("@")) {
            this.email = email;
        } else {
            System.out.println("Invalid email format!");
        }
    }
    
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Email: " + email);
    }
}

class Main {
    public static void main(String[] args) {
        Person person = new Person("John Doe", 25, "john@example.com");
        
        // Accessing private data through getters
        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());
        
        // Modifying data through setters
        person.setAge(30);  // Valid
        person.setAge(-5);  // Invalid - validation in setter
        person.setEmail("invalidemail");  // Invalid
        person.setEmail("john.new@example.com");  // Valid
        
        System.out.println("\nUpdated Information:");
        person.displayInfo();
        
        // person.age = -10; // ERROR! Cannot access private variable directly
    }
}
```

**Output:**
```
Name: John Doe
Age: 25
Invalid age! Must be between 1 and 149
Invalid email format!

Updated Information:
Name: John Doe
Age: 30
Email: john.new@example.com
```

---

### Example 2: Read-Only and Write-Only Properties

```java
public class BankAccount {
    private String accountNumber;
    private double balance;
    private String password;
    
    public BankAccount(String accountNumber, double initialBalance, String password) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
        this.password = password;
    }
    
    // Read-only property - only getter, no setter
    public String getAccountNumber() {
        return accountNumber;
    }
    
    // Read-only property with formatted output
    public double getBalance() {
        return balance;
    }
    
    // Write-only property - only setter, no getter (for security)
    public void setPassword(String oldPassword, String newPassword) {
        if (this.password.equals(oldPassword)) {
            this.password = newPassword;
            System.out.println("Password changed successfully!");
        } else {
            System.out.println("Incorrect old password!");
        }
    }
    
    // Controlled methods to modify balance
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount!");
        }
    }
    
    public void withdraw(double amount, String password) {
        if (!this.password.equals(password)) {
            System.out.println("Incorrect password!");
            return;
        }
        
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient balance!");
        }
    }
    
    public void displayAccountInfo(String password) {
        if (this.password.equals(password)) {
            System.out.println("Account Number: " + accountNumber);
            System.out.println("Balance: $" + balance);
        } else {
            System.out.println("Access denied! Incorrect password.");
        }
    }
}

class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("ACC12345", 1000.0, "secret123");
        
        // Read-only: Can get account number but can't change it
        System.out.println("Account: " + account.getAccountNumber());
        // account.setAccountNumber("NEW123"); // No such method exists!
        
        account.deposit(500);
        account.withdraw(200, "secret123");
        
        System.out.println("\nAccount Info:");
        account.displayAccountInfo("secret123");
        
        // Change password (write-only)
        account.setPassword("secret123", "newPassword456");
        account.withdraw(100, "newPassword456");
        
        System.out.println("\nFinal Balance: $" + account.getBalance());
    }
}
```

**Output:**
```
Account: ACC12345
Deposited: $500.0
Withdrawn: $200.0

Account Info:
Account Number: ACC12345
Balance: $1300.0
Password changed successfully!
Withdrawn: $100.0

Final Balance: $1200.0
```

---

### Example 3: Encapsulation with Business Logic

```java
public class Employee {
    private String employeeId;
    private String name;
    private double baseSalary;
    private double bonus;
    
    // Constants (typically public static final)
    public static final double MAX_BONUS_PERCENTAGE = 0.50; // 50%
    public static final double MIN_SALARY = 30000.0;
    
    public Employee(String employeeId, String name, double baseSalary) {
        this.employeeId = employeeId;
        this.name = name;
        setBaseSalary(baseSalary);
        this.bonus = 0.0;
    }
    
    public String getEmployeeId() {
        return employeeId;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public double getBaseSalary() {
        return baseSalary;
    }
    
    public void setBaseSalary(double baseSalary) {
        if (baseSalary >= MIN_SALARY) {
            this.baseSalary = baseSalary;
        } else {
            System.out.println("Salary cannot be less than $" + MIN_SALARY);
            this.baseSalary = MIN_SALARY;
        }
    }
    
    public double getBonus() {
        return bonus;
    }
    
    public void setBonus(double bonus) {
        double maxBonus = baseSalary * MAX_BONUS_PERCENTAGE;
        if (bonus >= 0 && bonus <= maxBonus) {
            this.bonus = bonus;
        } else {
            System.out.println("Bonus must be between $0 and $" + maxBonus);
        }
    }
    
    // Calculated property - no direct setter
    public double getTotalSalary() {
        return baseSalary + bonus;
    }
    
    // Business logic encapsulated within the class
    public void giveRaise(double percentage) {
        if (percentage > 0 && percentage <= 20) {
            double raiseAmount = baseSalary * (percentage / 100);
            baseSalary += raiseAmount;
            System.out.println("Raise of " + percentage + "% applied. New salary: $" + baseSalary);
        } else {
            System.out.println("Raise percentage must be between 0 and 20%");
        }
    }
    
    public void displayEmployeeInfo() {
        System.out.println("Employee ID: " + employeeId);
        System.out.println("Name: " + name);
        System.out.println("Base Salary: $" + baseSalary);
        System.out.println("Bonus: $" + bonus);
        System.out.println("Total Salary: $" + getTotalSalary());
    }
}

class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("EMP001", "Alice Johnson", 50000);
        
        emp.displayEmployeeInfo();
        
        System.out.println("\n--- Setting Bonus ---");
        emp.setBonus(10000);  // Valid
        emp.setBonus(30000);  // Invalid (exceeds 50%)
        
        System.out.println("\n--- Giving Raise ---");
        emp.giveRaise(10);    // Valid 10% raise
        emp.giveRaise(25);    // Invalid (exceeds 20%)
        
        System.out.println("\n--- Final Information ---");
        emp.displayEmployeeInfo();
    }
}
```

**Output:**
```
Employee ID: EMP001
Name: Alice Johnson
Base Salary: $50000.0
Bonus: $0.0
Total Salary: $50000.0

--- Setting Bonus ---
Bonus must be between $0 and $25000.0

--- Giving Raise ---
Raise of 10.0% applied. New salary: $55000.0
Raise percentage must be between 0 and 20%

--- Final Information ---
Employee ID: EMP001
Name: Alice Johnson
Base Salary: $55000.0
Bonus: $10000.0
Total Salary: $65000.0
```

---

## Interview Questions (2025)

### Question 1: What is encapsulation and why is it important in Java?

**Answer:**
Encapsulation is the bundling of data and methods that operate on that data within a single unit (class), while restricting direct access to the internal state of the object.

**Key Benefits:**

1. **Data Protection**: Private variables prevent unauthorized access
2. **Controlled Access**: Getters/setters provide controlled access with validation
3. **Flexibility**: Internal implementation can change without affecting external code
4. **Maintainability**: Changes are localized to the class
5. **Security**: Sensitive data can be hidden from external access

**Example:**
```java
public class CreditCard {
    private String cardNumber;  // Hidden
    private String cvv;         // Hidden
    private double balance;     // Hidden
    
    // Only masked version is exposed
    public String getMaskedCardNumber() {
        return "****-****-****-" + cardNumber.substring(12);
    }
    
    // CVV is never exposed
    public boolean validateCVV(String inputCVV) {
        return this.cvv.equals(inputCVV);
    }
}
```

**Without encapsulation**, anyone could do:
```java
card.cardNumber = "1234567890123456"; // Direct access - dangerous!
card.balance = 1000000; // Fraudulent modification!
```

**With encapsulation**, these operations are controlled and validated.

---

### Question 2: Explain the difference between all four access modifiers with examples.

**Answer:**

| Modifier | Same Class | Same Package | Subclass (different package) | Other Classes |
|----------|------------|--------------|------------------------------|---------------|
| **private** | ✅ | ❌ | ❌ | ❌ |
| **default** | ✅ | ✅ | ❌ | ❌ |
| **protected** | ✅ | ✅ | ✅ | ❌ |
| **public** | ✅ | ✅ | ✅ | ✅ |

**Example:**
```java
// File: package1/Parent.java
package package1;

public class Parent {
    public int publicVar = 10;
    protected int protectedVar = 20;
    int defaultVar = 30;              // default (package-private)
    private int privateVar = 40;
    
    public void display() {
        System.out.println(publicVar);    // ✅ Accessible
        System.out.println(protectedVar); // ✅ Accessible
        System.out.println(defaultVar);   // ✅ Accessible
        System.out.println(privateVar);   // ✅ Accessible
    }
}

// File: package1/SamePackageClass.java
package package1;

public class SamePackageClass {
    public void test() {
        Parent p = new Parent();
        System.out.println(p.publicVar);    // ✅ Accessible
        System.out.println(p.protectedVar); // ✅ Accessible
        System.out.println(p.defaultVar);   // ✅ Accessible
        // System.out.println(p.privateVar); // ❌ Error!
    }
}

// File: package2/Child.java
package package2;
import package1.Parent;

public class Child extends Parent {
    public void test() {
        System.out.println(publicVar);    // ✅ Accessible
        System.out.println(protectedVar); // ✅ Accessible (through inheritance)
        // System.out.println(defaultVar);   // ❌ Error!
        // System.out.println(privateVar);   // ❌ Error!
    }
}

// File: package2/UnrelatedClass.java
package package2;
import package1.Parent;

public class UnrelatedClass {
    public void test() {
        Parent p = new Parent();
        System.out.println(p.publicVar); // ✅ Accessible
        // System.out.println(p.protectedVar); // ❌ Error!
        // System.out.println(p.defaultVar);   // ❌ Error!
        // System.out.println(p.privateVar);   // ❌ Error!
    }
}
```

**When to use:**
- **private**: Internal implementation details
- **default**: Package-level access (utility classes within package)
- **protected**: For inheritance (subclasses need access)
- **public**: Public API that should be accessible everywhere

---

### Question 3: Why do we need getters and setters? Can't we just make variables public?

**Answer:**
While you *can* make variables public, getters and setters provide several advantages:

**1. Validation and Business Logic:**
```java
// Bad: Public variable - no validation
public class Person {
    public int age; // Anyone can set negative age!
}
person.age = -50; // No error!

// Good: Setter with validation
public class Person {
    private int age;
    
    public void setAge(int age) {
        if (age >= 0 && age <= 150) {
            this.age = age;
        } else {
            throw new IllegalArgumentException("Invalid age");
        }
    }
}
```

**2. Read-Only or Write-Only Properties:**
```java
public class Order {
    private String orderId;
    private LocalDateTime createdAt;
    
    // Read-only: getter exists, but no setter
    public String getOrderId() {
        return orderId;
    }
    
    public LocalDateTime getCreatedAt() {
        return createdAt;
    }
}
```

**3. Computed/Derived Values:**
```java
public class Rectangle {
    private double width;
    private double height;
    
    // Calculated on-the-fly, not stored
    public double getArea() {
        return width * height;
    }
}
```

**4. Future Flexibility:**
```java
// Version 1: Simple field
public class User {
    private String name;
    public String getName() { return name; }
}

// Version 2: Can add logging without changing API
public class User {
    private String name;
    public String getName() {
        logAccess("name field accessed");
        return name;
    }
}
```

**5. Encapsulation and Abstraction:**
```java
public class Temperature {
    private double celsius;
    
    public double getCelsius() {
        return celsius;
    }
    
    public double getFahrenheit() {
        return (celsius * 9/5) + 32;
    }
    
    public void setCelsius(double celsius) {
        this.celsius = celsius;
    }
    
    public void setFahrenheit(double fahrenheit) {
        this.celsius = (fahrenheit - 32) * 5/9;
    }
}
```

---

### Question 4: What is the difference between encapsulation and abstraction?

**Answer:**

| Aspect | Encapsulation | Abstraction |
|--------|---------------|-------------|
| **Focus** | Data hiding | Implementation hiding |
| **Purpose** | Protect data and control access | Hide complexity, show only essential features |
| **How** | Access modifiers, getters/setters | Abstract classes, interfaces |
| **Level** | Data level | Design level |
| **Example** | Private variables with public methods | Abstract class defining contract |

**Encapsulation Example:**
```java
public class BankAccount {
    private double balance; // Data hiding
    
    public void deposit(double amount) { // Controlled access
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

**Abstraction Example:**
```java
abstract class Vehicle {
    abstract void start(); // What to do, not how
    abstract void stop();
}

class Car extends Vehicle {
    void start() {
        // Car-specific implementation (how)
        System.out.println("Turn key to start");
    }
    
    void stop() {
        System.out.println("Press brake pedal");
    }
}
```

**Simple way to remember:**
- **Encapsulation**: "Hiding data" (using private, getters/setters)
- **Abstraction**: "Hiding implementation" (using abstract classes/interfaces)

---

### Question 5: In modern Java, are getters and setters still recommended, or should we use Records (Java 14+)?

**Answer:**
**Both have their place in 2025:**

**Use Traditional Getters/Setters when:**
- You need mutable objects
- Complex validation logic is required
- Business logic in getters/setters
- Need inheritance
- Backward compatibility with older Java versions

**Use Records when:**
- Immutable data carriers (DTOs)
- Simple data structures
- No business logic needed
- Cleaner, more concise code
- Working with Java 14+ projects

**Comparison:**

```java
// Traditional Class (mutable, with validation)
public class Person {
    private String name;
    private int age;
    
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    public int getAge() { return age; }
    public void setAge(int age) {
        if (age >= 0) this.age = age;
    }
}

// Record (immutable, no validation)
public record PersonRecord(String name, int age) {
    // Compact constructor for validation
    public PersonRecord {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
}

// Usage
PersonRecord person = new PersonRecord("John", 25);
System.out.println(person.name()); // Accessor method
// person.name = "Jane"; // ERROR! Records are immutable
```

**Modern Best Practice (2025):**
- Use **Records** for DTOs, API responses, configuration objects
- Use **traditional classes** when you need mutability or complex behavior
- Consider **Lombok** (@Getter, @Setter, @Data) for boilerplate reduction in traditional classes

```java
// Using Lombok (if available)
import lombok.Data;

@Data
public class User {
    private String username;
    private String email;
    private int age;
}
// Lombok auto-generates getters, setters, toString, equals, hashCode
```

---

## Practice Exercises

1. Create a `BankAccount` class with proper encapsulation and validation (no negative balance, withdrawal limits)
2. Design a `Product` class with read-only ID and mutable price with validation
3. Implement a `Temperature` class that stores Celsius but provides both Celsius and Fahrenheit getters/setters
4. Create a `User` class with password field that is write-only (no getter for password)
5. Build a `Circle` class with private radius and computed area/circumference

---

## Key Takeaways

✅ Encapsulation = Data Hiding + Controlled Access  
✅ Use **private** for variables, **public** for methods  
✅ Getters/setters provide validation and flexibility  
✅ Read-only properties have getter but no setter  
✅ Write-only properties have setter but no getter  
✅ Access modifiers: private < default < protected < public  
✅ Encapsulation improves security, flexibility, and maintainability  
✅ In 2025, consider Records for immutable data, traditional classes for mutable objects  

**Next Step:** Move to [Step 8.2: Inheritance](../Step-8.2-Inheritance/) to learn about code reusability through inheritance!

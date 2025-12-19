# Step 17: Exceptions

## What are Exceptions?

**Exception** is an abnormal event that disrupts the normal flow of a program. Java provides a robust exception handling mechanism to handle runtime errors.

### Exception Hierarchy:
```
Throwable
├── Error (Unrecoverable: OutOfMemoryError, StackOverflowError)
└── Exception
    ├── RuntimeException (Unchecked)
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── ArithmeticException
    │   └── IllegalArgumentException
    └── IOException, SQLException, etc. (Checked)
```

---

## Checked vs Unchecked Exceptions

| Type | Checked Exceptions | Unchecked Exceptions |
|------|-------------------|----------------------|
| **Check Time** | Compile-time | Runtime |
| **Handling** | Must handle | Optional |
| **Extends** | Exception class | RuntimeException class |
| **Examples** | IOException, SQLException | NullPointerException, ArrayIndexOutOfBoundsException |

---

## Keywords

- **try**: Code that might throw exception
- **catch**: Handle exception
- **finally**: Always executes (cleanup code)
- **throw**: Manually throw exception
- **throws**: Declare exceptions a method might throw

---

## Example 1: Basic Exception Handling

```java
public class BasicExceptionHandling {
    public static void main(String[] args) {
        System.out.println("=== Try-Catch Example ===");
        
        try {
            int result = 10 / 0;  // ArithmeticException
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
            System.out.println("Exception: " + e.getMessage());
        }
        
        System.out.println("Program continues...\n");
        
        // Multiple catch blocks
        System.out.println("=== Multiple Catch Blocks ===");
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]);  // ArrayIndexOutOfBoundsException
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic error: " + e);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index error: " + e.getMessage());
        } catch (Exception e) {
            System.out.println("General exception: " + e);
        }
        
        // Multi-catch (Java 7+)
        System.out.println("\n=== Multi-Catch Block ===");
        try {
            String str = null;
            System.out.println(str.length());  // NullPointerException
        } catch (NullPointerException | ArrayIndexOutOfBoundsException e) {
            System.out.println("Caught: " + e.getClass().getSimpleName());
        }
    }
}
```

---

## Example 2: Finally Block

```java
public class FinallyBlockExample {
    public static void main(String[] args) {
        System.out.println("=== Finally Block ===");
        
        try {
            System.out.println("In try block");
            int result = 10 / 2;
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("In catch block");
        } finally {
            System.out.println("In finally block - Always executes!");
        }
        
        System.out.println("\n=== Finally with Exception ===");
        try {
            System.out.println("In try block");
            int result = 10 / 0;  // Exception
        } catch (ArithmeticException e) {
            System.out.println("In catch block");
        } finally {
            System.out.println("Finally executes even after exception");
        }
        
        // Try-finally without catch
        System.out.println("\n=== Try-Finally (No Catch) ===");
        try {
            System.out.println("Opening resource...");
        } finally {
            System.out.println("Closing resource in finally");
        }
    }
}
```

---

## Example 3: Custom Exceptions

```java
// Custom checked exception
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// Custom unchecked exception
class InvalidAgeException extends RuntimeException {
    public InvalidAgeException(String message) {
        super(message);
    }
}

class BankAccount {
    private double balance;
    
    public BankAccount(double balance) {
        this.balance = balance;
    }
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException(
                "Insufficient funds! Balance: " + balance + ", Requested: " + amount
            );
        }
        balance -= amount;
        System.out.println("Withdrawn: $" + amount + ", Remaining: $" + balance);
    }
    
    public double getBalance() {
        return balance;
    }
}

class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        if (age < 0 || age > 150) {
            throw new InvalidAgeException("Age must be between 0 and 150");
        }
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class CustomExceptionExample {
    public static void main(String[] args) {
        System.out.println("=== Custom Checked Exception ===");
        BankAccount account = new BankAccount(1000);
        
        try {
            account.withdraw(500);   // Success
            account.withdraw(600);   // InsufficientFundsException
        } catch (InsufficientFundsException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        System.out.println("\n=== Custom Unchecked Exception ===");
        try {
            Person p1 = new Person("Alice", 25);
            System.out.println(p1);
            
            Person p2 = new Person("Bob", 200);  // InvalidAgeException
        } catch (InvalidAgeException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 2025 Interview Questions

**Q1: What is the difference between checked and unchecked exceptions?**
**A:** Checked exceptions are checked at compile-time (must handle). Unchecked exceptions are checked at runtime (optional to handle).

**Q2: Can we have try without catch?**
**A:** Yes, with finally block: `try { } finally { }`

**Q3: Can we have multiple catch blocks?**
**A:** Yes, but specific exceptions must come before general Exception class.

**Q4: What is the difference between throw and throws?**
**A:**
- `throw`: Used to explicitly throw an exception
- `throws`: Used in method signature to declare exceptions

**Q5: When does finally block not execute?**
**A:** When `System.exit()` is called, or JVM crashes, or infinite loop in try/catch.

**Q6: Can we rethrow an exception?**
**A:** Yes:
```java
try {
    // code
} catch (Exception e) {
    // handle
    throw e;  // rethrow
}
```

**Q7: What is try-with-resources?**
**A:** Automatic resource management (Java 7+):
```java
try (FileReader fr = new FileReader("file.txt")) {
    // use resource
}  // Automatically closed
```

---

**Next:** [Phase 6: Step 18 - Generics](../../Phase-6-Advanced-Topics/Step-18-Generics/README.md)

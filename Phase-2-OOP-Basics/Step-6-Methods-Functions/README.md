# Step 6: Methods/Functions in Java

## What are Methods?

A **method** is a block of code that performs a specific task. Methods help organize code, make it reusable, and easier to maintain. In Java, methods are defined inside classes.

### Method Syntax

```java
accessModifier returnType methodName(parameters) {
    // method body
    return value; // if returnType is not void
}
```

## Key Concepts

### 1. **Method Parameters**
- Java uses **pass by value** - a copy of the variable is passed
- Parameters are variables that receive values when the method is called

### 2. **Return Types**
- **void**: Method doesn't return any value
- **Data type** (int, String, etc.): Method returns a value of that type

### 3. **Method Overloading**
- Multiple methods with the same name but different parameters
- Differentiating factors: number of parameters, type of parameters, or order

### 4. **Static vs Instance Methods**
- **Static methods**: Belong to the class, called using class name
- **Instance methods**: Belong to objects, need an object to be called

### 5. **Variable Scope**
- **Local variables**: Declared inside a method, accessible only within that method
- **Instance variables**: Declared in class, accessible to all instance methods
- **Class variables (static)**: Declared with static keyword, shared by all instances

---

## Examples

### Example 1: Basic Method with Return Type

```java
public class Calculator {
    
    // Method to add two numbers
    public int add(int a, int b) {
        int sum = a + b;
        return sum;
    }
    
    // Method to check if number is even
    public boolean isEven(int number) {
        return number % 2 == 0;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        int result = calc.add(10, 20);
        System.out.println("Sum: " + result); // Output: Sum: 30
        
        boolean evenCheck = calc.isEven(15);
        System.out.println("Is 15 even? " + evenCheck); // Output: Is 15 even? false
    }
}
```

### Example 2: Method Overloading

```java
public class MathOperations {
    
    // Method to multiply two integers
    public int multiply(int a, int b) {
        return a * b;
    }
    
    // Overloaded method to multiply three integers
    public int multiply(int a, int b, int c) {
        return a * b * c;
    }
    
    // Overloaded method to multiply two doubles
    public double multiply(double a, double b) {
        return a * b;
    }
    
    public static void main(String[] args) {
        MathOperations math = new MathOperations();
        
        System.out.println(math.multiply(5, 3));           // Output: 15
        System.out.println(math.multiply(2, 3, 4));        // Output: 24
        System.out.println(math.multiply(2.5, 4.0));       // Output: 10.0
    }
}
```

### Example 3: Static vs Instance Methods

```java
public class Employee {
    String name;
    static String companyName = "Tech Corp"; // Class variable
    
    // Instance method - needs an object
    public void displayEmployeeInfo() {
        System.out.println("Name: " + name);
        System.out.println("Company: " + companyName);
    }
    
    // Static method - can be called without creating object
    public static void displayCompanyInfo() {
        System.out.println("Company Name: " + companyName);
        // System.out.println(name); // ERROR! Can't access instance variable
    }
    
    public static void main(String[] args) {
        // Calling static method using class name
        Employee.displayCompanyInfo();
        
        // Creating object to call instance method
        Employee emp = new Employee();
        emp.name = "John Doe";
        emp.displayEmployeeInfo();
    }
}
```

**Output:**
```
Company Name: Tech Corp
Name: John Doe
Company: Tech Corp
```

---

## Interview Questions (2025)

### Question 1: What is method overloading and can you overload a method by changing only the return type?

**Answer:**
Method overloading allows multiple methods with the same name but different parameters (number, type, or order). 

**No, you cannot overload a method by changing only the return type.** The method signature (method name + parameters) must be different. Return type alone is not part of the method signature.

**Example:**
```java
// Valid overloading
public int calculate(int a) { return a * 2; }
public int calculate(int a, int b) { return a + b; }

// Invalid overloading - Compilation Error!
public int process(int x) { return x; }
public double process(int x) { return x * 2.0; } // ERROR!
```

---

### Question 2: What is the difference between static and instance methods? When would you use each?

**Answer:**

| Aspect | Static Method | Instance Method |
|--------|---------------|-----------------|
| **Belongs to** | Class | Object/Instance |
| **Memory** | Loaded when class is loaded | Created with each object |
| **Calling** | `ClassName.methodName()` | `objectName.methodName()` |
| **Access** | Can access only static members | Can access both static and instance members |
| **`this` keyword** | Cannot use | Can use |

**When to use Static:**
- Utility methods (Math.sqrt(), Arrays.sort())
- Factory methods
- Methods that don't depend on object state
- Example: `public static int max(int a, int b)`

**When to use Instance:**
- Methods that operate on object's data
- Methods that need access to instance variables
- Example: `public void setName(String name)`

**Code Example:**
```java
public class BankAccount {
    private double balance; // instance variable
    private static double interestRate = 0.05; // static variable
    
    // Instance method - works with object's balance
    public void deposit(double amount) {
        this.balance += amount;
    }
    
    // Static method - utility function
    public static double calculateInterest(double principal, int years) {
        return principal * interestRate * years;
    }
}
```

---

### Question 3: Explain pass by value in Java with an example. What happens when you pass an object to a method?

**Answer:**
Java is **strictly pass by value**. This means:
- For primitives: A copy of the value is passed
- For objects: A copy of the reference (memory address) is passed, not the object itself

**Example:**
```java
public class PassByValueDemo {
    
    public static void modifyPrimitive(int num) {
        num = 100; // Changes local copy only
    }
    
    public static void modifyObject(StringBuilder sb) {
        sb.append(" World"); // Modifies the actual object
    }
    
    public static void reassignObject(StringBuilder sb) {
        sb = new StringBuilder("New Object"); // Changes local reference only
    }
    
    public static void main(String[] args) {
        // Primitive example
        int x = 10;
        modifyPrimitive(x);
        System.out.println("x = " + x); // Output: x = 10 (unchanged)
        
        // Object example
        StringBuilder str = new StringBuilder("Hello");
        modifyObject(str);
        System.out.println("str = " + str); // Output: str = Hello World (modified)
        
        reassignObject(str);
        System.out.println("str = " + str); // Output: str = Hello World (unchanged)
    }
}
```

**Key Point:** You can modify the object's contents through the reference, but you cannot change which object the original reference points to.

---

### Question 4: What is variable shadowing in methods? Provide an example.

**Answer:**
Variable shadowing occurs when a local variable has the same name as an instance variable, causing the local variable to "shadow" or hide the instance variable within that method's scope.

**Example:**
```java
public class Student {
    private String name = "John"; // Instance variable
    
    public void setName(String name) { // Parameter shadows instance variable
        name = name; // Assigns parameter to itself - BUG!
        // To fix, use 'this' keyword
    }
    
    public void setNameCorrectly(String name) {
        this.name = name; // 'this.name' refers to instance variable
    }
    
    public void display() {
        String name = "Local Name"; // Local variable shadows instance variable
        System.out.println(name);      // Prints: Local Name
        System.out.println(this.name); // Prints: John (instance variable)
    }
}
```

**Best Practice:** Use the `this` keyword to refer to instance variables when there's a naming conflict.

---

### Question 5: Can we overload the main method in Java? Will it run?

**Answer:**
**Yes, you can overload the main method**, but only the standard signature `public static void main(String[] args)` will be called by the JVM to start the program.

**Example:**
```java
public class MainOverload {
    
    // Standard main method - Entry point
    public static void main(String[] args) {
        System.out.println("Standard main method");
        main(10); // Call overloaded main
        main("Hello"); // Call another overloaded main
    }
    
    // Overloaded main method
    public static void main(int num) {
        System.out.println("Overloaded main with int: " + num);
    }
    
    // Another overloaded main method
    public static void main(String str) {
        System.out.println("Overloaded main with String: " + str);
    }
}
```

**Output:**
```
Standard main method
Overloaded main with int: 10
Overloaded main with String: Hello
```

**Important:** The overloaded versions won't run automatically - you must explicitly call them from the standard main method.

---

## Practice Exercises

1. Create a method that takes an array and returns the largest element
2. Write multiple overloaded methods to calculate the area of different shapes (circle, rectangle, triangle)
3. Create a utility class with static methods for common string operations (reverse, palindrome check, etc.)
4. Implement a method that demonstrates variable scope by using local, instance, and static variables

---

## Key Takeaways

✅ Methods make code reusable and organized  
✅ Java uses pass by value for both primitives and objects  
✅ Method overloading allows same name with different parameters  
✅ Static methods belong to class, instance methods belong to objects  
✅ Use `this` keyword to refer to instance variables in case of shadowing  
✅ Return type alone cannot differentiate overloaded methods  

**Next Step:** Move to [Step 7: Classes & Objects](../Step-7-Classes-Objects/) to learn how to create your own data types!

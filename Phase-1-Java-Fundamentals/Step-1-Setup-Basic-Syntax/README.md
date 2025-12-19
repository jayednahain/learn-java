# Step 1: Setup & Basic Syntax

## Overview
This is your first step into Java programming. You'll learn how to set up your development environment and write your first Java program.

## Key Concepts

### 1. What is Java?
- **Java** is a high-level, object-oriented programming language
- **Platform Independent**: Write once, run anywhere (WORA)
- Used for web applications, mobile apps (Android), enterprise software, and more

### 2. Understanding JVM, JRE, and JDK

- **JVM (Java Virtual Machine)**: Executes Java bytecode. Makes Java platform-independent.
- **JRE (Java Runtime Environment)**: JVM + Libraries needed to run Java applications
- **JDK (Java Development Kit)**: JRE + Development tools (compiler, debugger)

**Remember**: JDK > JRE > JVM

### 3. Java File Structure
Every Java program must have:
- A **class** declaration
- A **main method** (entry point of the program)

```
class → method → statements
```

---

## Code Examples

### Example 1: Hello World Program
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Explanation**:
- `public class HelloWorld`: Declares a public class named HelloWorld
- `public static void main(String[] args)`: The main method - program starts here
- `System.out.println()`: Prints text to console with a new line

### Example 2: Basic User Greeting
```java
public class Greeting {
    public static void main(String[] args) {
        String name = "Java Learner";
        System.out.println("Welcome, " + name + "!");
        System.out.println("Let's start coding!");
    }
}
```

**Explanation**:
- Creates a String variable to store a name
- Uses string concatenation with `+` operator
- Demonstrates multiple print statements

### Example 3: Simple Calculations
```java
public class Calculator {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 5;
        int sum = num1 + num2;
        
        System.out.println("First Number: " + num1);
        System.out.println("Second Number: " + num2);
        System.out.println("Sum: " + sum);
    }
}
```

**Explanation**:
- Declares integer variables
- Performs basic arithmetic
- Displays results using println

---

## Important Points to Remember

1. **File Naming**: Java filename must match the public class name (e.g., `HelloWorld.java`)
2. **Case Sensitivity**: Java is case-sensitive (`Main` ≠ `main`)
3. **Semicolons**: Every statement must end with a semicolon `;`
4. **Curly Braces**: Define blocks of code `{ }`
5. **main method**: Must be exactly `public static void main(String[] args)`

---

## Interview Questions (2025)

### Q1: What is the difference between JDK, JRE, and JVM?
**Answer**: 
- **JDK (Java Development Kit)**: Complete development environment containing JRE plus development tools like javac (compiler), debugger, and other utilities. Used by developers to write and compile Java code.
- **JRE (Java Runtime Environment)**: Runtime environment containing JVM plus Java class libraries. Used to run Java applications.
- **JVM (Java Virtual Machine)**: Virtual machine that executes Java bytecode. Provides platform independence by converting bytecode to machine-specific code.

**Relationship**: JDK contains JRE, and JRE contains JVM.

### Q2: Why is Java called "platform-independent"?
**Answer**: 
Java is platform-independent because of the JVM (Java Virtual Machine). When you compile Java code, it's converted to bytecode (.class files) rather than machine-specific code. This bytecode can run on any platform that has a JVM installed. The JVM interprets the bytecode and translates it to machine-specific instructions. This allows the same Java program to run on Windows, macOS, Linux, etc., without modification - "Write Once, Run Anywhere" (WORA).

### Q3: What is the purpose of the main method in Java?
**Answer**: 
The main method is the entry point of any Java application. When you run a Java program, the JVM looks for the main method to start execution. The signature must be exactly:
```java
public static void main(String[] args)
```
- **public**: Accessible from anywhere (JVM can call it)
- **static**: Can be called without creating an object
- **void**: Doesn't return any value
- **String[] args**: Command-line arguments passed to the program

### Q4: What happens when you compile and run a Java program?
**Answer**: 
1. **Compilation** (`javac HelloWorld.java`):
   - Java compiler (javac) reads the source code (.java file)
   - Checks for syntax errors
   - Converts source code to bytecode (.class file)
   - Bytecode is platform-independent

2. **Execution** (`java HelloWorld`):
   - JVM loads the .class file
   - Verifies the bytecode
   - Interprets/JIT compiles bytecode to machine code
   - Executes the program starting from the main method

### Q5: Can we have multiple classes in a single Java file? Can we have multiple public classes?
**Answer**: 
- **Yes**, you can have multiple classes in a single Java file.
- **No**, you can have only **one public class** per file, and the filename must match that public class name.
- Other classes in the file can be package-private (no access modifier).

Example:
```java
// File: Main.java
public class Main {
    public static void main(String[] args) {
        Helper h = new Helper();
    }
}

class Helper {  // package-private class
    // helper code
}
```

### Q6: What is bytecode in Java?
**Answer**: 
Bytecode is an intermediate, platform-independent code that Java source code is compiled into. It's stored in .class files and consists of instructions that the JVM can understand and execute. Bytecode is not human-readable and not machine-specific. The JVM's interpreter or JIT (Just-In-Time) compiler converts bytecode to native machine code at runtime. This is what enables Java's platform independence.

### Q7: What are the different ways to print output in Java?
**Answer**: 
1. **System.out.println()**: Prints and moves to next line
2. **System.out.print()**: Prints without moving to next line
3. **System.out.printf()**: Formatted output (like C printf)

Example:
```java
System.out.println("Hello");  // Hello\n
System.out.print("World");    // World
System.out.printf("Number: %d", 5);  // Number: 5
```

### Q8: What is the use of the `args` parameter in the main method?
**Answer**: 
The `String[] args` parameter holds command-line arguments passed to the program when it's executed.

Example:
```java
// File: Test.java
public class Test {
    public static void main(String[] args) {
        System.out.println("First argument: " + args[0]);
    }
}
```
Run: `java Test Hello`
Output: `First argument: Hello`

---

## Practice Exercises

1. Write a program that prints your name, age, and favorite programming language
2. Create a program that calculates the area of a rectangle (length × width)
3. Write a program that takes two numbers and displays their sum, difference, product, and quotient
4. Create a program that prints a pattern using System.out.println()

---

## Next Step
Once you're comfortable with basic syntax and can write simple programs, move to **Step 2: Data Types & Variables** to learn how to store and manipulate different types of data.

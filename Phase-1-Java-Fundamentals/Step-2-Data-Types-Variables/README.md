# Step 2: Data Types & Variables

## Overview
Learn how to store and manipulate data using variables and understand different data types in Java.

## Key Concepts

### 1. What is a Variable?
A variable is a container that holds data that can be changed during program execution.

```
Syntax: dataType variableName = value;
```

### 2. Data Types in Java

Java has two categories of data types:

#### **Primitive Data Types** (8 types)
| Type | Size | Range | Default | Example |
|------|------|-------|---------|---------|
| `byte` | 1 byte | -128 to 127 | 0 | `byte age = 25;` |
| `short` | 2 bytes | -32,768 to 32,767 | 0 | `short year = 2025;` |
| `int` | 4 bytes | -2³¹ to 2³¹-1 | 0 | `int salary = 50000;` |
| `long` | 8 bytes | -2⁶³ to 2⁶³-1 | 0L | `long population = 8000000000L;` |
| `float` | 4 bytes | ~6-7 decimal digits | 0.0f | `float price = 19.99f;` |
| `double` | 8 bytes | ~15 decimal digits | 0.0d | `double pi = 3.14159;` |
| `char` | 2 bytes | 0 to 65,535 (Unicode) | '\u0000' | `char grade = 'A';` |
| `boolean` | 1 bit | true or false | false | `boolean isActive = true;` |

#### **Non-Primitive (Reference) Data Types**
- `String`, Arrays, Classes, Interfaces, etc.
- Store references to objects, not actual values

### 3. Type Casting

**Implicit Casting (Automatic)** - smaller to larger
```
byte → short → int → long → float → double
```

**Explicit Casting (Manual)** - larger to smaller
```java
int num = (int) 10.5;  // Explicit cast
```

### 4. Constants
Use `final` keyword to create constants (values that cannot be changed)
```java
final double PI = 3.14159;
```

---

## Code Examples

### Example 1: Working with Different Data Types
```java
public class DataTypesDemo {
    public static void main(String[] args) {
        // Integer types
        byte age = 25;
        short year = 2025;
        int population = 1400000000;
        long distanceToSun = 149600000000L;  // L suffix for long
        
        // Floating-point types
        float temperature = 36.6f;  // f suffix for float
        double accountBalance = 15000.50;
        
        // Character and boolean
        char grade = 'A';
        boolean isPassed = true;
        
        // String (non-primitive)
        String name = "Java Developer";
        
        // Printing values
        System.out.println("Age: " + age);
        System.out.println("Year: " + year);
        System.out.println("Temperature: " + temperature + "°C");
        System.out.println("Grade: " + grade);
        System.out.println("Passed: " + isPassed);
        System.out.println("Name: " + name);
    }
}
```

**Output**:
```
Age: 25
Year: 2025
Temperature: 36.6°C
Grade: A
Passed: true
Name: Java Developer
```

### Example 2: Type Casting
```java
public class TypeCastingDemo {
    public static void main(String[] args) {
        // Implicit Casting (Widening)
        int num1 = 100;
        double num2 = num1;  // Automatic conversion
        System.out.println("Int to Double: " + num2);  // 100.0
        
        // Explicit Casting (Narrowing)
        double price = 99.99;
        int roundedPrice = (int) price;  // Manual conversion
        System.out.println("Double to Int: " + roundedPrice);  // 99 (decimal lost)
        
        // Character to int
        char letter = 'A';
        int asciiValue = letter;  // Implicit
        System.out.println("ASCII of A: " + asciiValue);  // 65
        
        // Arithmetic with casting
        int a = 10;
        int b = 3;
        double result = (double) a / b;  // Cast to avoid integer division
        System.out.println("10 / 3 = " + result);  // 3.3333...
    }
}
```

**Output**:
```
Int to Double: 100.0
Double to Int: 99
ASCII of A: 65
10 / 3 = 3.3333333333333335
```

### Example 3: Constants and Variable Scope
```java
public class ConstantsDemo {
    public static void main(String[] args) {
        // Constants using final
        final double PI = 3.14159;
        final int MAX_USERS = 100;
        final String APP_NAME = "MyApp";
        
        // Using constants in calculations
        double radius = 5.0;
        double area = PI * radius * radius;
        double circumference = 2 * PI * radius;
        
        System.out.println("Application: " + APP_NAME);
        System.out.println("Max Users: " + MAX_USERS);
        System.out.println("Circle Area: " + area);
        System.out.println("Circle Circumference: " + circumference);
        
        // PI = 3.14;  // Error! Cannot reassign final variable
        
        // Variable naming conventions
        int studentAge = 20;          // camelCase for variables
        String firstName = "John";    // camelCase
        final double TAX_RATE = 0.18; // UPPER_CASE for constants
    }
}
```

---

## Important Points to Remember

1. **Naming Rules**:
   - Must start with a letter, `$`, or `_`
   - Cannot use Java keywords (int, class, public, etc.)
   - Case-sensitive (`age` ≠ `Age`)
   - Use camelCase for variables (`studentName`)
   - Use UPPER_CASE for constants (`MAX_VALUE`)

2. **Default Values** (for class variables):
   - Numeric types: 0
   - boolean: false
   - char: '\u0000'
   - Reference types: null

3. **Integer Literals**:
   - Decimal: `int num = 100;`
   - Hexadecimal: `int hex = 0x64;`
   - Binary: `int bin = 0b1100100;`

4. **Underscores in Numbers** (Java 7+):
   ```java
   int million = 1_000_000;  // More readable
   ```

---

## Interview Questions (2025)

### Q1: What is the difference between primitive and non-primitive data types?
**Answer**:

**Primitive Data Types**:
- Predefined by Java (8 types)
- Store actual values
- Stored in stack memory
- Cannot be null
- Have default values
- Examples: int, boolean, char, double

**Non-Primitive (Reference) Data Types**:
- Created by programmer (except String, Arrays)
- Store memory addresses (references)
- Stored in heap memory
- Can be null
- Default value is null
- Examples: String, Arrays, Classes, Interfaces

### Q2: Why do we need to add 'f' or 'L' suffix to float and long literals?
**Answer**:
- By default, decimal numbers are treated as `double` and whole numbers as `int`
- **float**: Need 'f' or 'F' suffix to specify it's a float, not double
  ```java
  float price = 19.99f;  // Correct
  float price = 19.99;   // Error! double to float requires casting
  ```
- **long**: Need 'L' or 'l' suffix for values outside int range
  ```java
  long big = 3000000000L;  // Correct
  long big = 3000000000;   // Error! Out of int range
  ```

### Q3: What is the difference between int and Integer?
**Answer**:
- **int**: Primitive data type
  - Stores actual integer value
  - Cannot be null
  - Default value: 0
  - Faster (stored in stack)
  - Cannot call methods on it

- **Integer**: Wrapper class (non-primitive)
  - Stores reference to Integer object
  - Can be null
  - Default value: null
  - Slower (stored in heap)
  - Can call methods: `parseInt()`, `toString()`, etc.

```java
int num1 = 10;        // Primitive
Integer num2 = 10;    // Object (autoboxing)
Integer num3 = null;  // Valid
// int num4 = null;   // Error!
```

### Q4: What is autoboxing and unboxing?
**Answer**:
**Autoboxing**: Automatic conversion of primitive to wrapper object
```java
int num = 5;
Integer obj = num;  // Autoboxing (int → Integer)
```

**Unboxing**: Automatic conversion of wrapper object to primitive
```java
Integer obj = 10;
int num = obj;  // Unboxing (Integer → int)
```

Introduced in Java 5 to make code cleaner. Used with Collections which work only with objects.

### Q5: What is type casting? Explain widening and narrowing.
**Answer**:
Type casting is converting one data type to another.

**Widening (Implicit/Automatic)**:
- Converting smaller type to larger type
- No data loss
- Automatic
- Path: byte → short → int → long → float → double

```java
int num = 100;
double d = num;  // Automatic
```

**Narrowing (Explicit/Manual)**:
- Converting larger type to smaller type
- Possible data loss
- Requires explicit cast

```java
double d = 100.99;
int num = (int) d;  // num = 100 (decimal lost)
```

### Q6: Can we change the value of a final variable?
**Answer**:
No, once a `final` variable is initialized, its value cannot be changed.

```java
final int MAX = 100;
// MAX = 200;  // Compilation Error!
```

**However**:
- For final object references, the reference cannot change, but object state can:
```java
final StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // Valid! Modifying object state
// sb = new StringBuilder();  // Error! Cannot reassign reference
```

### Q7: What will happen if you don't initialize a local variable?
**Answer**:
**Local variables** must be explicitly initialized before use. If not initialized, you'll get a **compilation error**.

```java
public void method() {
    int num;
    System.out.println(num);  // Error! Variable might not be initialized
}
```

**Instance variables** (class-level) get default values automatically:
```java
class Test {
    int num;  // Automatically initialized to 0
}
```

### Q8: What is the size of char in Java and why?
**Answer**:
- **Size**: 2 bytes (16 bits)
- **Reason**: Java uses Unicode character set (UTF-16) instead of ASCII
- Unicode supports international characters (Chinese, Arabic, etc.)
- Range: 0 to 65,535 (can represent 65,536 characters)
- In C/C++, char is 1 byte (ASCII only)

```java
char letter = 'A';      // English
char chinese = '中';    // Chinese character
char emoji = '😊';      // Some emojis (BMP)
```

### Q9: What is the default value of variables in Java?
**Answer**:

**Instance Variables (class-level)**:
- Numeric: 0 (int, long, float, double, etc.)
- boolean: false
- char: '\u0000' (null character)
- Object references: null

**Local Variables**:
- No default value
- Must be explicitly initialized before use

**Static Variables**:
- Same default values as instance variables

### Q10: Can we use underscores in numeric literals? (Java 7+)
**Answer**:
Yes, Java 7 introduced underscores in numeric literals for better readability.

```java
int million = 1_000_000;
long creditCard = 1234_5678_9012_3456L;
double pi = 3.14_15_92_65;
int binary = 0b1010_1010_1010;
```

**Rules**:
- Cannot be at beginning or end
- Cannot be adjacent to decimal point
- Cannot be before L or F suffix

---

## Practice Exercises

1. Create variables of all 8 primitive types and print their values
2. Write a program to convert temperature from Celsius to Fahrenheit
3. Demonstrate widening and narrowing type casting
4. Calculate the area and perimeter of a rectangle using appropriate data types
5. Create constants for common values (PI, MAX_AGE, etc.) and use them

---

## Next Step
Move to **Step 3: Operators** to learn how to perform operations on variables and values.

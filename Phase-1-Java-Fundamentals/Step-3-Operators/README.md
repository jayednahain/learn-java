# Step 3: Operators

## Overview
Operators are special symbols that perform operations on variables and values. Java provides rich set of operators for arithmetic, comparison, logical operations, and more.

## Key Concepts

### 1. Types of Operators

1. **Arithmetic Operators**: +, -, *, /, %
2. **Relational/Comparison Operators**: ==, !=, >, <, >=, <=
3. **Logical Operators**: &&, ||, !
4. **Assignment Operators**: =, +=, -=, *=, /=, %=
5. **Increment/Decrement**: ++, --
6. **Ternary Operator**: ? :
7. **Bitwise Operators**: &, |, ^, ~, <<, >>, >>>
8. **instanceof Operator**: Check object type

### 2. Operator Precedence
```
Highest → Lowest
1. Postfix: expr++, expr--
2. Unary: ++expr, --expr, +, -, !, ~
3. Multiplicative: *, /, %
4. Additive: +, -
5. Shift: <<, >>, >>>
6. Relational: <, >, <=, >=, instanceof
7. Equality: ==, !=
8. Logical AND: &&
9. Logical OR: ||
10. Ternary: ? :
11. Assignment: =, +=, -=, etc.
```

---

## Code Examples

### Example 1: Arithmetic Operators
```java
public class ArithmeticDemo {
    public static void main(String[] args) {
        int a = 20;
        int b = 10;
        
        // Basic arithmetic
        System.out.println("Addition: " + (a + b));        // 30
        System.out.println("Subtraction: " + (a - b));     // 10
        System.out.println("Multiplication: " + (a * b));  // 200
        System.out.println("Division: " + (a / b));        // 2
        System.out.println("Modulus: " + (a % b));         // 0
        
        // Division behavior
        int x = 10;
        int y = 3;
        System.out.println("Integer Division: " + (x / y));        // 3 (not 3.33)
        System.out.println("Double Division: " + ((double)x / y)); // 3.333...
        
        // Modulus examples
        System.out.println("17 % 5 = " + (17 % 5));  // 2
        System.out.println("20 % 4 = " + (20 % 4));  // 0
        
        // Negative numbers
        System.out.println("-10 % 3 = " + (-10 % 3));  // -1
        System.out.println("10 % -3 = " + (10 % -3));  // 1
    }
}
```

### Example 2: Relational, Logical, and Increment Operators
```java
public class OperatorsDemo {
    public static void main(String[] args) {
        // Relational Operators
        int age = 25;
        int minAge = 18;
        
        System.out.println("age > minAge: " + (age > minAge));    // true
        System.out.println("age < minAge: " + (age < minAge));    // false
        System.out.println("age >= 25: " + (age >= 25));          // true
        System.out.println("age == 25: " + (age == 25));          // true
        System.out.println("age != 30: " + (age != 30));          // true
        
        // Logical Operators
        boolean hasLicense = true;
        boolean hasInsurance = true;
        
        System.out.println("\nLogical AND (&&):");
        System.out.println(hasLicense && hasInsurance);  // true (both true)
        System.out.println(hasLicense && !hasInsurance); // false
        
        System.out.println("\nLogical OR (||):");
        System.out.println(hasLicense || false);  // true (at least one true)
        System.out.println(false || false);       // false
        
        System.out.println("\nLogical NOT (!):");
        System.out.println(!hasLicense);          // false
        System.out.println(!false);               // true
        
        // Increment/Decrement
        int count = 5;
        System.out.println("\nIncrement/Decrement:");
        System.out.println("Original: " + count);           // 5
        System.out.println("Post-increment: " + count++);   // 5 (then becomes 6)
        System.out.println("After post-increment: " + count); // 6
        System.out.println("Pre-increment: " + (++count));  // 7 (increment first)
        System.out.println("Post-decrement: " + count--);   // 7 (then becomes 6)
        System.out.println("Pre-decrement: " + (--count));  // 5 (decrement first)
    }
}
```

### Example 3: Assignment and Ternary Operators
```java
public class AssignmentTernaryDemo {
    public static void main(String[] args) {
        // Assignment Operators
        int num = 10;
        System.out.println("Initial value: " + num);
        
        num += 5;  // num = num + 5
        System.out.println("After += 5: " + num);  // 15
        
        num -= 3;  // num = num - 3
        System.out.println("After -= 3: " + num);  // 12
        
        num *= 2;  // num = num * 2
        System.out.println("After *= 2: " + num);  // 24
        
        num /= 4;  // num = num / 4
        System.out.println("After /= 4: " + num);  // 6
        
        num %= 4;  // num = num % 4
        System.out.println("After %= 4: " + num);  // 2
        
        // Ternary Operator (condition ? valueIfTrue : valueIfFalse)
        int age = 20;
        String status = (age >= 18) ? "Adult" : "Minor";
        System.out.println("\nAge: " + age + ", Status: " + status);
        
        // Nested ternary
        int marks = 75;
        String grade = (marks >= 90) ? "A" :
                       (marks >= 80) ? "B" :
                       (marks >= 70) ? "C" :
                       (marks >= 60) ? "D" : "F";
        System.out.println("Marks: " + marks + ", Grade: " + grade);
        
        // Finding max using ternary
        int a = 15, b = 25;
        int max = (a > b) ? a : b;
        System.out.println("Max of " + a + " and " + b + " is: " + max);
    }
}
```

---

## Important Points to Remember

1. **Integer Division**: `5 / 2 = 2` (not 2.5). Use casting for decimal result.

2. **Modulus Sign**: Result of `%` has same sign as dividend
   - `10 % 3 = 1`
   - `-10 % 3 = -1`

3. **Short-Circuit Evaluation**:
   ```java
   false && expression  // expression not evaluated
   true || expression   // expression not evaluated
   ```

4. **Increment/Decrement**:
   - `++i` (pre): Increment first, then use
   - `i++` (post): Use first, then increment

5. **String Concatenation**:
   ```java
   "Result: " + 5 + 3  // "Result: 53"
   "Result: " + (5 + 3) // "Result: 8"
   ```

---

## Interview Questions (2025)

### Q1: What is the difference between ++i and i++?
**Answer**:
- **++i (Pre-increment)**: Increments value first, then returns it
- **i++ (Post-increment)**: Returns current value, then increments

```java
int i = 5;
System.out.println(++i);  // Output: 6, i becomes 6
System.out.println(i);    // Output: 6

int j = 5;
System.out.println(j++);  // Output: 5, then j becomes 6
System.out.println(j);    // Output: 6
```

**In expressions**:
```java
int a = 5;
int b = ++a;  // a=6, b=6

int x = 5;
int y = x++;  // x=6, y=5
```

### Q2: What is the difference between & and && operators?
**Answer**:
Both are logical AND operators, but with key differences:

**&& (Conditional/Short-circuit AND)**:
- If first operand is false, second is NOT evaluated
- More efficient
- Used for boolean expressions

**& (Bitwise AND)**:
- Always evaluates both operands
- Works on individual bits
- Can be used with boolean and integers

```java
// Short-circuit example
int x = 5;
if (false && (++x > 0)) {  // ++x is NOT executed
    // ...
}
System.out.println(x);  // 5

// Bitwise example
if (false & (++x > 0)) {  // ++x IS executed
    // ...
}
System.out.println(x);  // 6

// Bitwise on integers
int a = 5;  // 0101
int b = 3;  // 0011
System.out.println(a & b);  // 1 (0001)
```

**Same applies to || vs |**

### Q3: What is the output of 10 / 3 and 10.0 / 3 in Java?
**Answer**:
- **10 / 3**: Integer division = `3` (decimal part truncated)
- **10.0 / 3**: Double division = `3.3333333333333335`

```java
System.out.println(10 / 3);      // 3
System.out.println(10.0 / 3);    // 3.3333333333333335
System.out.println(10 / 3.0);    // 3.3333333333333335
System.out.println((double)10/3); // 3.3333333333333335
```

**Rule**: If at least one operand is double/float, result is double/float.

### Q4: Explain the ternary operator with an example.
**Answer**:
The ternary operator is a shorthand for if-else. Syntax:
```
condition ? valueIfTrue : valueIfFalse
```

**Example**:
```java
int age = 20;
String status = (age >= 18) ? "Adult" : "Minor";
// Equivalent to:
String status;
if (age >= 18) {
    status = "Adult";
} else {
    status = "Minor";
}

// Finding maximum
int max = (a > b) ? a : b;

// Nested ternary
int marks = 75;
String grade = (marks >= 90) ? "A" :
               (marks >= 75) ? "B" : "C";
```

**Use case**: Simple conditional assignments. Avoid complex nested ternaries for readability.

### Q5: What is operator precedence? Give an example.
**Answer**:
Operator precedence determines the order in which operators are evaluated in an expression. Higher precedence operators execute first.

**Order (High to Low)**:
1. Parentheses `()`
2. Unary: `++`, `--`, `!`, `-`
3. Multiplicative: `*`, `/`, `%`
4. Additive: `+`, `-`
5. Relational: `<`, `>`, `<=`, `>=`
6. Equality: `==`, `!=`
7. Logical AND: `&&`
8. Logical OR: `||`
9. Ternary: `? :`
10. Assignment: `=`, `+=`, etc.

**Example**:
```java
int result = 10 + 5 * 2;  // 20 (not 30)
// 5 * 2 evaluated first (precedence), then + 10

int a = 5, b = 10, c = 15;
boolean flag = a < b && b < c;  // true
// Relational operators before &&

int x = 10 + 5 > 12 ? 100 : 200;  // 100
// 10+5 → 15>12 → true → 100
```

**Use parentheses** for clarity: `int result = 10 + (5 * 2);`

### Q6: What will be the output: System.out.println("5" + 3 + 2)?
**Answer**:
Output: `"532"`

**Explanation**:
- `+` operator evaluated left-to-right
- `"5" + 3` → String concatenation → `"53"`
- `"53" + 2` → String concatenation → `"532"`

**Different scenarios**:
```java
System.out.println("5" + 3 + 2);      // "532" (string concat)
System.out.println(5 + 3 + "2");      // "82" (8 + "2")
System.out.println("5" + (3 + 2));    // "55" (parentheses first)
System.out.println(5 + 3 + 2);        // 10 (all numeric)
```

**Rule**: If any operand is String, `+` performs concatenation.

### Q7: What is the difference between = and ==?
**Answer**:
- **= (Assignment operator)**: Assigns value to a variable
  ```java
  int x = 10;  // Assigns 10 to x
  ```

- **== (Equality operator)**: Compares two values, returns boolean
  ```java
  if (x == 10) {  // Checks if x equals 10
      // true
  }
  ```

**Common mistake**:
```java
int x = 5;
if (x = 10) {  // Error in Java! (Valid in C/C++)
    // Assignment, not comparison
}

// Correct:
if (x == 10) {
    // Comparison
}
```

**For objects** (like String):
```java
String s1 = new String("hello");
String s2 = new String("hello");
System.out.println(s1 == s2);       // false (different references)
System.out.println(s1.equals(s2));  // true (same content)
```

### Q8: Explain short-circuit evaluation in logical operators.
**Answer**:
Short-circuit evaluation means the second operand is evaluated only if needed.

**&& (AND)**:
- If first operand is `false`, result is always `false`
- Second operand not evaluated

**|| (OR)**:
- If first operand is `true`, result is always `true`
- Second operand not evaluated

**Example**:
```java
int x = 5;
// && short-circuit
if (false && (++x > 0)) {  // ++x NOT executed
}
System.out.println(x);  // 5

// || short-circuit
if (true || (++x > 0)) {  // ++x NOT executed
}
System.out.println(x);  // 5

// No short-circuit with & and |
if (false & (++x > 0)) {  // ++x IS executed
}
System.out.println(x);  // 6
```

**Benefit**: Prevents errors and improves performance
```java
if (str != null && str.length() > 0) {  // Safe
    // If str is null, length() not called
}
```

### Q9: What is the modulus operator and when is it useful?
**Answer**:
The modulus operator `%` returns the remainder of division.

**Syntax**: `a % b` returns remainder when a is divided by b

**Examples**:
```java
System.out.println(10 % 3);   // 1
System.out.println(20 % 5);   // 0
System.out.println(7 % 2);    // 1
System.out.println(15 % 4);   // 3
```

**Use Cases**:
1. **Check even/odd**:
   ```java
   if (num % 2 == 0) {
       System.out.println("Even");
   }
   ```

2. **Circular arrays/rotation**:
   ```java
   int index = (currentIndex + 1) % arrayLength;
   ```

3. **Get last digit**:
   ```java
   int lastDigit = number % 10;
   ```

4. **Time calculations**:
   ```java
   int hours = minutes / 60;
   int remainingMinutes = minutes % 60;
   ```

### Q10: What happens when you divide by zero in Java?
**Answer**:

**Integer division by zero**:
- Throws `ArithmeticException` at runtime
```java
int result = 10 / 0;  // ArithmeticException: / by zero
```

**Floating-point division by zero**:
- Returns `Infinity` or `-Infinity` (no exception)
```java
double result = 10.0 / 0.0;  // Infinity
double result = -10.0 / 0.0; // -Infinity
double result = 0.0 / 0.0;   // NaN (Not a Number)
```

**Example**:
```java
try {
    int x = 10 / 0;  // Exception
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
}

double y = 10.0 / 0.0;
System.out.println(y);  // Infinity
System.out.println(Double.isInfinite(y));  // true
```

---

## Practice Exercises

1. Write a program to swap two numbers without using a third variable (using arithmetic operators)
2. Create a calculator that takes two numbers and performs all arithmetic operations
3. Check if a number is even or odd using the modulus operator
4. Find the largest of three numbers using ternary operator
5. Demonstrate the difference between pre and post increment in a loop

---

## Next Step
Move to **Step 4: Control Flow Statements** to learn how to control the flow of your program using conditions and loops.

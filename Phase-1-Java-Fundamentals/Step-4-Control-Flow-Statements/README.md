# Step 4: Control Flow Statements

## Overview
Control flow statements determine the order in which code executes. They allow you to make decisions, repeat code, and control program flow based on conditions.

## Key Concepts

### 1. Decision Making Statements
- **if statement**: Execute code if condition is true
- **if-else statement**: Choose between two blocks
- **if-else-if ladder**: Multiple conditions
- **switch statement**: Multiple cases based on value

### 2. Looping Statements
- **for loop**: Known number of iterations
- **while loop**: Condition-based iteration
- **do-while loop**: Execute at least once
- **enhanced for loop (for-each)**: Iterate over arrays/collections

### 3. Jump Statements
- **break**: Exit loop or switch
- **continue**: Skip current iteration
- **return**: Exit from method

---

## Code Examples

### Example 1: Decision Making (if-else, switch)
```java
public class DecisionMakingDemo {
    public static void main(String[] args) {
        // Simple if
        int age = 20;
        if (age >= 18) {
            System.out.println("You can vote!");
        }
        
        // if-else
        int marks = 75;
        if (marks >= 60) {
            System.out.println("Passed");
        } else {
            System.out.println("Failed");
        }
        
        // if-else-if ladder
        int score = 85;
        if (score >= 90) {
            System.out.println("Grade: A");
        } else if (score >= 80) {
            System.out.println("Grade: B");
        } else if (score >= 70) {
            System.out.println("Grade: C");
        } else if (score >= 60) {
            System.out.println("Grade: D");
        } else {
            System.out.println("Grade: F");
        }
        
        // Nested if
        boolean hasTicket = true;
        int passengerAge = 65;
        
        if (hasTicket) {
            if (passengerAge >= 60) {
                System.out.println("Senior citizen discount applied");
            } else {
                System.out.println("Regular ticket price");
            }
        } else {
            System.out.println("Please buy a ticket");
        }
        
        // Switch statement (Traditional)
        int day = 3;
        switch (day) {
            case 1:
                System.out.println("Monday");
                break;
            case 2:
                System.out.println("Tuesday");
                break;
            case 3:
                System.out.println("Wednesday");
                break;
            case 4:
                System.out.println("Thursday");
                break;
            case 5:
                System.out.println("Friday");
                break;
            case 6:
                System.out.println("Saturday");
                break;
            case 7:
                System.out.println("Sunday");
                break;
            default:
                System.out.println("Invalid day");
        }
        
        // Switch with String (Java 7+)
        String month = "January";
        switch (month) {
            case "January":
            case "March":
            case "May":
                System.out.println("31 days");
                break;
            case "April":
            case "June":
                System.out.println("30 days");
                break;
            case "February":
                System.out.println("28/29 days");
                break;
            default:
                System.out.println("Invalid month");
        }
    }
}
```

### Example 2: Loops (for, while, do-while)
```java
public class LoopsDemo {
    public static void main(String[] args) {
        // For loop - print 1 to 5
        System.out.println("For loop:");
        for (int i = 1; i <= 5; i++) {
            System.out.print(i + " ");
        }
        System.out.println();
        
        // While loop - print even numbers 2 to 10
        System.out.println("\nWhile loop (even numbers):");
        int num = 2;
        while (num <= 10) {
            System.out.print(num + " ");
            num += 2;
        }
        System.out.println();
        
        // Do-while loop - execute at least once
        System.out.println("\nDo-while loop:");
        int count = 1;
        do {
            System.out.print(count + " ");
            count++;
        } while (count <= 5);
        System.out.println();
        
        // Do-while executes at least once (even if condition false)
        int x = 10;
        do {
            System.out.println("Executed once: " + x);
        } while (x < 5);  // Condition is false, but still runs once
        
        // Enhanced for loop (for-each) with array
        System.out.println("\nEnhanced for loop:");
        int[] numbers = {10, 20, 30, 40, 50};
        for (int number : numbers) {
            System.out.print(number + " ");
        }
        System.out.println();
        
        // Nested loops - multiplication table
        System.out.println("\nMultiplication Table (3x3):");
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                System.out.print((i * j) + "\t");
            }
            System.out.println();
        }
        
        // Infinite loop (be careful!)
        // while (true) {
        //     System.out.println("Infinite loop");
        //     break;  // Need break to exit
        // }
    }
}
```

### Example 3: Jump Statements (break, continue, return)
```java
public class JumpStatementsDemo {
    public static void main(String[] args) {
        // Break - exit loop
        System.out.println("Break example:");
        for (int i = 1; i <= 10; i++) {
            if (i == 6) {
                break;  // Exit loop when i is 6
            }
            System.out.print(i + " ");
        }
        System.out.println("\n");
        
        // Continue - skip current iteration
        System.out.println("Continue example (skip even numbers):");
        for (int i = 1; i <= 10; i++) {
            if (i % 2 == 0) {
                continue;  // Skip even numbers
            }
            System.out.print(i + " ");
        }
        System.out.println("\n");
        
        // Break in nested loops (breaks only inner loop)
        System.out.println("Break in nested loops:");
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 5; j++) {
                if (j == 3) {
                    break;  // Breaks only inner loop
                }
                System.out.print("(" + i + "," + j + ") ");
            }
            System.out.println();
        }
        
        // Labeled break (break outer loop)
        System.out.println("\nLabeled break:");
        outer:
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    break outer;  // Break outer loop
                }
                System.out.print("(" + i + "," + j + ") ");
            }
            System.out.println();
        }
        System.out.println("\n");
        
        // Break in switch
        String grade = getGrade(85);
        System.out.println("Grade: " + grade);
        
        // Finding prime number
        int number = 17;
        boolean isPrime = checkPrime(number);
        System.out.println(number + " is prime? " + isPrime);
    }
    
    // Return statement in method
    static String getGrade(int marks) {
        if (marks >= 90) {
            return "A";  // Exit method
        } else if (marks >= 80) {
            return "B";
        } else if (marks >= 70) {
            return "C";
        } else {
            return "F";
        }
    }
    
    static boolean checkPrime(int num) {
        if (num <= 1) {
            return false;
        }
        for (int i = 2; i <= num/2; i++) {
            if (num % i == 0) {
                return false;  // Not prime, exit immediately
            }
        }
        return true;
    }
}
```

---

## Important Points to Remember

1. **if vs switch**:
   - Use `if` for range checks and complex conditions
   - Use `switch` for exact value matching (cleaner for many cases)

2. **for vs while**:
   - Use `for` when iterations are known
   - Use `while` when condition-based

3. **do-while**: Executes at least once (condition checked at end)

4. **break vs continue**:
   - `break`: Exits loop completely
   - `continue`: Skips to next iteration

5. **Enhanced for loop**: Cannot modify array elements or access index

6. **Fall-through in switch**: Without `break`, execution continues to next case

---

## Interview Questions (2025)

### Q1: What is the difference between if-else and switch statements?
**Answer**:

**if-else**:
- Can handle complex conditions and ranges
- Works with boolean expressions
- More flexible

```java
if (age >= 18 && age <= 60) {
    // Complex condition
}
```

**switch**:
- Matches exact values only
- Works with byte, short, int, char, String, enum
- Better readability for many cases
- Typically faster for many conditions

```java
switch (day) {
    case 1: // exact match
        break;
}
```

**When to use**:
- **if-else**: Range checks, complex conditions, boolean logic
- **switch**: Multiple exact value matches (menu selection, day of week)

**Java 12+ Switch Expressions**:
```java
String result = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};
```

### Q2: What is the difference between while and do-while loops?
**Answer**:

**while loop**:
- Condition checked BEFORE execution
- May not execute at all if condition is initially false
```java
int i = 10;
while (i < 5) {  // Condition false
    System.out.println(i);  // Never executes
}
```

**do-while loop**:
- Condition checked AFTER execution
- Executes at least once, even if condition is false
```java
int i = 10;
do {
    System.out.println(i);  // Executes once
} while (i < 5);  // Then condition checked
```

**Use cases**:
- **while**: Input validation, reading files
- **do-while**: Menu-driven programs (display menu at least once)

### Q3: What happens if you forget break in a switch statement?
**Answer**:
Without `break`, **fall-through** occurs - execution continues to the next case(s) until a break or end of switch.

```java
int day = 2;
switch (day) {
    case 1:
        System.out.println("Monday");
    case 2:
        System.out.println("Tuesday");  // Executes
    case 3:
        System.out.println("Wednesday"); // Also executes (fall-through)
        break;
    case 4:
        System.out.println("Thursday");
}
// Output:
// Tuesday
// Wednesday
```

**Intentional fall-through** (useful):
```java
switch (month) {
    case 1:
    case 3:
    case 5:
        System.out.println("31 days");
        break;
    case 4:
    case 6:
        System.out.println("30 days");
        break;
}
```

### Q4: Explain the difference between break and continue.
**Answer**:

**break**:
- Exits the loop/switch completely
- Control goes to statement after loop

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) break;  // Exit loop
    System.out.print(i + " ");  // 1 2
}
System.out.println("After loop");
```

**continue**:
- Skips current iteration only
- Control goes to next iteration

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;  // Skip 3
    System.out.print(i + " ");  // 1 2 4 5
}
System.out.println("After loop");
```

**In nested loops**:
- Both affect only the innermost loop (unless labeled)

```java
outer:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) break outer;  // Break outer loop
    }
}
```

### Q5: What is an enhanced for loop (for-each)? What are its limitations?
**Answer**:
Enhanced for loop (for-each) simplifies iteration over arrays and collections.

**Syntax**:
```java
for (dataType variable : array/collection) {
    // use variable
}
```

**Example**:
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

**Limitations**:
1. **Cannot modify array elements**:
   ```java
   for (int num : numbers) {
       num = num * 2;  // Doesn't modify array!
   }
   ```

2. **No access to index**:
   ```java
   // Cannot do: numbers[i]
   ```

3. **Cannot iterate backwards**

4. **Cannot iterate multiple arrays simultaneously**

5. **Only for complete iteration** (can't skip elements except with continue)

**When to use**:
- Reading/displaying array/collection elements
- No need for index or modification

### Q6: Can you use String in a switch statement?
**Answer**:
**Yes**, since Java 7, String can be used in switch statements.

```java
String day = "Monday";
switch (day) {
    case "Monday":
        System.out.println("Start of week");
        break;
    case "Friday":
        System.out.println("End of week");
        break;
    default:
        System.out.println("Mid week");
}
```

**Switch works with**:
- byte, short, int, char (since Java 1.0)
- Enum (since Java 5)
- String (since Java 7)
- **NOT** long, float, double, boolean

**String switch is case-sensitive**:
```java
String s = "hello";
switch (s) {
    case "HELLO":  // Won't match
        break;
    case "hello":  // Matches
        break;
}
```

**Null handling**:
```java
String s = null;
switch (s) {  // NullPointerException!
    case "hello":
        break;
}
```

### Q7: What is the difference between for and enhanced for loop?
**Answer**:

**Traditional for loop**:
- Has index variable
- Can modify array elements
- Can iterate in any order
- More control

```java
int[] arr = {1, 2, 3, 4, 5};
for (int i = 0; i < arr.length; i++) {
    arr[i] = arr[i] * 2;  // Modify
    System.out.println("Index " + i + ": " + arr[i]);
}
```

**Enhanced for loop**:
- No index variable
- Cannot modify array elements
- Forward iteration only
- Simpler syntax

```java
for (int num : arr) {
    System.out.println(num);  // Read only
}
```

**Comparison**:
| Feature | for | for-each |
|---------|-----|----------|
| Syntax | Complex | Simple |
| Index access | Yes | No |
| Modify elements | Yes | No |
| Partial iteration | Yes | No |
| Reverse iteration | Yes | No |
| Multiple arrays | Yes | No |

### Q8: What will happen if the condition in a while loop is always true?
**Answer**:
It creates an **infinite loop** - the loop never terminates and runs forever (until program is forcefully stopped or system crashes).

```java
while (true) {  // Infinite loop
    System.out.println("This will print forever");
}
```

**Common causes**:
```java
int i = 1;
while (i <= 10) {
    System.out.println(i);
    // Forgot to increment i - infinite loop!
}
```

**Intentional infinite loops** (with exit condition):
```java
while (true) {
    System.out.println("Enter command (exit to quit):");
    String input = scanner.nextLine();
    if (input.equals("exit")) {
        break;  // Exit loop
    }
    // Process command
}
```

**In production**: Always ensure loop has proper termination condition or use break.

### Q9: Can we use multiple variables in a for loop?
**Answer**:
**Yes**, Java allows multiple variables in for loop initialization and update.

```java
// Multiple variables of same type
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println("i=" + i + ", j=" + j);
}
// Output:
// i=0, j=10
// i=1, j=9
// i=2, j=8
// ...
```

**Rules**:
- Variables must be of same type in initialization
- Comma-separated in initialization and update
- Only one condition

```java
// Valid
for (int i = 0, j = 0; i < 5; i++, j+=2) {
    System.out.println(i + " " + j);
}

// Invalid - different types
// for (int i = 0, double d = 0.0; ...) { }
```

### Q10: What is labeled break and continue?
**Answer**:
Labels allow you to break/continue outer loops from nested loops.

**Labeled break**:
```java
outer:  // Label
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (i == 2 && j == 2) {
            break outer;  // Break outer loop
        }
        System.out.print("(" + i + "," + j + ") ");
    }
}
// Output: (1,1) (1,2) (1,3) (2,1)
```

**Labeled continue**:
```java
outer:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            continue outer;  // Continue outer loop
        }
        System.out.print("(" + i + "," + j + ") ");
    }
}
// Output: (1,1) (2,1) (3,1)
```

**Without label**:
- break/continue affects only the innermost loop

**Use case**:
- Matrix search
- Breaking multiple nested loops
- Complex loop control

---

## Practice Exercises

1. Write a program to print Fibonacci series up to n terms
2. Check if a number is prime using loops
3. Create a menu-driven calculator using switch statement
4. Print the following pattern:
   ```
   *
   **
   ***
   ****
   *****
   ```
5. Find the sum of all even numbers between 1 and 100
6. Write a program to reverse a number using while loop

---

## Next Step
Move to **Step 5: Arrays** to learn how to store and manipulate collections of data.

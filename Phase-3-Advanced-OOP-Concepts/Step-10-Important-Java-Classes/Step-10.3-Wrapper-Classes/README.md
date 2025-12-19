# Step 10.3: Wrapper Classes

## What are Wrapper Classes?

**Wrapper classes** convert Java primitives into objects. They "wrap" primitive data types into objects so they can be used where objects are required (like collections).

### Why do we need Wrapper Classes?

1. **Collections**: Collections (ArrayList, HashMap, etc.) only work with objects, not primitives
2. **Null values**: Primitives cannot be null, but wrapper objects can be
3. **Utility methods**: Wrapper classes provide useful methods for type conversion
4. **Generics**: Generic types require objects, not primitives
5. **Synchronization**: Some threading operations require objects

---

## Primitive Types and Their Wrapper Classes

| Primitive Type | Wrapper Class | Example |
|---------------|---------------|---------|
| `byte` | `Byte` | `Byte b = 10;` |
| `short` | `Short` | `Short s = 100;` |
| `int` | `Integer` | `Integer i = 500;` |
| `long` | `Long` | `Long l = 1000L;` |
| `float` | `Float` | `Float f = 3.14f;` |
| `double` | `Double` | `Double d = 99.99;` |
| `char` | `Character` | `Character c = 'A';` |
| `boolean` | `Boolean` | `Boolean flag = true;` |

---

## Autoboxing and Unboxing

### Autoboxing
**Automatic conversion** of primitive to wrapper object.

```java
int primitive = 10;
Integer wrapper = primitive;  // Autoboxing (automatic)
```

### Unboxing
**Automatic conversion** of wrapper object to primitive.

```java
Integer wrapper = 100;
int primitive = wrapper;  // Unboxing (automatic)
```

---

## Example 1: Basic Wrapper Class Usage

```java
public class WrapperBasics {
    public static void main(String[] args) {
        // Creating wrapper objects - different ways
        
        // 1. Using constructor (deprecated in Java 9+)
        Integer num1 = new Integer(10);
        Double num2 = new Double(3.14);
        
        // 2. Using valueOf() method (preferred)
        Integer num3 = Integer.valueOf(20);
        Double num4 = Double.valueOf(2.71);
        Character ch1 = Character.valueOf('A');
        Boolean flag1 = Boolean.valueOf(true);
        
        // 3. Autoboxing (automatic conversion)
        Integer num5 = 30;  // primitive int to Integer object
        Double num6 = 1.618;
        Character ch2 = 'B';
        Boolean flag2 = false;
        
        System.out.println("=== Wrapper Objects ===");
        System.out.println("Integer: " + num3);
        System.out.println("Double: " + num4);
        System.out.println("Character: " + ch1);
        System.out.println("Boolean: " + flag1);
        
        // Unboxing (automatic conversion to primitive)
        int primitiveInt = num3;  // Integer to int
        double primitiveDouble = num4;  // Double to double
        char primitiveChar = ch1;  // Character to char
        boolean primitiveBoolean = flag1;  // Boolean to boolean
        
        System.out.println("\n=== Primitives (after unboxing) ===");
        System.out.println("int: " + primitiveInt);
        System.out.println("double: " + primitiveDouble);
        System.out.println("char: " + primitiveChar);
        System.out.println("boolean: " + primitiveBoolean);
        
        // Wrapper objects can be null
        Integer nullableInt = null;
        System.out.println("\n=== Null values ===");
        System.out.println("Nullable Integer: " + nullableInt);
        
        // int primitiveFromNull = nullableInt;  // NullPointerException!
    }
}
```

**Output:**
```
=== Wrapper Objects ===
Integer: 20
Double: 2.71
Character: A
Boolean: true

=== Primitives (after unboxing) ===
int: 20
double: 2.71
char: A
boolean: true

=== Null values ===
Nullable Integer: null
```

---

## Example 2: Wrapper Class Utility Methods

```java
public class WrapperUtilityMethods {
    public static void main(String[] args) {
        System.out.println("=== Integer Wrapper Methods ===");
        
        // String to int conversion
        String numberStr = "12345";
        int num1 = Integer.parseInt(numberStr);
        System.out.println("parseInt(\"12345\"): " + num1);
        
        // String to Integer object
        Integer num2 = Integer.valueOf(numberStr);
        System.out.println("valueOf(\"12345\"): " + num2);
        
        // int to String conversion
        int number = 789;
        String str1 = Integer.toString(number);
        System.out.println("toString(789): " + str1);
        
        // Binary, Octal, Hex conversion
        System.out.println("toBinaryString(15): " + Integer.toBinaryString(15));
        System.out.println("toOctalString(15): " + Integer.toOctalString(15));
        System.out.println("toHexString(15): " + Integer.toHexString(15));
        
        // Parse binary, octal, hex strings
        System.out.println("parseInt(\"1111\", 2): " + Integer.parseInt("1111", 2));  // Binary
        System.out.println("parseInt(\"17\", 8): " + Integer.parseInt("17", 8));      // Octal
        System.out.println("parseInt(\"F\", 16): " + Integer.parseInt("F", 16));      // Hex
        
        // Compare values
        System.out.println("compare(10, 20): " + Integer.compare(10, 20));  // -1 (first < second)
        System.out.println("compare(20, 10): " + Integer.compare(20, 10));  // 1 (first > second)
        System.out.println("compare(10, 10): " + Integer.compare(10, 10));  // 0 (equal)
        
        // Max and Min values
        System.out.println("Integer.MAX_VALUE: " + Integer.MAX_VALUE);
        System.out.println("Integer.MIN_VALUE: " + Integer.MIN_VALUE);
        
        System.out.println("\n=== Double Wrapper Methods ===");
        
        // String to double
        double d1 = Double.parseDouble("3.14159");
        System.out.println("parseDouble(\"3.14159\"): " + d1);
        
        // Check for special values
        double zero = 0.0;
        double positiveInfinity = 1.0 / zero;
        double negativeInfinity = -1.0 / zero;
        double notANumber = zero / zero;
        
        System.out.println("isInfinite(1.0/0): " + Double.isInfinite(positiveInfinity));
        System.out.println("isNaN(0.0/0): " + Double.isNaN(notANumber));
        System.out.println("isFinite(3.14): " + Double.isFinite(3.14));
        
        // Double constants
        System.out.println("Double.MAX_VALUE: " + Double.MAX_VALUE);
        System.out.println("Double.MIN_VALUE: " + Double.MIN_VALUE);
        System.out.println("Double.POSITIVE_INFINITY: " + Double.POSITIVE_INFINITY);
        System.out.println("Double.NEGATIVE_INFINITY: " + Double.NEGATIVE_INFINITY);
        System.out.println("Double.NaN: " + Double.NaN);
        
        System.out.println("\n=== Character Wrapper Methods ===");
        
        char ch = 'A';
        System.out.println("isDigit('A'): " + Character.isDigit(ch));
        System.out.println("isLetter('A'): " + Character.isLetter(ch));
        System.out.println("isUpperCase('A'): " + Character.isUpperCase(ch));
        System.out.println("isLowerCase('A'): " + Character.isLowerCase(ch));
        System.out.println("isWhitespace(' '): " + Character.isWhitespace(' '));
        System.out.println("toLowerCase('A'): " + Character.toLowerCase(ch));
        System.out.println("toUpperCase('a'): " + Character.toUpperCase('a'));
        
        System.out.println("\n=== Boolean Wrapper Methods ===");
        
        Boolean b1 = Boolean.valueOf("true");
        Boolean b2 = Boolean.valueOf("TrUe");  // Case insensitive
        Boolean b3 = Boolean.valueOf("yes");   // Returns false (not "true")
        
        System.out.println("valueOf(\"true\"): " + b1);
        System.out.println("valueOf(\"TrUe\"): " + b2);
        System.out.println("valueOf(\"yes\"): " + b3);
        
        boolean parsed = Boolean.parseBoolean("true");
        System.out.println("parseBoolean(\"true\"): " + parsed);
    }
}
```

**Output:**
```
=== Integer Wrapper Methods ===
parseInt("12345"): 12345
valueOf("12345"): 12345
toString(789): 789
toBinaryString(15): 1111
toOctalString(15): 17
toHexString(15): f
parseInt("1111", 2): 15
parseInt("17", 8): 15
parseInt("F", 16): 15
compare(10, 20): -1
compare(20, 10): 1
compare(10, 10): 0
Integer.MAX_VALUE: 2147483647
Integer.MIN_VALUE: -2147483648

=== Double Wrapper Methods ===
parseDouble("3.14159"): 3.14159
isInfinite(1.0/0): true
isNaN(0.0/0): true
isFinite(3.14): true
Double.MAX_VALUE: 1.7976931348623157E308
Double.MIN_VALUE: 4.9E-324
Double.POSITIVE_INFINITY: Infinity
Double.NEGATIVE_INFINITY: -Infinity
Double.NaN: NaN

=== Character Wrapper Methods ===
isDigit('A'): false
isLetter('A'): true
isUpperCase('A'): true
isLowerCase('A'): false
isWhitespace(' '): true
toLowerCase('A'): a
toUpperCase('a'): A

=== Boolean Wrapper Methods ===
valueOf("true"): true
valueOf("TrUe"): true
valueOf("yes"): false
parseBoolean("true"): true
```

---

## Example 3: Wrapper Classes with Collections

```java
import java.util.ArrayList;
import java.util.HashMap;

public class WrapperWithCollections {
    public static void main(String[] args) {
        // ArrayList with Integer (not int)
        ArrayList<Integer> numbers = new ArrayList<>();
        
        // Autoboxing when adding
        numbers.add(10);   // int 10 → Integer 10
        numbers.add(20);
        numbers.add(30);
        numbers.add(40);
        numbers.add(50);
        
        System.out.println("=== ArrayList of Integers ===");
        System.out.println("Numbers: " + numbers);
        
        // Unboxing when retrieving
        int firstNumber = numbers.get(0);  // Integer → int
        System.out.println("First number: " + firstNumber);
        
        // Operations with autoboxing/unboxing
        int sum = 0;
        for (Integer num : numbers) {
            sum += num;  // Unboxing: Integer → int
        }
        System.out.println("Sum: " + sum);
        
        // HashMap with wrapper classes
        HashMap<String, Integer> scores = new HashMap<>();
        scores.put("Alice", 95);    // Autoboxing
        scores.put("Bob", 87);
        scores.put("Charlie", 92);
        scores.put("Diana", 88);
        
        System.out.println("\n=== HashMap with Integer values ===");
        System.out.println("Scores: " + scores);
        
        // Getting value (with unboxing)
        int aliceScore = scores.get("Alice");  // Integer → int
        System.out.println("Alice's score: " + aliceScore);
        
        // Null handling with wrapper classes
        ArrayList<Integer> listWithNull = new ArrayList<>();
        listWithNull.add(10);
        listWithNull.add(null);  // Wrapper objects can be null
        listWithNull.add(30);
        
        System.out.println("\n=== ArrayList with null ===");
        System.out.println("List: " + listWithNull);
        
        // Safe null handling
        for (Integer num : listWithNull) {
            if (num != null) {
                System.out.println("Number: " + num);
            } else {
                System.out.println("Found null value");
            }
        }
    }
}
```

**Output:**
```
=== ArrayList of Integers ===
Numbers: [10, 20, 30, 40, 50]
First number: 10
Sum: 150

=== HashMap with Integer values ===
Scores: {Alice=95, Bob=87, Charlie=92, Diana=88}
Alice's score: 95

=== ArrayList with null ===
List: [10, null, 30]
Number: 10
Found null value
Number: 30
```

---

## Important Concepts

### 1. Caching (Integer Cache)

Java caches Integer objects in the range -128 to 127 for performance.

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);  // true (same object from cache)

Integer c = 200;
Integer d = 200;
System.out.println(c == d);  // false (different objects)

// Always use equals() for value comparison
System.out.println(c.equals(d));  // true (correct way)
```

### 2. Immutability

All wrapper classes are **immutable** (like String). Once created, their values cannot be changed.

```java
Integer num = 10;
num = num + 5;  // Creates new Integer object with value 15
```

### 3. Performance Considerations

- Autoboxing/unboxing has overhead
- Avoid in performance-critical code (loops with many iterations)
- Use primitives when objects are not required

```java
// Less efficient (autoboxing in loop)
Integer sum1 = 0;
for (int i = 0; i < 1000000; i++) {
    sum1 += i;  // Unboxing + boxing in each iteration
}

// More efficient (primitive)
int sum2 = 0;
for (int i = 0; i < 1000000; i++) {
    sum2 += i;  // No boxing/unboxing
}
```

---

## 2025 Interview Questions

### Basic Level

**Q1: What are wrapper classes in Java?**
**A:** Wrapper classes convert primitive data types into objects. Each primitive type has a corresponding wrapper class (int → Integer, char → Character, etc.). They allow primitives to be used where objects are required.

**Q2: Why do we need wrapper classes?**
**A:** We need wrapper classes because:
1. Collections only work with objects
2. Generics require objects
3. Wrapper classes provide utility methods
4. Some APIs require objects, not primitives
5. Objects can be null, primitives cannot

**Q3: What is autoboxing and unboxing?**
**A:**
- **Autoboxing**: Automatic conversion of primitive to wrapper object
  ```java
  int primitive = 10;
  Integer wrapper = primitive;  // Autoboxing
  ```
- **Unboxing**: Automatic conversion of wrapper object to primitive
  ```java
  Integer wrapper = 20;
  int primitive = wrapper;  // Unboxing
  ```

**Q4: List all primitive types and their wrapper classes.**
**A:**
- byte → Byte
- short → Short
- int → Integer
- long → Long
- float → Float
- double → Double
- char → Character
- boolean → Boolean

**Q5: Can wrapper class objects be null?**
**A:** Yes, wrapper class objects can be null, unlike primitives which always have a default value.

```java
Integer num = null;  // Valid
int primitive = null;  // Compilation error
```

### Intermediate Level

**Q6: What is Integer caching in Java?**
**A:** Java caches Integer objects in the range -128 to 127 for memory efficiency. When you create Integer objects in this range using autoboxing or valueOf(), the same object is reused.

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);  // true (same cached object)

Integer c = 200;
Integer d = 200;
System.out.println(c == d);  // false (different objects)
```

**Q7: Why should we use equals() instead of == for wrapper classes?**
**A:** 
- `==` compares object references (memory addresses)
- `equals()` compares actual values
- Due to caching, `==` may give unexpected results

```java
Integer a = 150;
Integer b = 150;
System.out.println(a == b);        // false (different objects)
System.out.println(a.equals(b));   // true (same value)
```

**Q8: Are wrapper classes mutable or immutable?**
**A:** All wrapper classes are immutable. Once created, their value cannot be changed. Any operation that appears to modify the value actually creates a new object.

**Q9: What is the difference between Integer.parseInt() and Integer.valueOf()?**
**A:**
- `parseInt(String s)`: Returns primitive `int`
- `valueOf(String s)`: Returns `Integer` object

```java
int primitive = Integer.parseInt("123");      // Returns int
Integer wrapper = Integer.valueOf("123");     // Returns Integer
```

**Q10: What happens if you unbox a null wrapper object?**
**A:** It throws `NullPointerException`.

```java
Integer num = null;
int value = num;  // NullPointerException at runtime!
```

### Advanced Level

**Q11: What is the performance impact of autoboxing/unboxing?**
**A:** Autoboxing/unboxing has performance overhead because:
1. Object creation takes time and memory
2. Each boxing creates a new object (unless cached)
3. In loops, this can be significant

Use primitives in performance-critical code.

**Q12: Which wrapper classes have caching, and what is the range?**
**A:**
- **Integer, Short, Byte, Long**: -128 to 127
- **Character**: 0 to 127
- **Boolean**: true and false are cached
- **Float, Double**: No caching

**Q13: Can you override methods in wrapper classes?**
**A:** No, all wrapper classes are **final** classes. They cannot be extended, so their methods cannot be overridden.

**Q14: What is the difference between new Integer(10) and Integer.valueOf(10)?**
**A:**
- `new Integer(10)`: Always creates a new object (deprecated in Java 9+)
- `Integer.valueOf(10)`: May return cached object for -128 to 127 range (preferred)

```java
Integer a = new Integer(10);      // Always new object
Integer b = Integer.valueOf(10);  // May use cache
```

**Q15: How do you convert between different wrapper types?**
**A:** Use the corresponding parseXxx() or valueOf() methods.

```java
Integer intObj = 100;
Double doubleObj = Double.valueOf(intObj.doubleValue());
String strObj = intObj.toString();
Long longObj = Long.valueOf(intObj.longValue());
```

**Q16: What is the use of xxxValue() methods in wrapper classes?**
**A:** The xxxValue() methods convert a wrapper object to primitive types.

```java
Integer num = 100;
int intValue = num.intValue();
double doubleValue = num.doubleValue();
long longValue = num.longValue();
```

**Q17: Can you use wrapper classes in switch statements?**
**A:** Yes, from Java 5+, wrapper classes can be used in switch statements due to auto-unboxing.

```java
Integer num = 2;
switch(num) {  // Auto-unboxed to int
    case 1: System.out.println("One"); break;
    case 2: System.out.println("Two"); break;
    default: System.out.println("Other");
}
```

**Q18: What is the size difference between primitives and wrapper objects?**
**A:** Wrapper objects consume more memory:
- `int`: 4 bytes
- `Integer` object: ~16 bytes (object header + value + alignment)

For large datasets, use primitives for better memory efficiency.

**Q19: How does Java handle arithmetic operations with wrapper classes?**
**A:** Java auto-unboxes wrapper objects before performing arithmetic operations, then auto-boxes the result if needed.

```java
Integer a = 10;
Integer b = 20;
Integer c = a + b;  // Unboxed to int, added, then boxed to Integer
```

**Q20: What are the common pitfalls when using wrapper classes?**
**A:**
1. **NullPointerException** with auto-unboxing of null
2. **Using == instead of equals()** for comparison
3. **Performance issues** in loops with autoboxing/unboxing
4. **Assuming immutability behavior** incorrectly
5. **Memory overhead** for large collections

---

## Key Takeaways

✅ Wrapper classes convert primitives to objects
✅ Used with collections, generics, and APIs requiring objects
✅ Autoboxing and unboxing happen automatically
✅ All wrapper classes are immutable and final
✅ Integer caching: -128 to 127
✅ Use equals() for value comparison, not ==
✅ Can be null (unlike primitives)
✅ Performance overhead in tight loops
✅ Provide utility methods for conversions

---

## Practice Exercises

1. Write a program that demonstrates the difference between == and equals() with wrapper classes.

2. Create a program showing autoboxing/unboxing with all primitive types.

3. Build a calculator that uses wrapper classes and demonstrates their utility methods.

4. Write code to demonstrate Integer caching behavior.

5. Create a collection-based program that handles null wrapper values safely.

---

**Next Step:** [Phase 4: Step 11 - Collections Basics](../../../Phase-4-Collections-Framework/Step-11-Collections-Basics/README.md)

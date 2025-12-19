# Step 10.2: String Class

## Overview
String is one of the most commonly used classes in Java. Strings are immutable - once created, their value cannot be changed. Understanding String manipulation is essential for Java programming.

## Key Concepts

### 1. String Immutability
- String objects cannot be modified
- Any modification creates a new String object
- Stored in String Pool (for literals)

### 2. String Creation
```java
// String literal (stored in String Pool)
String s1 = "Hello";

// Using new keyword (stored in Heap)
String s2 = new String("Hello");
```

### 3. Important String Methods
- `length()`, `charAt()`, `substring()`
- `concat()`, `replace()`, `trim()`
- `toUpperCase()`, `toLowerCase()`
- `equals()`, `equalsIgnoreCase()`, `compareTo()`
- `indexOf()`, `lastIndexOf()`, `contains()`
- `split()`, `join()`, `valueOf()`

---

## Code Examples

### Example 1: String Creation and Immutability
```java
public class StringImmutabilityDemo {
    public static void main(String[] args) {
        // String literal - stored in String Pool
        String s1 = "Hello";
        String s2 = "Hello";
        String s3 = "World";
        
        // new keyword - stored in Heap
        String s4 = new String("Hello");
        
        // Reference comparison
        System.out.println("s1 == s2: " + (s1 == s2));  // true (same object in pool)
        System.out.println("s1 == s4: " + (s1 == s4));  // false (different objects)
        
        // Content comparison
        System.out.println("s1.equals(s4): " + s1.equals(s4));  // true
        
        // Immutability demonstration
        String original = "Java";
        String modified = original.concat(" Programming");
        
        System.out.println("\nOriginal: " + original);  // Java (unchanged)
        System.out.println("Modified: " + modified);    // Java Programming
        
        // String Pool demonstration
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");
        String str4 = str3.intern();  // Add to pool
        
        System.out.println("\nString Pool:");
        System.out.println("str1 == str2: " + (str1 == str2));  // true
        System.out.println("str1 == str3: " + (str1 == str3));  // false
        System.out.println("str1 == str4: " + (str1 == str4));  // true
    }
}
```

### Example 2: Common String Methods
```java
public class StringMethodsDemo {
    public static void main(String[] args) {
        String text = "  Java Programming  ";
        
        // Length and character access
        System.out.println("Length: " + text.length());
        System.out.println("charAt(2): " + text.charAt(2));
        
        // Trimming whitespace
        String trimmed = text.trim();
        System.out.println("Trimmed: '" + trimmed + "'");
        
        // Case conversion
        System.out.println("Uppercase: " + trimmed.toUpperCase());
        System.out.println("Lowercase: " + trimmed.toLowerCase());
        
        // Substring
        String sub1 = trimmed.substring(5);     // From index 5 to end
        String sub2 = trimmed.substring(5, 11); // From 5 to 11 (exclusive)
        System.out.println("Substring(5): " + sub1);
        System.out.println("Substring(5,11): " + sub2);
        
        // Replace
        String replaced = trimmed.replace("Java", "Python");
        System.out.println("Replaced: " + replaced);
        
        // Contains, startsWith, endsWith
        System.out.println("Contains 'Java': " + trimmed.contains("Java"));
        System.out.println("Starts with 'Java': " + trimmed.startsWith("Java"));
        System.out.println("Ends with 'ing': " + trimmed.endsWith("ing"));
        
        // indexOf, lastIndexOf
        String sample = "Java is awesome, Java is popular";
        System.out.println("indexOf 'Java': " + sample.indexOf("Java"));
        System.out.println("lastIndexOf 'Java': " + sample.lastIndexOf("Java"));
        System.out.println("indexOf 'Python': " + sample.indexOf("Python"));  // -1
        
        // Split
        String csv = "Apple,Banana,Orange,Mango";
        String[] fruits = csv.split(",");
        System.out.println("\nFruits:");
        for (String fruit : fruits) {
            System.out.println("- " + fruit);
        }
        
        // Join
        String joined = String.join(" | ", fruits);
        System.out.println("Joined: " + joined);
        
        // Comparison
        String s1 = "Apple";
        String s2 = "Banana";
        System.out.println("\nCompareTo:");
        System.out.println("Apple compareTo Banana: " + s1.compareTo(s2));  // Negative
        System.out.println("Banana compareTo Apple: " + s2.compareTo(s1));  // Positive
    }
}
```

### Example 3: StringBuilder and StringBuffer
```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        // Problem with String concatenation in loop
        long start = System.currentTimeMillis();
        String str = "";
        for (int i = 0; i < 10000; i++) {
            str += "a";  // Creates new object each time (inefficient)
        }
        long end = System.currentTimeMillis();
        System.out.println("String concat time: " + (end - start) + "ms");
        
        // StringBuilder - mutable, not thread-safe, faster
        start = System.currentTimeMillis();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 10000; i++) {
            sb.append("a");  // Modifies same object
        }
        end = System.currentTimeMillis();
        System.out.println("StringBuilder time: " + (end - start) + "ms");
        
        // StringBuilder methods
        StringBuilder builder = new StringBuilder("Hello");
        builder.append(" World");
        builder.insert(5, ",");
        builder.delete(11, 16);
        builder.reverse();
        
        System.out.println("\nStringBuilder operations:");
        System.out.println(builder);
        
        // Converting to String
        String result = builder.toString();
        
        // StringBuffer - mutable, thread-safe, slower than StringBuilder
        StringBuffer buffer = new StringBuffer("Thread");
        buffer.append(" Safe");
        System.out.println("StringBuffer: " + buffer);
    }
}
```

---

## Interview Questions (2025)

### Q1: Why are Strings immutable in Java?
**Answer**:

**Reasons**:

1. **Security**: Strings are used for sensitive data (passwords, file paths, network connections). Immutability prevents modification after creation.

2. **String Pool**: Allows multiple references to share same object, saving memory.

3. **Thread Safety**: No synchronization needed (multiple threads can safely access)

4. **Caching**: hashCode() is cached (important for HashMap keys)

5. **Class Loading**: Class names are Strings. Immutability prevents runtime modification.

**Example**:
```java
String password = "secret123";
// If String were mutable, could be changed without our knowledge
// Immutability prevents this security risk
```

### Q2: What is String Pool?
**Answer**:
**String Pool** (String Intern Pool) is a special memory area in the heap where Java stores string literals. When you create a string literal, JVM checks if it exists in the pool. If yes, returns reference to existing object; if no, creates new object.

```java
String s1 = "Hello";  // Creates object in pool
String s2 = "Hello";  // Reuses same object from pool
System.out.println(s1 == s2);  // true (same reference)

String s3 = new String("Hello");  // Creates object in heap (not pool)
System.out.println(s1 == s3);  // false (different objects)

String s4 = s3.intern();  // Add to pool or return existing
System.out.println(s1 == s4);  // true (now same reference)
```

**Benefits**: Memory efficiency

### Q3: What is the difference between String, StringBuilder, and StringBuffer?
**Answer**:

| Feature | String | StringBuilder | StringBuffer |
|---------|--------|---------------|--------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread Safety | Yes (immutable) | No | Yes (synchronized) |
| Performance | Slow (for concatenation) | Fast | Slower than StringBuilder |
| Memory | More (creates new objects) | Less | Less |
| When to Use | Fixed strings | Single-threaded string building | Multi-threaded string building |

```java
// String - immutable
String s = "Hello";
s = s + " World";  // Creates new object

// StringBuilder - mutable, fast
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // Modifies same object

// StringBuffer - mutable, thread-safe
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World");  // Thread-safe
```

---

## Practice Exercises

1. Write a program to reverse a string without using built-in methods
2. Check if a string is a palindrome
3. Count the number of vowels and consonants in a string
4. Compare performance of String vs StringBuilder for concatenation

---

## Next Step
Continue to **Step 10.3: Wrapper Classes** to learn about primitive wrappers and autoboxing.

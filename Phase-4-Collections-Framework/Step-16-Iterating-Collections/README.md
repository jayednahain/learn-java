# Step 16: Iterating Collections

Multiple ways to iterate through collections in Java.

## Methods:

### 1. For Loop (index-based)
```java
List<String> list = Arrays.asList("A", "B", "C");
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```

### 2. Enhanced For Loop (for-each)
```java
for (String item : list) {
    System.out.println(item);
}
```

### 3. Iterator
```java
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

### 4. ListIterator (bidirectional)
```java
ListIterator<String> lit = list.listIterator();
while (lit.hasNext()) {
    System.out.println(lit.next());
}
```

### 5. forEach with Lambda (Java 8+)
```java
list.forEach(item -> System.out.println(item));
// Or method reference
list.forEach(System.out::println);
```

### 6. Stream API (Java 8+)
```java
list.stream().forEach(System.out::println);
```

## Comparison:

| Method | When to Use |
|--------|-------------|
| For loop | Need index, List only |
| For-each | Simple iteration, all collections |
| Iterator | Need to remove elements while iterating |
| ListIterator | Need bidirectional iteration, List only |
| forEach | Functional style, Java 8+ |
| Stream | Complex operations, transformations |

## Example - Complete:

```java
import java.util.*;

public class IterationExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        
        // forEach with lambda
        System.out.println("=== forEach ===");
        numbers.forEach(n -> System.out.print(n + " "));
        
        // Stream with operations
        System.out.println("\n\n=== Stream ===");
        numbers.stream()
               .filter(n -> n % 2 == 0)
               .map(n -> n * n)
               .forEach(n -> System.out.print(n + " "));
    }
}
```

**Next:** [Phase 5: Exception Handling](../../Phase-5-Exception-Handling/Step-17-Exceptions/README.md)

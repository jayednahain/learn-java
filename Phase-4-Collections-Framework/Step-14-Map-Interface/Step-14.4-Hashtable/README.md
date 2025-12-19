# Step 14.4: Hashtable

**Hashtable** is legacy synchronized map. Use ConcurrentHashMap instead.

```java
import java.util.Hashtable;

public class HashtableExample {
    public static void main(String[] args) {
        Hashtable<String, Integer> table = new Hashtable<>();
        table.put("One", 1);
        table.put("Two", 2);
        
        System.out.println(table);
        // No null keys or values allowed!
    }
}
```

**Note:** Prefer `ConcurrentHashMap` for thread-safe operations.

# Step 13.1: HashSet

**HashSet** uses hash table for storage. Fast operations, no ordering.

```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple");  // Duplicate - ignored
        
        System.out.println(set);  // [Apple, Banana] or [Banana, Apple]
        System.out.println("Contains Apple: " + set.contains("Apple"));
        System.out.println("Size: " + set.size());
    }
}
```

**Time Complexity:** O(1) for add, remove, contains

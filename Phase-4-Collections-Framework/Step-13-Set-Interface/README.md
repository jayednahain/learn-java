# Step 13: Set Interface

The **Set** interface represents a collection that contains NO duplicate elements.

## Key Features:
- No duplicates allowed
- At most one null element
- Models mathematical set abstraction

## Implementations:

### [13.1 HashSet](Step-13.1-HashSet/README.md)
- Hash table based
- No ordering guaranteed
- Best performance: O(1) for add, remove, contains
- **Use when**: Need fast operations, order doesn't matter

### [13.2 LinkedHashSet](Step-13.2-LinkedHashSet/README.md)
- Hash table + linked list
- Maintains insertion order
- Slightly slower than HashSet
- **Use when**: Need set with insertion order

### [13.3 TreeSet](Step-13.3-TreeSet/README.md)
- Red-Black tree (sorted)
- Elements in natural/custom order
- O(log n) for operations
- **Use when**: Need sorted set

## Quick Comparison:

| Feature | HashSet | LinkedHashSet | TreeSet |
|---------|---------|---------------|---------|
| Order | No order | Insertion order | Sorted order |
| Performance | O(1) | O(1) | O(log n) |
| Null elements | One null | One null | No null (Java 7+) |
| Use case | Fast, unordered | Fast + ordered | Sorted |

## Quick Example:

```java
import java.util.*;

public class SetExample {
    public static void main(String[] args) {
        // HashSet - no order
        Set<String> hashSet = new HashSet<>();
        hashSet.add("C");
        hashSet.add("A");
        hashSet.add("B");
        hashSet.add("A");  // Duplicate ignored
        System.out.println("HashSet: " + hashSet);  // Random order
        
        // LinkedHashSet - insertion order
        Set<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("C");
        linkedHashSet.add("A");
        linkedHashSet.add("B");
        System.out.println("LinkedHashSet: " + linkedHashSet);  // C, A, B
        
        // TreeSet - sorted
        Set<String> treeSet = new TreeSet<>();
        treeSet.add("C");
        treeSet.add("A");
        treeSet.add("B");
        System.out.println("TreeSet: " + treeSet);  // A, B, C
    }
}
```

**Next:** Explore each Set implementation in detail!

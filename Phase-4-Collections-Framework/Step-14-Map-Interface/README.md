# Step 14: Map Interface

The **Map** interface represents key-value pairs. It's NOT part of Collection interface but is part of Collections Framework.

## Key Features:
- Stores key-value pairs
- No duplicate keys (values can be duplicate)
- Each key maps to at most one value

## Implementations:

### [14.1 HashMap](Step-14.1-HashMap/README.md)
- Hash table based
- No ordering
- Best performance: O(1) average
- Allows one null key, multiple null values
- **Use when**: Fast lookups, order doesn't matter

### [14.2 LinkedHashMap](Step-14.2-LinkedHashMap/README.md)
- Hash table + linked list
- Maintains insertion order
- **Use when**: Need map with insertion order

### [14.3 TreeMap](Step-14.3-TreeMap/README.md)
- Red-Black tree
- Sorted by keys
- O(log n) operations
- **Use when**: Need sorted map

### [14.4 Hashtable](Step-14.4-Hashtable/README.md)
- Legacy, synchronized
- No null keys/values
- **Use when**: Thread safety (prefer ConcurrentHashMap)

## Quick Comparison:

| Feature | HashMap | LinkedHashMap | TreeMap | Hashtable |
|---------|---------|---------------|---------|-----------|
| Order | No order | Insertion order | Sorted | No order |
| Performance | O(1) | O(1) | O(log n) | O(1) |
| Null key/value | 1 null key/multiple null values | Yes | No null keys | No nulls |
| Thread-safe | No | No | No | Yes |

## Quick Example:

```java
import java.util.*;

public class MapExample {
    public static void main(String[] args) {
        // HashMap
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Alice", 25);
        hashMap.put("Bob", 30);
        hashMap.put("Charlie", 28);
        System.out.println("HashMap: " + hashMap);
        
        // Access
        System.out.println("Alice's age: " + hashMap.get("Alice"));
        
        // Check
        System.out.println("Contains Bob? " + hashMap.containsKey("Bob"));
        
        // Iterate
        System.out.println("\nIterating:");
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + " => " + entry.getValue());
        }
        
        // TreeMap - sorted by keys
        Map<String, Integer> treeMap = new TreeMap<>(hashMap);
        System.out.println("\nTreeMap (sorted): " + treeMap);
    }
}
```

## Common Methods:

```java
put(K key, V value)        // Add/update
get(Object key)            // Retrieve value
remove(Object key)         // Remove entry
containsKey(Object key)    // Check key exists
containsValue(Object value)// Check value exists
keySet()                   // Get all keys
values()                   // Get all values
entrySet()                 // Get all key-value pairs
size()                     // Number of entries
isEmpty()                  // Check if empty
clear()                    // Remove all
```

**Next:** Explore each Map implementation in detail!

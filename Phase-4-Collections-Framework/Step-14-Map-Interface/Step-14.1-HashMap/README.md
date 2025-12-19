# Step 14.1: HashMap

**HashMap** stores key-value pairs using hash table. Fast, unordered.

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("Alice", 25);
        map.put("Bob", 30);
        map.put("Charlie", 28);
        
        System.out.println("Map: " + map);
        System.out.println("Alice's age: " + map.get("Alice"));
        
        // Iterate
        map.forEach((name, age) -> 
            System.out.println(name + " is " + age + " years old"));
    }
}
```

**Time Complexity:** O(1) average for get, put, remove

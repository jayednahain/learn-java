# Step 14.3: TreeMap

**TreeMap** stores entries sorted by keys.

```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        TreeMap<String, Integer> map = new TreeMap<>();
        map.put("C", 3);
        map.put("A", 1);
        map.put("B", 2);
        
        System.out.println(map);  // {A=1, B=2, C=3} - sorted by key
        System.out.println("First key: " + map.firstKey());
        System.out.println("Last key: " + map.lastKey());
    }
}
```

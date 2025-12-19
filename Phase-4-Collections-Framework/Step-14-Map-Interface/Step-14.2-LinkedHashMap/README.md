# Step 14.2: LinkedHashMap

**LinkedHashMap** maintains insertion order.

```java
import java.util.LinkedHashMap;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
        map.put("C", 3);
        map.put("A", 1);
        map.put("B", 2);
        
        System.out.println(map);  // {C=3, A=1, B=2} - insertion order
    }
}
```

# Step 13.2: LinkedHashSet

**LinkedHashSet** maintains insertion order using linked list.

```java
import java.util.LinkedHashSet;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        LinkedHashSet<Integer> set = new LinkedHashSet<>();
        set.add(30);
        set.add(10);
        set.add(20);
        
        System.out.println(set);  // [30, 10, 20] - insertion order maintained
    }
}
```

**Use when:** Need set with predictable iteration order

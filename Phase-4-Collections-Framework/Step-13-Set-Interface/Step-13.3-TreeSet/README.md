# Step 13.3: TreeSet

**TreeSet** stores elements in sorted order using Red-Black tree.

```java
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        TreeSet<Integer> set = new TreeSet<>();
        set.add(30);
        set.add(10);
        set.add(20);
        
        System.out.println(set);  // [10, 20, 30] - always sorted
        System.out.println("First: " + set.first());
        System.out.println("Last: " + set.last());
    }
}
```

**Time Complexity:** O(log n) for add, remove, contains

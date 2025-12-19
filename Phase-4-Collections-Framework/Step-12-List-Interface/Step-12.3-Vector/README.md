# Step 12.3: Vector

## What is Vector?

**Vector** is a legacy synchronized version of ArrayList. It's thread-safe but has performance overhead.

### Key Features:
- Synchronized (thread-safe)
- Similar to ArrayList but slower
- Legacy class (pre-Java 1.2)
- Default capacity: 10, doubles when full

### Modern Alternative:
Use `Collections.synchronizedList(new ArrayList<>())` or `CopyOnWriteArrayList` instead.

## Quick Example:

```java
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();
        
        vector.add(10);
        vector.add(20);
        vector.add(30);
        
        System.out.println("Vector: " + vector);
        System.out.println("Capacity: " + vector.capacity());
        System.out.println("Size: " + vector.size());
    }
}
```

**Next:** [Step 13: Set Interface](../../Step-13-Set-Interface/Step-13.1-HashSet/README.md)

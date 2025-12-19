# Step 12.2: LinkedList

## What is LinkedList?

**LinkedList** is a doubly-linked list implementation. Each element (node) contains data and references to next and previous elements.

### Key Features:
- Fast insertion/deletion at both ends: O(1)
- Slow random access: O(n)
- Implements both List and Deque interfaces
- No initial capacity needed
- More memory per element (stores two references)

### When to Use:
✅ Frequent insertions/deletions at beginning or end
✅ Implementing queue or deque
❌ Frequent random access by index
❌ Memory-constrained applications

## Quick Example:

```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        
        // Adding elements
        list.add("A");
        list.add("B");
        list.addFirst("Start");  // Add at beginning
        list.addLast("End");     // Add at end
        
        System.out.println("LinkedList: " + list);
        
        // Accessing
        System.out.println("First: " + list.getFirst());
        System.out.println("Last: " + list.getLast());
        
        // Removing
        list.removeFirst();
        list.removeLast();
        System.out.println("After removal: " + list);
    }
}
```

### ArrayList vs LinkedList:

| Operation | ArrayList | LinkedList |
|-----------|-----------|------------|
| get(index) | O(1) | O(n) |
| add() at end | O(1) | O(1) |
| add(index) | O(n) | O(n) |
| remove() first | O(n) | O(1) |

**Next:** [Step 12.3: Vector](../Step-12.3-Vector/README.md)

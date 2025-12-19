# Step 15: Queue Interface

**Queue** holds elements prior to processing (FIFO - First In First Out).

## Implementations:

### PriorityQueue
Elements ordered by priority (natural order or comparator).

### ArrayDeque
Resizable array implementation of Deque (double-ended queue).

### LinkedList
Also implements Queue interface.

## Quick Example:

```java
import java.util.*;

public class QueueExample {
    public static void main(String[] args) {
        // PriorityQueue - natural order
        Queue<Integer> pq = new PriorityQueue<>();
        pq.offer(30);
        pq.offer(10);
        pq.offer(20);
        
        System.out.println("PriorityQueue:");
        while (!pq.isEmpty()) {
            System.out.println(pq.poll());  // 10, 20, 30 (sorted)
        }
        
        // ArrayDeque - FIFO
        Deque<String> deque = new ArrayDeque<>();
        deque.addLast("First");
        deque.addLast("Second");
        deque.addFirst("Before First");
        
        System.out.println("\nDeque: " + deque);
    }
}
```

## Common Methods:

```java
offer(E e)  // Add element (preferred)
add(E e)    // Add element (throws exception if fails)
poll()      // Remove and return head (returns null if empty)
remove()    // Remove and return head (throws exception if empty)
peek()      // Return head without removing (returns null if empty)
element()   // Return head without removing (throws exception if empty)
```

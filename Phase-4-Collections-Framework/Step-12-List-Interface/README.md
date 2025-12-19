# Step 12: List Interface

The **List** interface represents an ordered collection (sequence). Lists allow:
- Duplicate elements
- Positional access (index-based)
- Insertion order maintained

## Implementations:

### [12.1 ArrayList](Step-12.1-ArrayList/README.md)
- Resizable array implementation
- Fast random access O(1)
- Slow insertion/deletion O(n)
- **Use when**: Frequent access by index

### [12.2 LinkedList](Step-12.2-LinkedList/README.md)
- Doubly-linked list implementation
- Slow random access O(n)
- Fast insertion/deletion at ends O(1)
- **Use when**: Frequent insertions/deletions

### [12.3 Vector](Step-12.3-Vector/README.md)
- Legacy class (synchronized ArrayList)
- Thread-safe but slower
- **Use when**: Thread safety needed (prefer CopyOnWriteArrayList)

## Quick Comparison:

| Feature | ArrayList | LinkedList | Vector |
|---------|-----------|------------|--------|
| Structure | Dynamic array | Doubly-linked list | Synchronized array |
| Access | O(1) | O(n) | O(1) |
| Insert/Delete | O(n) | O(1) at ends | O(n) |
| Thread-safe | No | No | Yes |
| Performance | Fast reads | Fast insert/delete | Slower (synchronized) |

**Next:** Explore each implementation in detail!

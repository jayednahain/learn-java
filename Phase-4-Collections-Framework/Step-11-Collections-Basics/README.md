# Step 11: Collections Basics

## What is the Collections Framework?

The **Java Collections Framework** is a unified architecture for representing and manipulating collections of objects. It provides interfaces, implementations, and algorithms to work with groups of objects efficiently.

### Benefits:
- **Reduces programming effort**: Ready-to-use data structures
- **Increases performance**: Highly optimized implementations
- **Interoperability**: Standard interfaces allow communication between unrelated APIs
- **Reduces code maintenance**: Well-tested implementations
- **Reusability**: Generic algorithms work with multiple collection types

---

## Collection Hierarchy

```
                    Iterable<E>
                        |
                  Collection<E>
                /       |        \
             List<E>  Set<E>   Queue<E>
              /  |      |  \       |
         ArrayList  LinkedList  HashSet  TreeSet  PriorityQueue
          Vector              LinkedHashSet

                    Map<E>  (Not a Collection)
                      |
            HashMap  TreeMap  LinkedHashMap
             Hashtable
```

---

## Core Interfaces

### 1. **Collection Interface**
The root interface for List, Set, and Queue.

**Common Methods:**
- `add(E e)`: Add element
- `remove(Object o)`: Remove element
- `contains(Object o)`: Check if element exists
- `size()`: Get number of elements
- `isEmpty()`: Check if empty
- `clear()`: Remove all elements
- `iterator()`: Get iterator

### 2. **List Interface**
Ordered collection (sequence). Allows duplicates.

**Implementations:** ArrayList, LinkedList, Vector

### 3. **Set Interface**
Unordered collection. No duplicates allowed.

**Implementations:** HashSet, LinkedHashSet, TreeSet

### 4. **Queue Interface**
Holds elements prior to processing (FIFO typically).

**Implementations:** PriorityQueue, ArrayDeque, LinkedList

### 5. **Map Interface**
Key-value pairs. Not a Collection, but part of Collections Framework.

**Implementations:** HashMap, TreeMap, LinkedHashMap, Hashtable

---

## Example 1: Basic Collection Operations

```java
import java.util.*;

public class CollectionBasicsExample {
    public static void main(String[] args) {
        // Creating a Collection (using ArrayList as implementation)
        Collection<String> fruits = new ArrayList<>();
        
        // Adding elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        fruits.add("Mango");
        fruits.add("Apple");  // Duplicates allowed in List
        
        System.out.println("=== Collection Operations ===");
        System.out.println("Fruits: " + fruits);
        System.out.println("Size: " + fruits.size());
        System.out.println("Is empty: " + fruits.isEmpty());
        System.out.println("Contains 'Banana': " + fruits.contains("Banana"));
        System.out.println("Contains 'Grapes': " + fruits.contains("Grapes"));
        
        // Removing elements
        fruits.remove("Orange");
        System.out.println("\nAfter removing 'Orange': " + fruits);
        
        // Adding multiple elements
        Collection<String> moreFruits = Arrays.asList("Grapes", "Pineapple");
        fruits.addAll(moreFruits);
        System.out.println("After adding more fruits: " + fruits);
        
        // Checking if contains all
        System.out.println("Contains all moreFruits: " + fruits.containsAll(moreFruits));
        
        // Clearing all elements
        Collection<String> tempCollection = new ArrayList<>(fruits);
        tempCollection.clear();
        System.out.println("\nAfter clear: " + tempCollection);
        System.out.println("Is empty: " + tempCollection.isEmpty());
    }
}
```

**Output:**
```
=== Collection Operations ===
Fruits: [Apple, Banana, Orange, Mango, Apple]
Size: 5
Is empty: false
Contains 'Banana': true
Contains 'Grapes': false

After removing 'Orange': [Apple, Banana, Mango, Apple]
After adding more fruits: [Apple, Banana, Mango, Apple, Grapes, Pineapple]
Contains all moreFruits: true

After clear: []
Is empty: true
```

---

## Example 2: Iterator Interface

The **Iterator** is used to traverse collections.

```java
import java.util.*;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> languages = new ArrayList<>();
        languages.add("Java");
        languages.add("Python");
        languages.add("JavaScript");
        languages.add("C++");
        languages.add("Go");
        
        System.out.println("=== Using Iterator ===");
        
        // Getting iterator
        Iterator<String> iterator = languages.iterator();
        
        // hasNext() and next()
        while (iterator.hasNext()) {
            String language = iterator.next();
            System.out.println(language);
            
            // Removing element while iterating
            if (language.equals("C++")) {
                iterator.remove();  // Safe removal during iteration
            }
        }
        
        System.out.println("\nAfter removing 'C++': " + languages);
        
        // For-each loop (internally uses iterator)
        System.out.println("\n=== Using For-Each Loop ===");
        for (String lang : languages) {
            System.out.println(lang);
        }
    }
}
```

**Output:**
```
=== Using Iterator ===
Java
Python
JavaScript
C++
Go

After removing 'C++': [Java, Python, JavaScript, Go]

=== Using For-Each Loop ===
Java
Python
JavaScript
Go
```

---

## Example 3: Comparing List, Set, and Map

```java
import java.util.*;

public class CollectionTypesComparison {
    public static void main(String[] args) {
        System.out.println("=== LIST (ArrayList) ===");
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Apple");  // Duplicates allowed
        list.add("Cherry");
        System.out.println("List: " + list);
        System.out.println("Maintains order: Yes");
        System.out.println("Allows duplicates: Yes");
        System.out.println("Access by index: list.get(0) = " + list.get(0));
        
        System.out.println("\n=== SET (HashSet) ===");
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple");  // Duplicate ignored
        set.add("Cherry");
        System.out.println("Set: " + set);
        System.out.println("Maintains order: No (HashSet)");
        System.out.println("Allows duplicates: No");
        System.out.println("Access by index: Not supported");
        
        System.out.println("\n=== MAP (HashMap) ===");
        Map<String, Integer> map = new HashMap<>();
        map.put("Apple", 10);
        map.put("Banana", 20);
        map.put("Apple", 15);  // Updates value for existing key
        map.put("Cherry", 25);
        System.out.println("Map: " + map);
        System.out.println("Stores: Key-Value pairs");
        System.out.println("Allows duplicate keys: No (overwrites)");
        System.out.println("Allows duplicate values: Yes");
        System.out.println("Access by key: map.get(\"Apple\") = " + map.get("Apple"));
    }
}
```

**Output:**
```
=== LIST (ArrayList) ===
List: [Apple, Banana, Apple, Cherry]
Maintains order: Yes
Allows duplicates: Yes
Access by index: list.get(0) = Apple

=== SET (HashSet) ===
Set: [Apple, Cherry, Banana]
Maintains order: No (HashSet)
Allows duplicates: No
Access by index: Not supported

=== MAP (HashMap) ===
Map: {Apple=15, Cherry=25, Banana=20}
Stores: Key-Value pairs
Allows duplicate keys: No (overwrites)
Allows duplicate values: Yes
Access by key: map.get("Apple") = 15
```

---

## Key Interfaces Summary

| Interface | Ordered | Duplicates | Index Access | Null Elements |
|-----------|---------|------------|--------------|---------------|
| **List** | Yes | Yes | Yes | Yes (multiple) |
| **Set** | No* | No | No | Yes (one) |
| **Queue** | Yes | Yes | No | No** |
| **Map** | No* | No (keys) | By key | Yes (one null key)** |

*TreeSet, TreeMap, LinkedHashSet, LinkedHashMap maintain order
**Depends on implementation

---

## 2025 Interview Questions

### Basic Level

**Q1: What is the Java Collections Framework?**
**A:** The Java Collections Framework is a unified architecture for storing and manipulating groups of objects. It provides interfaces (List, Set, Map, Queue) and implementations (ArrayList, HashSet, HashMap, etc.) along with algorithms.

**Q2: What is the difference between Collection and Collections?**
**A:**
- **Collection**: Interface (singular) - root interface for List, Set, Queue
- **Collections**: Class (plural) - utility class with static methods for operating on collections

**Q3: What is the difference between List and Set?**
**A:**
- **List**: Ordered, allows duplicates, index-based access
- **Set**: Unordered*, no duplicates, no index access
(*TreeSet/LinkedHashSet maintain order)

**Q4: Why is Map not a part of the Collection interface?**
**A:** Map stores key-value pairs, not single elements. Collection interface methods (add, remove) are designed for single elements. Map has different methods (put, get) suitable for key-value pairs.

**Q5: What is an Iterator?**
**A:** Iterator is an interface used to traverse elements in a collection one by one. It provides methods: `hasNext()`, `next()`, and `remove()`.

### Intermediate Level

**Q6: What is the difference between Iterator and Iterable?**
**A:**
- **Iterable**: Interface with `iterator()` method that returns an Iterator. Collection extends Iterable.
- **Iterator**: Interface used to iterate over elements with `hasNext()`, `next()`, `remove()`.

**Q7: Can we add/remove elements while iterating using for-each loop?**
**A:** No, modifying collection during for-each loop throws `ConcurrentModificationException`. Use Iterator's `remove()` method instead.

```java
// Wrong
for (String s : list) {
    list.remove(s);  // ConcurrentModificationException
}

// Correct
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    it.next();
    it.remove();  // Safe
}
```

**Q8: What are the core interfaces in the Collections Framework?**
**A:**
1. Collection (root)
2. List (extends Collection)
3. Set (extends Collection)
4. Queue (extends Collection)
5. Map (separate hierarchy)

**Q9: What is fail-fast and fail-safe iterator?**
**A:**
- **Fail-fast**: Throws `ConcurrentModificationException` if collection is modified during iteration (ArrayList, HashMap)
- **Fail-safe**: Works on copy, doesn't throw exception (ConcurrentHashMap, CopyOnWriteArrayList)

**Q10: What is the difference between Comparable and Comparator?**
**A:**
- **Comparable**: Interface for natural ordering (single way). Class implements `compareTo()`.
- **Comparator**: Interface for custom ordering (multiple ways). Separate class implements `compare()`.

### Advanced Level

**Q11: How does the Collection Framework use Generics?**
**A:** Generics provide type safety. Collection<T> ensures only objects of type T can be added, catching errors at compile-time instead of runtime.

```java
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123);  // Compilation error
```

**Q12: What is the time complexity of basic operations in different collections?**
**A:**
- **ArrayList**: get O(1), add O(1) amortized, remove O(n)
- **LinkedList**: get O(n), add/remove at ends O(1)
- **HashSet**: add/remove/contains O(1) average
- **TreeSet**: add/remove/contains O(log n)
- **HashMap**: put/get O(1) average
- **TreeMap**: put/get O(log n)

**Q13: Can we store null elements in collections?**
**A:**
- **ArrayList, LinkedList, HashSet**: Yes
- **TreeSet, TreeMap**: No (throws NullPointerException)
- **HashMap**: One null key, multiple null values
- **Hashtable**: No null keys or values

**Q14: What is the difference between synchronized and concurrent collections?**
**A:**
- **Synchronized** (Vector, Hashtable): Lock entire collection, poor performance
- **Concurrent** (ConcurrentHashMap): Lock only segments, better performance in multithreading

**Q15: How to make a collection read-only?**
**A:** Use `Collections.unmodifiableList/Set/Map()`.

```java
List<String> list = new ArrayList<>();
list.add("A");
List<String> readOnly = Collections.unmodifiableList(list);
// readOnly.add("B");  // UnsupportedOperationException
```

---

## Key Takeaways

✅ Collections Framework provides standard interfaces and implementations
✅ Collection is interface, Collections is utility class
✅ List: ordered, duplicates allowed
✅ Set: no duplicates
✅ Map: key-value pairs
✅ Iterator for traversing collections
✅ Use generics for type safety
✅ Choose appropriate collection based on requirements

---

**Next Step:** [Step 12: List Interface](../Step-12-List-Interface/Step-12.1-ArrayList/README.md)

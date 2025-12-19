# Step 12.1: ArrayList

## What is ArrayList?

**ArrayList** is a resizable array implementation of the List interface. It provides dynamic arrays that can grow or shrink in size, unlike regular arrays which have fixed size.

### Key Features:
- **Dynamic size**: Grows automatically when needed
- **Index-based access**: Fast random access O(1)
- **Maintains insertion order**: Elements stay in the order they were added
- **Allows duplicates**: Can have multiple same elements
- **Allows null values**: Can store null elements
- **Not synchronized**: Not thread-safe (use Collections.synchronizedList() or CopyOnWriteArrayList for thread safety)

### Internal Working:
- Uses an internal array to store elements
- Default initial capacity: 10
- When full, creates new array of size: `(currentCapacity * 3/2) + 1`
- Copies all elements to the new array

---

## Common Methods

| Method | Description | Time Complexity |
|--------|-------------|-----------------|
| `add(E e)` | Adds element at end | O(1) amortized |
| `add(int index, E element)` | Inserts at specific position | O(n) |
| `get(int index)` | Returns element at index | O(1) |
| `set(int index, E element)` | Replaces element at index | O(1) |
| `remove(int index)` | Removes element at index | O(n) |
| `remove(Object o)` | Removes first occurrence | O(n) |
| `size()` | Returns number of elements | O(1) |
| `isEmpty()` | Checks if empty | O(1) |
| `contains(Object o)` | Checks if element exists | O(n) |
| `indexOf(Object o)` | Returns first index of element | O(n) |
| `clear()` | Removes all elements | O(n) |

---

## Example 1: Basic ArrayList Operations

```java
import java.util.ArrayList;

public class ArrayListBasicExample {
    public static void main(String[] args) {
        // Creating ArrayList
        ArrayList<String> fruits = new ArrayList<>();
        
        // Adding elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        fruits.add("Mango");
        fruits.add("Apple");  // Duplicates allowed
        
        System.out.println("=== ArrayList Operations ===");
        System.out.println("Fruits: " + fruits);
        System.out.println("Size: " + fruits.size());
        
        // Access by index
        System.out.println("\n=== Accessing Elements ===");
        System.out.println("Element at index 0: " + fruits.get(0));
        System.out.println("Element at index 2: " + fruits.get(2));
        
        // Modify element
        fruits.set(1, "Blueberry");
        System.out.println("\nAfter setting index 1 to 'Blueberry': " + fruits);
        
        // Insert at specific position
        fruits.add(2, "Cherry");
        System.out.println("After inserting 'Cherry' at index 2: " + fruits);
        
        // Check if contains
        System.out.println("\n=== Searching ===");
        System.out.println("Contains 'Mango': " + fruits.contains("Mango"));
        System.out.println("Contains 'Grapes': " + fruits.contains("Grapes"));
        System.out.println("Index of 'Apple': " + fruits.indexOf("Apple"));
        System.out.println("Last index of 'Apple': " + fruits.lastIndexOf("Apple"));
        
        // Remove elements
        System.out.println("\n=== Removing Elements ===");
        fruits.remove(0);  // Remove by index
        System.out.println("After removing index 0: " + fruits);
        
        fruits.remove("Mango");  // Remove by object
        System.out.println("After removing 'Mango': " + fruits);
        
        // Check empty
        System.out.println("\nIs empty: " + fruits.isEmpty());
        
        // Clear all
        fruits.clear();
        System.out.println("After clear: " + fruits);
        System.out.println("Is empty: " + fruits.isEmpty());
    }
}
```

---

## Example 2: Iterating ArrayList

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.ListIterator;

public class ArrayListIterationExample {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<>();
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        numbers.add(40);
        numbers.add(50);
        
        System.out.println("=== Method 1: For Loop ===");
        for (int i = 0; i < numbers.size(); i++) {
            System.out.println("Index " + i + ": " + numbers.get(i));
        }
        
        System.out.println("\n=== Method 2: Enhanced For Loop ===");
        for (Integer num : numbers) {
            System.out.println(num);
        }
        
        System.out.println("\n=== Method 3: Iterator ===");
        Iterator<Integer> iterator = numbers.iterator();
        while (iterator.hasNext()) {
            Integer num = iterator.next();
            System.out.println(num);
        }
        
        System.out.println("\n=== Method 4: ListIterator (Bidirectional) ===");
        ListIterator<Integer> listIterator = numbers.listIterator();
        
        System.out.println("Forward:");
        while (listIterator.hasNext()) {
            System.out.println(listIterator.next());
        }
        
        System.out.println("\nBackward:");
        while (listIterator.hasPrevious()) {
            System.out.println(listIterator.previous());
        }
        
        System.out.println("\n=== Method 5: forEach with Lambda (Java 8+) ===");
        numbers.forEach(num -> System.out.println(num));
        
        System.out.println("\n=== Method 6: Stream API (Java 8+) ===");
        numbers.stream().forEach(System.out::println);
    }
}
```

---

## Example 3: ArrayList with Custom Objects

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Student {
    private int id;
    private String name;
    private double gpa;
    
    public Student(int id, String name, double gpa) {
        this.id = id;
        this.name = name;
        this.gpa = gpa;
    }
    
    // Getters
    public int getId() { return id; }
    public String getName() { return name; }
    public double getGpa() { return gpa; }
    
    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "', gpa=" + gpa + "}";
    }
}

public class ArrayListCustomObjectExample {
    public static void main(String[] args) {
        ArrayList<Student> students = new ArrayList<>();
        
        // Adding students
        students.add(new Student(101, "Alice", 3.8));
        students.add(new Student(102, "Bob", 3.5));
        students.add(new Student(103, "Charlie", 3.9));
        students.add(new Student(104, "Diana", 3.7));
        
        System.out.println("=== All Students ===");
        for (Student student : students) {
            System.out.println(student);
        }
        
        // Sort by name
        System.out.println("\n=== Sorted by Name ===");
        Collections.sort(students, Comparator.comparing(Student::getName));
        students.forEach(System.out::println);
        
        // Sort by GPA (descending)
        System.out.println("\n=== Sorted by GPA (Descending) ===");
        Collections.sort(students, Comparator.comparingDouble(Student::getGpa).reversed());
        students.forEach(System.out::println);
        
        // Find student with highest GPA
        Student topStudent = Collections.max(students, Comparator.comparingDouble(Student::getGpa));
        System.out.println("\n=== Top Student ===");
        System.out.println(topStudent);
        
        // Filter students with GPA > 3.7
        System.out.println("\n=== Students with GPA > 3.7 ===");
        students.stream()
                .filter(s -> s.getGpa() > 3.7)
                .forEach(System.out::println);
    }
}
```

---

## 2025 Interview Questions

**Q1: How does ArrayList work internally?**
**A:** ArrayList uses a dynamic array internally. When it reaches capacity, it creates a new array (1.5x size), copies all elements, and discards the old array.

**Q2: What is the default capacity of ArrayList?**
**A:** The default initial capacity is 10.

**Q3: What is the difference between size() and capacity()?**
**A:** 
- `size()`: Number of elements currently in the ArrayList
- `capacity()`: Total space available (internal array size)

**Q4: When to use ArrayList?**
**A:** Use ArrayList when:
- Need fast random access by index
- More reads than insertions/deletions
- Don't know the size in advance

**Q5: How to synchronize ArrayList?**
**A:** 
```java
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
// Or use CopyOnWriteArrayList
```

---

**Next:** [Step 12.2: LinkedList](../Step-12.2-LinkedList/README.md)

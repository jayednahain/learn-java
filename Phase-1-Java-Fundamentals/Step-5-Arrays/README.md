# Step 5: Arrays

## Overview
An array is a collection of similar type of elements stored in contiguous memory locations. Arrays allow you to store multiple values of the same data type under a single variable name.

## Key Concepts

### 1. What is an Array?
- Fixed-size collection of elements
- Elements are of the same data type
- Indexed from 0 to (length - 1)
- Stored in contiguous memory

### 2. Types of Arrays
- **Single-dimensional arrays**: Linear list of elements
- **Multi-dimensional arrays**: Array of arrays (2D, 3D, etc.)

### 3. Array Declaration and Initialization
```java
// Declaration
dataType[] arrayName;  // Preferred
dataType arrayName[];  // Also valid

// Initialization
arrayName = new dataType[size];

// Combined
int[] numbers = new int[5];

// Direct initialization
int[] numbers = {1, 2, 3, 4, 5};
```

---

## Code Examples

### Example 1: Single-Dimensional Arrays
```java
public class SingleArrayDemo {
    public static void main(String[] args) {
        // Method 1: Declare then initialize
        int[] numbers;
        numbers = new int[5];  // Array of size 5
        
        // Assigning values
        numbers[0] = 10;
        numbers[1] = 20;
        numbers[2] = 30;
        numbers[3] = 40;
        numbers[4] = 50;
        
        // Accessing elements
        System.out.println("First element: " + numbers[0]);
        System.out.println("Last element: " + numbers[4]);
        System.out.println("Array length: " + numbers.length);
        
        // Method 2: Declare and initialize together
        int[] scores = {85, 90, 78, 92, 88};
        
        // Iterating using for loop
        System.out.println("\nScores using for loop:");
        for (int i = 0; i < scores.length; i++) {
            System.out.println("Score " + (i+1) + ": " + scores[i]);
        }
        
        // Iterating using enhanced for loop
        System.out.println("\nScores using for-each:");
        for (int score : scores) {
            System.out.println(score);
        }
        
        // String array
        String[] names = {"Alice", "Bob", "Charlie", "David"};
        System.out.println("\nNames:");
        for (String name : names) {
            System.out.println(name);
        }
        
        // Finding sum and average
        int sum = 0;
        for (int score : scores) {
            sum += score;
        }
        double average = (double) sum / scores.length;
        System.out.println("\nTotal: " + sum);
        System.out.println("Average: " + average);
        
        // Finding maximum
        int max = scores[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > max) {
                max = scores[i];
            }
        }
        System.out.println("Maximum score: " + max);
    }
}
```

### Example 2: Multi-Dimensional Arrays (2D Arrays)
```java
public class MultiDimensionalArrayDemo {
    public static void main(String[] args) {
        // 2D Array - Matrix representation
        // Method 1: Declaration and initialization
        int[][] matrix = new int[3][4];  // 3 rows, 4 columns
        
        // Assigning values
        matrix[0][0] = 1;
        matrix[0][1] = 2;
        matrix[0][2] = 3;
        matrix[0][3] = 4;
        // ... and so on
        
        // Method 2: Direct initialization
        int[][] numbers = {
            {1, 2, 3, 4},
            {5, 6, 7, 8},
            {9, 10, 11, 12}
        };
        
        System.out.println("2D Array:");
        // Printing 2D array using nested loops
        for (int i = 0; i < numbers.length; i++) {
            for (int j = 0; j < numbers[i].length; j++) {
                System.out.print(numbers[i][j] + "\t");
            }
            System.out.println();
        }
        
        // Enhanced for loop with 2D array
        System.out.println("\nUsing for-each:");
        for (int[] row : numbers) {
            for (int num : row) {
                System.out.print(num + "\t");
            }
            System.out.println();
        }
        
        // Jagged array (irregular 2D array)
        int[][] jagged = {
            {1, 2},
            {3, 4, 5, 6},
            {7, 8, 9}
        };
        
        System.out.println("\nJagged Array:");
        for (int i = 0; i < jagged.length; i++) {
            for (int j = 0; j < jagged[i].length; j++) {
                System.out.print(jagged[i][j] + " ");
            }
            System.out.println();
        }
        
        // 3D Array
        int[][][] cube = {
            {{1, 2}, {3, 4}},
            {{5, 6}, {7, 8}}
        };
        
        System.out.println("\n3D Array:");
        for (int i = 0; i < cube.length; i++) {
            for (int j = 0; j < cube[i].length; j++) {
                for (int k = 0; k < cube[i][j].length; k++) {
                    System.out.print(cube[i][j][k] + " ");
                }
                System.out.println();
            }
            System.out.println();
        }
    }
}
```

### Example 3: Array Operations and Algorithms
```java
import java.util.Arrays;

public class ArrayOperationsDemo {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 9, 3, 7};
        
        System.out.println("Original array: " + Arrays.toString(numbers));
        
        // 1. Find minimum and maximum
        int min = numbers[0];
        int max = numbers[0];
        for (int num : numbers) {
            if (num < min) min = num;
            if (num > max) max = num;
        }
        System.out.println("Min: " + min + ", Max: " + max);
        
        // 2. Linear Search
        int searchElement = 9;
        int index = -1;
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == searchElement) {
                index = i;
                break;
            }
        }
        System.out.println(searchElement + " found at index: " + index);
        
        // 3. Reverse array
        int[] reversed = new int[numbers.length];
        for (int i = 0; i < numbers.length; i++) {
            reversed[i] = numbers[numbers.length - 1 - i];
        }
        System.out.println("Reversed: " + Arrays.toString(reversed));
        
        // 4. Reverse in-place
        int[] inPlace = numbers.clone();
        for (int i = 0; i < inPlace.length / 2; i++) {
            int temp = inPlace[i];
            inPlace[i] = inPlace[inPlace.length - 1 - i];
            inPlace[inPlace.length - 1 - i] = temp;
        }
        System.out.println("Reversed in-place: " + Arrays.toString(inPlace));
        
        // 5. Copy array
        int[] copy1 = numbers.clone();
        int[] copy2 = Arrays.copyOf(numbers, numbers.length);
        int[] copy3 = new int[numbers.length];
        System.arraycopy(numbers, 0, copy3, 0, numbers.length);
        
        // 6. Sort array (using Arrays.sort())
        int[] sorted = numbers.clone();
        Arrays.sort(sorted);
        System.out.println("Sorted: " + Arrays.toString(sorted));
        
        // 7. Binary Search (array must be sorted)
        int result = Arrays.binarySearch(sorted, 8);
        System.out.println("Binary search for 8: index " + result);
        
        // 8. Fill array with same value
        int[] filled = new int[5];
        Arrays.fill(filled, 10);
        System.out.println("Filled array: " + Arrays.toString(filled));
        
        // 9. Check if two arrays are equal
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        System.out.println("Arrays equal? " + Arrays.equals(arr1, arr2));
        
        // 10. Sum of array elements
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        System.out.println("Sum: " + sum);
        
        // 11. Count occurrences
        int[] data = {1, 2, 3, 2, 4, 2, 5};
        int countOf2 = 0;
        for (int num : data) {
            if (num == 2) countOf2++;
        }
        System.out.println("Occurrences of 2: " + countOf2);
    }
}
```

---

## Important Points to Remember

1. **Array Index**: Starts from 0 to (length - 1)
   ```java
   int[] arr = {10, 20, 30};
   // arr[0] = 10, arr[1] = 20, arr[2] = 30
   ```

2. **Array Length**: Fixed at creation, use `.length` property
   ```java
   int size = arr.length;  // No parentheses!
   ```

3. **Default Values**:
   - Numeric: 0
   - boolean: false
   - char: '\u0000'
   - Object references: null

4. **ArrayIndexOutOfBoundsException**: Accessing invalid index
   ```java
   int[] arr = new int[5];
   arr[5] = 10;  // Error! Index 5 is out of bounds
   ```

5. **Arrays are Objects**: Stored in heap memory

6. **Array Copy**: Use `.clone()`, `Arrays.copyOf()`, or `System.arraycopy()`

---

## Interview Questions (2025)

### Q1: What is an array? What are its advantages and disadvantages?
**Answer**:

**Definition**: An array is a fixed-size, indexed collection of elements of the same data type stored in contiguous memory.

**Advantages**:
1. **Random Access**: Direct access to elements using index - O(1) time
2. **Memory Efficient**: No overhead for storing links/pointers
3. **Cache Friendly**: Contiguous memory improves cache performance
4. **Simple Iteration**: Easy to traverse using loops

**Disadvantages**:
1. **Fixed Size**: Cannot resize after creation
2. **Homogeneous**: Only one data type allowed
3. **Insertion/Deletion**: Expensive (requires shifting elements)
4. **Wasted Space**: If array not fully used

```java
int[] arr = new int[100];  // Wastes space if only 10 elements used
```

### Q2: What is the difference between array and ArrayList?
**Answer**:

| Feature | Array | ArrayList |
|---------|-------|-----------|
| Size | Fixed | Dynamic (resizable) |
| Type | Primitive or Object | Only Objects (uses autoboxing) |
| Performance | Faster | Slightly slower |
| Memory | Less overhead | More overhead |
| Methods | Limited | Rich methods (add, remove, etc.) |
| Dimensions | Multi-dimensional | Single dimension |

```java
// Array
int[] arr = new int[5];  // Fixed size
// arr.add(10);  // No such method

// ArrayList
ArrayList<Integer> list = new ArrayList<>();
list.add(10);  // Dynamic
list.add(20);
list.remove(0);  // Easy deletion
```

**When to use**:
- **Array**: Fixed size, performance-critical, primitive types, multi-dimensional
- **ArrayList**: Dynamic size, frequent insertions/deletions

### Q3: How do you declare and initialize an array in Java?
**Answer**:

**Declaration**:
```java
int[] arr;          // Preferred
int arr[];          // Also valid (C-style)
String[] names;
double[][] matrix;
```

**Initialization**:
```java
// Method 1: Declare then initialize
int[] arr;
arr = new int[5];  // Size 5, default values 0

// Method 2: Combined
int[] arr = new int[5];

// Method 3: Direct initialization
int[] arr = {1, 2, 3, 4, 5};  // Size inferred

// Method 4: Anonymous array
printArray(new int[]{1, 2, 3});

// 2D Array
int[][] matrix = new int[3][4];
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

**Default Values**:
```java
int[] nums = new int[3];      // {0, 0, 0}
boolean[] flags = new boolean[3];  // {false, false, false}
String[] names = new String[3];    // {null, null, null}
```

### Q4: Can we change the size of an array after creation?
**Answer**:
**No**, arrays in Java have fixed size once created. The size cannot be changed.

**Workaround**:
1. **Create new larger array**:
   ```java
   int[] arr = {1, 2, 3};
   int[] larger = new int[5];
   System.arraycopy(arr, 0, larger, 0, arr.length);
   arr = larger;  // Reassign reference
   ```

2. **Use Arrays.copyOf()**:
   ```java
   int[] arr = {1, 2, 3};
   arr = Arrays.copyOf(arr, 5);  // New array size 5
   ```

3. **Use ArrayList** (dynamic):
   ```java
   ArrayList<Integer> list = new ArrayList<>();
   list.add(1);  // Grows automatically
   ```

**Why fixed size?**
- Performance: No overhead for resizing
- Memory: Allocated once in contiguous block

### Q5: What is the difference between length and length() in Java?
**Answer**:

**length (property)**:
- Used with **arrays**
- Not a method (no parentheses)
- Returns array size

```java
int[] arr = {1, 2, 3};
System.out.println(arr.length);  // 3
```

**length() (method)**:
- Used with **String**
- Method call (requires parentheses)
- Returns string length

```java
String str = "Hello";
System.out.println(str.length());  // 5
```

**size() (method)**:
- Used with **Collections** (ArrayList, HashMap, etc.)
```java
ArrayList<Integer> list = new ArrayList<>();
list.add(10);
System.out.println(list.size());  // 1
```

**Common mistake**:
```java
int[] arr = {1, 2, 3};
// arr.length()  // Error! No such method
// arr.size()    // Error!

String str = "Hello";
// str.length   // Error! length is a method for String
```

### Q6: What is ArrayIndexOutOfBoundsException?
**Answer**:
**ArrayIndexOutOfBoundsException** is a runtime exception thrown when trying to access an array element with an invalid index (negative or >= array length).

**Example**:
```java
int[] arr = {10, 20, 30};  // Valid indices: 0, 1, 2

System.out.println(arr[3]);  // Error! Index 3 is out of bounds
System.out.println(arr[-1]); // Error! Negative index
```

**Common scenarios**:
```java
// 1. Loop error
for (int i = 0; i <= arr.length; i++) {  // Should be <
    System.out.println(arr[i]);  // Error at i = arr.length
}

// 2. Off-by-one error
int[] arr = new int[5];
arr[5] = 10;  // Error! Last valid index is 4

// 3. Empty array
int[] empty = new int[0];
System.out.println(empty[0]);  // Error!
```

**Prevention**:
```java
// Check bounds
if (index >= 0 && index < arr.length) {
    System.out.println(arr[index]);
}

// Use try-catch
try {
    System.out.println(arr[index]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Invalid index");
}
```

### Q7: How do you copy an array in Java?
**Answer**:

**4 Ways to copy arrays**:

**1. clone() method**:
```java
int[] original = {1, 2, 3};
int[] copy = original.clone();
```
- Creates shallow copy
- Fast and simple

**2. Arrays.copyOf()**:
```java
int[] copy = Arrays.copyOf(original, original.length);
int[] larger = Arrays.copyOf(original, 5);  // New size
```
- Can change size
- Part of java.util.Arrays

**3. System.arraycopy()**:
```java
int[] copy = new int[original.length];
System.arraycopy(original, 0, copy, 0, original.length);
```
- Most flexible
- Can copy portion of array
- Native method (fast)

**4. Manual copy (loop)**:
```java
int[] copy = new int[original.length];
for (int i = 0; i < original.length; i++) {
    copy[i] = original[i];
}
```

**Shallow vs Deep Copy**:
```java
// For primitive arrays - all methods create deep copy
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1.clone();
arr2[0] = 99;
System.out.println(arr1[0]);  // 1 (not affected)

// For object arrays - shallow copy
String[] names1 = {"Alice", "Bob"};
String[] names2 = names1.clone();
// Both reference same String objects (but Strings are immutable)
```

### Q8: What is a jagged array?
**Answer**:
A **jagged array** is a multi-dimensional array where each row can have different number of columns (irregular shape).

**Example**:
```java
int[][] jagged = {
    {1, 2},           // Row 0: 2 elements
    {3, 4, 5, 6},     // Row 1: 4 elements
    {7, 8, 9}         // Row 2: 3 elements
};

System.out.println(jagged[0].length);  // 2
System.out.println(jagged[1].length);  // 4
System.out.println(jagged[2].length);  // 3
```

**Creating jagged array**:
```java
int[][] jagged = new int[3][];  // 3 rows, columns not specified
jagged[0] = new int[2];
jagged[1] = new int[4];
jagged[2] = new int[3];
```

**Iterating**:
```java
for (int i = 0; i < jagged.length; i++) {
    for (int j = 0; j < jagged[i].length; j++) {
        System.out.print(jagged[i][j] + " ");
    }
    System.out.println();
}
```

**Use case**: 
- Variable-length data (e.g., different number of students in each class)
- Memory efficient (don't allocate unused space)

**Regular vs Jagged**:
```java
// Regular (rectangular)
int[][] regular = new int[3][4];  // All rows have 4 columns

// Jagged
int[][] jagged = new int[3][];  // Rows can have different columns
```

### Q9: Can we store different data types in an array?
**Answer**:
**No, arrays in Java are homogeneous** - they can store only one data type.

```java
int[] arr = {1, 2, 3.5, "hello"};  // Compilation Error!
```

**Workarounds**:

**1. Object array** (not recommended):
```java
Object[] mixed = {1, "Hello", 3.14, true};
// Loses type safety, requires casting
int num = (Integer) mixed[0];
```

**2. Wrapper classes with superclass**:
```java
Number[] numbers = {10, 20.5, 30L};  // Integer, Double, Long
// All extend Number class
```

**3. Use ArrayList with generics**:
```java
ArrayList<Object> list = new ArrayList<>();
list.add(1);
list.add("Hello");
list.add(3.14);
```

**Best practice**: Avoid mixing types. Use proper data structures or create custom classes.

### Q10: How do you search for an element in an array?
**Answer**:

**1. Linear Search** (Unsorted array):
```java
public static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;  // Found at index i
        }
    }
    return -1;  // Not found
}
// Time Complexity: O(n)
```

**2. Binary Search** (Sorted array):
```java
public static int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            return mid;  // Found
        }
        if (arr[mid] < target) {
            left = mid + 1;  // Search right half
        } else {
            right = mid - 1;  // Search left half
        }
    }
    return -1;  // Not found
}
// Time Complexity: O(log n)
```

**3. Using Arrays.binarySearch()** (Sorted array):
```java
int[] arr = {1, 3, 5, 7, 9};
int index = Arrays.binarySearch(arr, 5);  // Returns 2
```

**4. Enhanced for loop** (Simple search):
```java
boolean found = false;
for (int num : arr) {
    if (num == target) {
        found = true;
        break;
    }
}
```

**When to use**:
- **Linear Search**: Unsorted array, small size
- **Binary Search**: Sorted array, large size (faster)

---

## Practice Exercises

1. Write a program to find the second largest element in an array
2. Merge two sorted arrays into one sorted array
3. Rotate an array to the right by k positions
4. Find all pairs in an array that sum to a given number
5. Implement bubble sort or selection sort on an array
6. Create a program to add two matrices (2D arrays)
7. Remove duplicates from an array
8. Find the missing number in an array of 1 to n

---

## Next Step
Congratulations! You've completed **Phase 1: Java Fundamentals**. Move to **Phase 2: Object-Oriented Programming Basics** to learn about methods, classes, and OOP principles.

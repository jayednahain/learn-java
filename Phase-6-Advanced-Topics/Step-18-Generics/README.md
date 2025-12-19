# Step 18: Generics

## What are Generics?

**Generics** enable types (classes and interfaces) to be parameters when defining classes, interfaces, and methods. They provide compile-time type safety and eliminate the need for casting.

### Benefits:
- **Type Safety**: Compile-time checking prevents ClassCastException
- **No Casting**: No need to cast objects
- **Code Reusability**: Write once, use with any type
- **Generic Algorithms**: Write algorithms that work on different types

---

## Generic Class

```java
// Generic class with type parameter T
class Box<T> {
    private T content;
    
    public void set(T content) {
        this.content = content;
    }
    
    public T get() {
        return content;
    }
}

public class GenericClassExample {
    public static void main(String[] args) {
        // Box for Integer
        Box<Integer> intBox = new Box<>();
        intBox.set(123);
        Integer value = intBox.get();  // No casting needed
        System.out.println("Integer Box: " + value);
        
        // Box for String
        Box<String> strBox = new Box<>();
        strBox.set("Hello Generics");
        String str = strBox.get();
        System.out.println("String Box: " + str);
        
        // Box for custom object
        Box<Person> personBox = new Box<>();
        personBox.set(new Person("Alice", 25));
        System.out.println("Person Box: " + personBox.get());
    }
}

class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

---

## Generic Methods

```java
public class GenericMethodExample {
    // Generic method
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
    
    // Generic method with return type
    public static <T> T getFirst(T[] array) {
        return array.length > 0 ? array[0] : null;
    }
    
    // Multiple type parameters
    public static <K, V> void printKeyValue(K key, V value) {
        System.out.println(key + " => " + value);
    }
    
    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"Java", "Python", "C++"};
        
        System.out.println("=== Generic Method ===");
        printArray(intArray);
        printArray(strArray);
        
        System.out.println("\n=== Generic Method with Return ===");
        System.out.println("First integer: " + getFirst(intArray));
        System.out.println("First string: " + getFirst(strArray));
        
        System.out.println("\n=== Multiple Type Parameters ===");
        printKeyValue("Name", "Alice");
        printKeyValue(1, "One");
        printKeyValue("Age", 25);
    }
}
```

---

## Bounded Type Parameters

```java
// Upper bound: T must be Number or its subclass
class Calculator<T extends Number> {
    private T num1;
    private T num2;
    
    public Calculator(T num1, T num2) {
        this.num1 = num1;
        this.num2 = num2;
    }
    
    public double sum() {
        return num1.doubleValue() + num2.doubleValue();
    }
    
    public double multiply() {
        return num1.doubleValue() * num2.doubleValue();
    }
}

public class BoundedTypeExample {
    public static void main(String[] args) {
        Calculator<Integer> intCalc = new Calculator<>(10, 20);
        System.out.println("Integer Sum: " + intCalc.sum());
        System.out.println("Integer Multiply: " + intCalc.multiply());
        
        Calculator<Double> doubleCalc = new Calculator<>(5.5, 2.5);
        System.out.println("\nDouble Sum: " + doubleCalc.sum());
        System.out.println("Double Multiply: " + doubleCalc.multiply());
        
        // Calculator<String> strCalc = new Calculator<>("a", "b");  // ERROR!
    }
    
    // Method with bounded type parameter
    public static <T extends Comparable<T>> T getMax(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
}
```

---

## Wildcards

```java
import java.util.*;

public class WildcardExample {
    // Unbounded wildcard (?)
    public static void printList(List<?> list) {
        for (Object obj : list) {
            System.out.print(obj + " ");
        }
        System.out.println();
    }
    
    // Upper bounded wildcard (? extends Type)
    public static double sumOfNumbers(List<? extends Number> list) {
        double sum = 0;
        for (Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }
    
    // Lower bounded wildcard (? super Type)
    public static void addNumbers(List<? super Integer> list) {
        for (int i = 1; i <= 5; i++) {
            list.add(i);
        }
    }
    
    public static void main(String[] args) {
        System.out.println("=== Unbounded Wildcard ===");
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<String> strList = Arrays.asList("A", "B", "C");
        printList(intList);
        printList(strList);
        
        System.out.println("\n=== Upper Bounded Wildcard ===");
        List<Integer> integers = Arrays.asList(1, 2, 3, 4, 5);
        List<Double> doubles = Arrays.asList(1.1, 2.2, 3.3);
        System.out.println("Sum of integers: " + sumOfNumbers(integers));
        System.out.println("Sum of doubles: " + sumOfNumbers(doubles));
        
        System.out.println("\n=== Lower Bounded Wildcard ===");
        List<Number> numbers = new ArrayList<>();
        addNumbers(numbers);
        System.out.println("Numbers: " + numbers);
    }
}
```

---

## 2025 Interview Questions

**Q1: What are generics in Java?**
**A:** Generics enable types to be parameters when defining classes, interfaces, and methods. They provide compile-time type safety.

**Q2: What is type erasure?**
**A:** Java uses type erasure to implement generics. Generic type information is removed at runtime, replaced with Object or bounds.

**Q3: Can you create an instance of a generic type?**
**A:** No, due to type erasure: `T obj = new T();` // ERROR

**Q4: What is the difference between <?>, <? extends T>, and <? super T>?**
**A:**
- `<?>`: Unbounded wildcard (any type)
- `<? extends T>`: Upper bound (T or subclass) - Read only
- `<? super T>`: Lower bound (T or superclass) - Write only

**Q5: Can we have static generic methods?**
**A:** Yes, but not static generic variables:
```java
public static <T> void print(T t) { }  // OK
// private static T value;  // ERROR
```

---

**Next:** [Step 19: Lambda & Functional Programming](../Step-19-Lambda-Functional-Programming/README.md)

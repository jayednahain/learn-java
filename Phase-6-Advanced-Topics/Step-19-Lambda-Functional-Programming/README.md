# Step 19: Lambda Expressions & Functional Programming (Java 8+)

## What are Lambda Expressions?

**Lambda expressions** provide a clear and concise way to represent a functional interface using an expression. They enable functional programming in Java.

### Syntax:
```java
(parameters) -> expression
(parameters) -> { statements; }
```

### Benefits:
- **Concise code**: Less boilerplate
- **Functional programming**: Treat functions as first-class citizens
- **Parallel processing**: Easy with streams
- **Better readability**: For simple operations

---

## Functional Interfaces

A functional interface has exactly ONE abstract method. Used with lambda expressions.

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class LambdaBasicExample {
    public static void main(String[] args) {
        // Old way (Anonymous class)
        Calculator add = new Calculator() {
            @Override
            public int calculate(int a, int b) {
                return a + b;
            }
        };
        
        // Lambda way
        Calculator addLambda = (a, b) -> a + b;
        Calculator subtract = (a, b) -> a - b;
        Calculator multiply = (a, b) -> a * b;
        Calculator divide = (a, b) -> a / b;
        
        System.out.println("=== Lambda Expressions ===");
        System.out.println("10 + 5 = " + addLambda.calculate(10, 5));
        System.out.println("10 - 5 = " + subtract.calculate(10, 5));
        System.out.println("10 * 5 = " + multiply.calculate(10, 5));
        System.out.println("10 / 5 = " + divide.calculate(10, 5));
    }
}
```

---

## Built-in Functional Interfaces

Java provides several built-in functional interfaces in `java.util.function` package:

### 1. Predicate<T> - Test condition (returns boolean)

```java
import java.util.function.Predicate;
import java.util.Arrays;
import java.util.List;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = num -> num % 2 == 0;
        Predicate<Integer> isPositive = num -> num > 0;
        Predicate<String> isLong = str -> str.length() > 5;
        
        System.out.println("=== Predicate ===");
        System.out.println("Is 10 even? " + isEven.test(10));
        System.out.println("Is 7 even? " + isEven.test(7));
        System.out.println("Is -5 positive? " + isPositive.test(-5));
        System.out.println("Is 'HelloWorld' long? " + isLong.test("HelloWorld"));
        
        // Combining predicates
        Predicate<Integer> isEvenAndPositive = isEven.and(isPositive);
        System.out.println("\nIs 10 even AND positive? " + isEvenAndPositive.test(10));
        System.out.println("Is -10 even AND positive? " + isEvenAndPositive.test(-10));
        
        // Filter list using predicate
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        System.out.println("\nEven numbers:");
        numbers.stream()
               .filter(isEven)
               .forEach(System.out::println);
    }
}
```

### 2. Function<T, R> - Transform input to output

```java
import java.util.function.Function;
import java.util.Arrays;
import java.util.List;

public class FunctionExample {
    public static void main(String[] args) {
        Function<String, Integer> stringLength = str -> str.length();
        Function<Integer, Integer> square = num -> num * num;
        Function<String, String> toUpperCase = str -> str.toUpperCase();
        
        System.out.println("=== Function ===");
        System.out.println("Length of 'Hello': " + stringLength.apply("Hello"));
        System.out.println("Square of 5: " + square.apply(5));
        System.out.println("Uppercase 'java': " + toUpperCase.apply("java"));
        
        // Function composition
        Function<Integer, Integer> addTwo = num -> num + 2;
        Function<Integer, Integer> multiplyThree = num -> num * 3;
        Function<Integer, Integer> combined = addTwo.andThen(multiplyThree);
        
        System.out.println("\n(5 + 2) * 3 = " + combined.apply(5));
        
        // Map with function
        List<String> words = Arrays.asList("java", "python", "javascript");
        System.out.println("\nLengths:");
        words.stream()
             .map(stringLength)
             .forEach(System.out::println);
    }
}
```

### 3. Consumer<T> - Accept input, no return

```java
import java.util.function.Consumer;
import java.util.Arrays;
import java.util.List;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> printUpperCase = str -> System.out.println(str.toUpperCase());
        Consumer<Integer> printSquare = num -> System.out.println("Square: " + (num * num));
        
        System.out.println("=== Consumer ===");
        printUpperCase.accept("hello");
        printSquare.accept(5);
        
        // forEach with consumer
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        System.out.println("\nNames in uppercase:");
        names.forEach(printUpperCase);
        
        // Multiple operations
        Consumer<String> print = System.out::println;
        Consumer<String> printWithGreeting = str -> System.out.println("Hello, " + str);
        Consumer<String> combined = print.andThen(printWithGreeting);
        
        System.out.println("\nCombined consumer:");
        combined.accept("David");
    }
}
```

### 4. Supplier<T> - Provide output, no input

```java
import java.util.function.Supplier;
import java.util.Random;

public class SupplierExample {
    public static void main(String[] args) {
        Supplier<Double> randomValue = () -> Math.random();
        Supplier<Integer> randomInt = () -> new Random().nextInt(100);
        Supplier<String> greeting = () -> "Hello, World!";
        
        System.out.println("=== Supplier ===");
        System.out.println("Random value: " + randomValue.get());
        System.out.println("Random int: " + randomInt.get());
        System.out.println("Greeting: " + greeting.get());
        
        // Generate 5 random numbers
        System.out.println("\n5 random numbers:");
        for (int i = 0; i < 5; i++) {
            System.out.println(randomInt.get());
        }
    }
}
```

---

## Method References

Shorthand notation for lambda expressions calling a specific method.

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.*;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
        
        // 1. Static method reference
        Consumer<String> print1 = str -> System.out.println(str);
        Consumer<String> print2 = System.out::println;  // Method reference
        
        System.out.println("=== Static Method Reference ===");
        names.forEach(print2);
        
        // 2. Instance method reference
        String prefix = "Hello, ";
        Function<String, String> concat1 = str -> prefix.concat(str);
        Function<String, String> concat2 = prefix::concat;  // Method reference
        
        System.out.println("\n=== Instance Method Reference ===");
        System.out.println(concat2.apply("World"));
        
        // 3. Constructor reference
        Supplier<List> listSupplier1 = () -> new ArrayList<>();
        Supplier<List> listSupplier2 = ArrayList::new;  // Constructor reference
        
        System.out.println("\n=== Constructor Reference ===");
        List list = listSupplier2.get();
        System.out.println("Created list: " + list);
    }
}
```

---

## Streams API

Process collections functionally with operations like filter, map, reduce.

```java
import java.util.*;
import java.util.stream.Collectors;

public class StreamsExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        
        // Filter: Select even numbers
        System.out.println("=== Filter (Even Numbers) ===");
        List<Integer> evens = numbers.stream()
                                    .filter(n -> n % 2 == 0)
                                    .collect(Collectors.toList());
        System.out.println(evens);
        
        // Map: Square each number
        System.out.println("\n=== Map (Squares) ===");
        List<Integer> squares = numbers.stream()
                                      .map(n -> n * n)
                                      .collect(Collectors.toList());
        System.out.println(squares);
        
        // Reduce: Sum all numbers
        System.out.println("\n=== Reduce (Sum) ===");
        int sum = numbers.stream()
                        .reduce(0, (a, b) -> a + b);
        System.out.println("Sum: " + sum);
        
        // Chaining operations
        System.out.println("\n=== Chained Operations ===");
        int sumOfEvenSquares = numbers.stream()
                                     .filter(n -> n % 2 == 0)  // Even only
                                     .map(n -> n * n)          // Square
                                     .reduce(0, Integer::sum); // Sum
        System.out.println("Sum of even squares: " + sumOfEvenSquares);
        
        // Other useful operations
        System.out.println("\n=== Other Operations ===");
        System.out.println("Count: " + numbers.stream().count());
        System.out.println("Max: " + numbers.stream().max(Integer::compareTo).get());
        System.out.println("Min: " + numbers.stream().min(Integer::compareTo).get());
        System.out.println("Average: " + numbers.stream().mapToInt(Integer::intValue).average().getAsDouble());
        
        // Sorted
        List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
        System.out.println("\nOriginal: " + names);
        System.out.println("Sorted: " + names.stream().sorted().collect(Collectors.toList()));
    }
}
```

---

## 2025 Interview Questions

**Q1: What is a lambda expression?**
**A:** A lambda expression is a concise way to represent a functional interface using an expression. Syntax: `(parameters) -> expression`

**Q2: What is a functional interface?**
**A:** An interface with exactly ONE abstract method. Can be annotated with `@FunctionalInterface`.

**Q3: Can a lambda expression throw exceptions?**
**A:** Yes, but if it's a checked exception, the functional interface method must declare it.

**Q4: What is the difference between map() and flatMap()?**
**A:**
- `map()`: Transforms each element (one-to-one)
- `flatMap()`: Transforms each element to stream and flattens (one-to-many)

**Q5: What are the built-in functional interfaces?**
**A:**
- Predicate<T>: boolean test(T t)
- Function<T,R>: R apply(T t)
- Consumer<T>: void accept(T t)
- Supplier<T>: T get()

**Q6: What is method reference?**
**A:** Shorthand for lambda expressions calling a specific method. Types: static, instance, constructor.

**Q7: Are streams reusable?**
**A:** No, a stream can be consumed only once. Trying to reuse throws IllegalStateException.

---

**Next:** [Step 20: File I/O](../Step-20-File-IO/README.md)

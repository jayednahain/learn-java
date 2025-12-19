# Step 9: Interfaces

## Overview
An interface in Java is a blueprint of a class that contains only abstract methods and constants. It's used to achieve abstraction and multiple inheritance in Java.

## Key Concepts

### 1. What is an Interface?
- Collection of abstract methods (methods without body)
- Cannot be instantiated
- Implemented by classes using `implements` keyword
- Provides 100% abstraction (before Java 8)
- Supports multiple inheritance

### 2. Interface Features (Java 8+)
- Abstract methods (implicitly public and abstract)
- Default methods (with implementation)
- Static methods
- Constants (implicitly public, static, final)
- Private methods (Java 9+)

### 3. Why Use Interfaces?
- **Abstraction**: Hide implementation details
- **Multiple Inheritance**: Achieve multiple inheritance
- **Loose Coupling**: Reduce dependencies
- **Contract**: Define what a class must do, not how

---

## Code Examples

### Example 1: Basic Interface Implementation
```java
// Define interface
interface Animal {
    // Abstract methods (implicitly public abstract)
    void sound();
    void eat();
    
    // Constants (implicitly public static final)
    int LEGS = 4;
}

// Implement interface
class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks: Woof Woof!");
    }
    
    @Override
    public void eat() {
        System.out.println("Dog eats meat");
    }
}

class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("Cat meows: Meow Meow!");
    }
    
    @Override
    public void eat() {
        System.out.println("Cat eats fish");
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        // Interface reference, object implementation
        Animal dog = new Dog();
        dog.sound();
        dog.eat();
        System.out.println("Legs: " + Animal.LEGS);
        
        System.out.println();
        
        Animal cat = new Cat();
        cat.sound();
        cat.eat();
    }
}
```

**Output**:
```
Dog barks: Woof Woof!
Dog eats meat
Legs: 4

Cat meows: Meow Meow!
Cat eats fish
```

### Example 2: Multiple Interface Implementation
```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// Class implementing multiple interfaces
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}

class Fish implements Swimmable {
    @Override
    public void swim() {
        System.out.println("Fish is swimming");
    }
}

class Bird implements Flyable {
    @Override
    public void fly() {
        System.out.println("Bird is flying");
    }
}

public class MultipleInterfaceDemo {
    public static void main(String[] args) {
        Duck duck = new Duck();
        duck.fly();
        duck.swim();
        
        System.out.println();
        
        // Interface references
        Flyable flyingBird = new Bird();
        flyingBird.fly();
        
        Swimmable swimmingFish = new Fish();
        swimmingFish.swim();
    }
}
```

### Example 3: Default and Static Methods (Java 8+)
```java
interface Vehicle {
    // Abstract method
    void start();
    void stop();
    
    // Default method (with implementation)
    default void honk() {
        System.out.println("Beep! Beep!");
    }
    
    default void displayInfo() {
        System.out.println("This is a vehicle");
    }
    
    // Static method
    static void service() {
        System.out.println("Vehicle servicing in progress");
    }
}

class Car implements Vehicle {
    private String model;
    
    public Car(String model) {
        this.model = model;
    }
    
    @Override
    public void start() {
        System.out.println(model + " car started");
    }
    
    @Override
    public void stop() {
        System.out.println(model + " car stopped");
    }
    
    // Override default method (optional)
    @Override
    public void displayInfo() {
        System.out.println("This is a " + model + " car");
    }
}

class Bike implements Vehicle {
    @Override
    public void start() {
        System.out.println("Bike started");
    }
    
    @Override
    public void stop() {
        System.out.println("Bike stopped");
    }
    
    // Uses default honk() method
}

public class DefaultStaticMethodDemo {
    public static void main(String[] args) {
        Car car = new Car("Tesla");
        car.start();
        car.honk();           // Default method
        car.displayInfo();    // Overridden default method
        car.stop();
        
        System.out.println();
        
        Bike bike = new Bike();
        bike.start();
        bike.honk();          // Default method from interface
        bike.displayInfo();   // Default method from interface
        bike.stop();
        
        System.out.println();
        
        // Static method called using interface name
        Vehicle.service();
    }
}
```

---

## Important Points to Remember

1. **Interface vs Abstract Class**:
   - Interface: 100% abstraction (before Java 8), multiple inheritance
   - Abstract class: Partial abstraction, single inheritance

2. **All methods are public**: Interface methods are implicitly public

3. **Variables are constants**: All variables are `public static final`

4. **Cannot instantiate**: `new Interface()` not allowed

5. **Functional Interface**: Interface with single abstract method (SAM)
   ```java
   @FunctionalInterface
   interface Calculator {
       int calculate(int a, int b);
   }
   ```

6. **Marker Interface**: Empty interface (e.g., Serializable, Cloneable)

---

## Interview Questions (2025)

### Q1: What is an interface in Java? Why do we use it?
**Answer**:

**Definition**: An interface is a reference type in Java that contains only abstract methods, constants, default methods, static methods, and nested types. It defines a contract that classes must follow.

**Why Use Interfaces**:

1. **Abstraction**: Achieve 100% abstraction by hiding implementation details
   ```java
   interface Payment {
       void processPayment(double amount);
   }
   ```

2. **Multiple Inheritance**: Java doesn't support multiple class inheritance, but supports multiple interface implementation
   ```java
   class Duck implements Flyable, Swimmable { }
   ```

3. **Loose Coupling**: Reduce dependency between components
   ```java
   interface Database {
       void connect();
   }
   // Can switch between MySQL, MongoDB, Oracle
   ```

4. **Polymorphism**: Write flexible, extensible code
   ```java
   List<String> list = new ArrayList<>();  // Interface reference
   ```

5. **API Design**: Define contracts for frameworks and libraries

**Real-world example**: JDBC uses interfaces (Connection, Statement, ResultSet) - allows different database drivers to provide their own implementations.

### Q2: What is the difference between abstract class and interface?
**Answer**:

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Abstract + Concrete methods | Abstract + Default + Static (Java 8+) |
| Variables | Any type (instance, static, final) | Only constants (public static final) |
| Inheritance | Single inheritance (extends) | Multiple inheritance (implements) |
| Constructor | Can have constructor | Cannot have constructor |
| Access Modifiers | Any (public, private, protected) | Public only (implicitly) |
| Use Case | "is-a" relationship | "can-do" relationship |
| Speed | Faster | Slightly slower |
| When to Use | Share code among related classes | Unrelated classes with common behavior |

**Example**:
```java
// Abstract class - "is-a" relationship
abstract class Animal {
    String name;
    
    Animal(String name) {  // Constructor
        this.name = name;
    }
    
    abstract void sound();
    
    void sleep() {  // Concrete method
        System.out.println(name + " is sleeping");
    }
}

// Interface - "can-do" relationship
interface Flyable {
    void fly();  // What it can do
}

class Bird extends Animal implements Flyable {
    Bird(String name) {
        super(name);
    }
    
    void sound() {
        System.out.println("Chirp");
    }
    
    public void fly() {
        System.out.println("Flying");
    }
}
```

**Rule of thumb**:
- Use **abstract class** when classes are related and share common code
- Use **interface** when unrelated classes share common capability

### Q3: Can we have multiple inheritance in Java using interfaces?
**Answer**:
**Yes**, Java supports multiple inheritance through interfaces (not through classes).

**Example**:
```java
interface Printable {
    void print();
}

interface Showable {
    void show();
}

// Multiple interface implementation
class Document implements Printable, Showable {
    public void print() {
        System.out.println("Printing document");
    }
    
    public void show() {
        System.out.println("Showing document");
    }
}
```

**Why not multiple class inheritance?**
Diamond Problem:
```java
// This would cause ambiguity (not allowed in Java)
class A {
    void display() { System.out.println("A"); }
}

class B extends A {
    void display() { System.out.println("B"); }
}

class C extends A {
    void display() { System.out.println("C"); }
}

// If this were allowed:
// class D extends B, C { }
// Which display() would D inherit? Ambiguous!
```

**Interface solves this** because:
- Methods are abstract (no implementation conflict)
- With default methods (Java 8+), implementing class must override conflicting methods

```java
interface X {
    default void display() { System.out.println("X"); }
}

interface Y {
    default void display() { System.out.println("Y"); }
}

class Z implements X, Y {
    // Must override to resolve conflict
    public void display() {
        X.super.display();  // Or Y.super.display() or custom implementation
    }
}
```

### Q4: What are default methods in interfaces (Java 8)?
**Answer**:
**Default methods** are interface methods with implementation, introduced in Java 8. They allow adding new methods to interfaces without breaking existing implementations.

**Syntax**:
```java
interface MyInterface {
    // Abstract method
    void abstractMethod();
    
    // Default method
    default void defaultMethod() {
        System.out.println("Default implementation");
    }
}
```

**Why needed?**
Before Java 8, adding a new method to an interface would break all implementing classes.

```java
// Java 7 and before
interface List {
    void add(Object o);
    void remove(Object o);
    // Adding new method would break all implementations!
}
```

**Java 8 solution**:
```java
interface List {
    void add(Object o);
    void remove(Object o);
    
    // New method with default implementation
    default void forEach(Consumer<? super E> action) {
        // implementation
    }
}
// Existing implementations not broken!
```

**Example**:
```java
interface Vehicle {
    void start();
    
    default void honk() {
        System.out.println("Beep!");
    }
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car started");
    }
    // honk() inherited from interface
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike started");
    }
    
    // Override default method
    @Override
    public void honk() {
        System.out.println("Bike horn: Pee Pee!");
    }
}
```

**Key points**:
- Classes can override default methods
- Resolves multiple inheritance ambiguity
- Enables interface evolution without breaking code

### Q5: What is a functional interface?
**Answer**:
A **functional interface** is an interface with exactly one abstract method (SAM - Single Abstract Method). It can have multiple default or static methods, but only one abstract method.

**Annotation**: `@FunctionalInterface` (optional but recommended)

**Example**:
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);  // Single abstract method
    
    // Can have default methods
    default void display() {
        System.out.println("Calculator");
    }
    
    // Can have static methods
    static void info() {
        System.out.println("Performs calculations");
    }
}
```

**Why important?**
- Used with **lambda expressions** (Java 8+)
- Foundation for functional programming in Java

**Usage with lambda**:
```java
// Without lambda (verbose)
Calculator add = new Calculator() {
    public int calculate(int a, int b) {
        return a + b;
    }
};

// With lambda (concise)
Calculator add = (a, b) -> a + b;
Calculator subtract = (a, b) -> a - b;

System.out.println(add.calculate(10, 5));      // 15
System.out.println(subtract.calculate(10, 5)); // 5
```

**Built-in functional interfaces** (java.util.function):
- `Predicate<T>`: Takes T, returns boolean
- `Consumer<T>`: Takes T, returns void
- `Function<T,R>`: Takes T, returns R
- `Supplier<T>`: Takes nothing, returns T

**Example**:
```java
import java.util.function.Predicate;

Predicate<Integer> isEven = num -> num % 2 == 0;
System.out.println(isEven.test(10));  // true
System.out.println(isEven.test(7));   // false
```

### Q6: Can we create an object of an interface?
**Answer**:
**No**, we cannot directly instantiate an interface using `new Interface()`.

**Why?** Interfaces contain abstract methods (no implementation), so creating an object doesn't make sense.

**What we can do**:

**1. Anonymous Inner Class**:
```java
interface Greeting {
    void greet();
}

// Create anonymous implementation
Greeting greeting = new Greeting() {
    @Override
    public void greet() {
        System.out.println("Hello!");
    }
};
greeting.greet();
```

**2. Lambda Expression** (for functional interfaces):
```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

Calculator calc = (a, b) -> a + b;
System.out.println(calc.add(5, 3));  // 8
```

**3. Reference to implementing class object**:
```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}

// Interface reference, class object
Animal animal = new Dog();  // Valid
animal.sound();
```

**Invalid**:
```java
Animal animal = new Animal();  // Compilation Error!
```

### Q7: What are marker interfaces? Give examples.
**Answer**:
**Marker interfaces** (tag interfaces) are empty interfaces with no methods or fields. They're used to mark/tag a class to provide metadata to the JVM or compiler.

**Purpose**: Signal to the JVM that classes implementing them have some special behavior.

**Built-in marker interfaces**:

**1. Serializable** (java.io.Serializable):
```java
import java.io.Serializable;

class Student implements Serializable {
    String name;
    int age;
}
// Tells JVM this class can be serialized (converted to byte stream)
```

**2. Cloneable** (java.lang.Cloneable):
```java
class Employee implements Cloneable {
    String name;
    
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
// Tells JVM this class can be cloned
```

**3. Remote** (java.rmi.Remote):
```java
interface MyRemote extends Remote {
    // For RMI (Remote Method Invocation)
}
```

**How they work**:
```java
if (obj instanceof Serializable) {
    // Object can be serialized
}
```

**Modern alternative**: Annotations
```java
@Serializable  // More expressive than empty interface
class Student { }
```

**Creating custom marker interface**:
```java
interface Deletable {
    // Empty marker interface
}

class File implements Deletable {
    String name;
}

// Usage
if (file instanceof Deletable) {
    // Allow deletion
}
```

### Q8: Can an interface extend another interface?
**Answer**:
**Yes**, an interface can extend one or more interfaces using the `extends` keyword.

**Single interface extension**:
```java
interface Animal {
    void eat();
}

interface Mammal extends Animal {
    void giveBirth();
}

class Dog implements Mammal {
    public void eat() {
        System.out.println("Dog eats");
    }
    
    public void giveBirth() {
        System.out.println("Dog gives birth");
    }
}
```

**Multiple interface extension**:
```java
interface Movable {
    void move();
}

interface Flyable {
    void fly();
}

// Interface extending multiple interfaces
interface Bird extends Movable, Flyable {
    void chirp();
}

class Sparrow implements Bird {
    public void move() { System.out.println("Moving"); }
    public void fly() { System.out.println("Flying"); }
    public void chirp() { System.out.println("Chirping"); }
}
```

**Key points**:
- Interface extends interface (not implements)
- Class extends class
- Class implements interface
- Can extend multiple interfaces (multiple inheritance)

```java
interface A { }
interface B { }
interface C extends A, B { }  // Valid

class D extends A { }  // Error! A is interface, not class
class E implements A, B { }  // Valid
```

### Q9: What happens if a class implements two interfaces with same method signature?
**Answer**:
If two interfaces have the same method signature (name, parameters, return type), the implementing class needs to provide only one implementation.

**Example**:
```java
interface Interface1 {
    void display();
}

interface Interface2 {
    void display();
}

class MyClass implements Interface1, Interface2 {
    // Single implementation satisfies both interfaces
    public void display() {
        System.out.println("Display method");
    }
}
```

**With different return types** - Compilation Error:
```java
interface A {
    int getValue();
}

interface B {
    double getValue();  // Different return type
}

class C implements A, B {  // Error! Cannot implement both
    // Cannot provide implementation for different return types
}
```

**With default methods** - Must override to resolve conflict:
```java
interface X {
    default void show() {
        System.out.println("X");
    }
}

interface Y {
    default void show() {
        System.out.println("Y");
    }
}

class Z implements X, Y {
    // Must override to resolve ambiguity
    public void show() {
        X.super.show();  // Call X's implementation
        // OR Y.super.show();
        // OR custom implementation
    }
}
```

### Q10: What is the difference between implements and extends keywords?
**Answer**:

**extends**:
- Used for **inheritance**
- Class extends class
- Interface extends interface
- **Single inheritance** for classes
- **Multiple inheritance** for interfaces

```java
// Class extending class
class Animal { }
class Dog extends Animal { }  // Dog inherits from Animal

// Interface extending interface
interface A { }
interface B { }
interface C extends A, B { }  // Multiple inheritance

// Error examples
class X extends Y, Z { }  // Error! Multiple class inheritance not allowed
```

**implements**:
- Used for **interface implementation**
- Class implements interface
- **Multiple implementation** allowed

```java
// Class implementing interface
interface Flyable { }
interface Swimmable { }
class Duck implements Flyable, Swimmable { }  // Multiple implementation

// Error example
interface X implements Y { }  // Error! Interface extends, not implements
```

**Summary**:
```java
class A { }
class B extends A { }           // ✓ Class extends class

interface X { }
interface Y extends X { }       // ✓ Interface extends interface

class C implements X, Y { }     // ✓ Class implements interfaces

interface Z extends X, Y { }    // ✓ Interface extends interfaces

class D extends A implements X, Y { }  // ✓ Both together
```

---

## Practice Exercises

1. Create an interface `Shape` with methods `area()` and `perimeter()`. Implement it in `Circle`, `Rectangle`, and `Triangle` classes.
2. Demonstrate multiple inheritance using interfaces with a class that implements `Readable` and `Writable` interfaces.
3. Create a functional interface `StringOperation` and use it with lambda expressions.
4. Implement a payment system with interface `Payment` and classes `CreditCard`, `PayPal`, and `Bitcoin`.
5. Create an interface with default methods and demonstrate method overriding.

---

## Next Step
Move to **Step 10: Important Java Classes** to learn about essential built-in classes like Object, String, and Wrapper classes.

# Step 8.3: Polymorphism

## What is Polymorphism?

**Polymorphism** means "many forms". It allows objects to take on multiple forms and behave differently based on the context. In Java, polymorphism enables one interface to be used for a general class of actions.

### Key Concepts:
- **Compile-time Polymorphism** (Static/Early Binding): Method Overloading
- **Runtime Polymorphism** (Dynamic/Late Binding): Method Overriding
- **Upcasting**: Parent reference pointing to child object
- **Downcasting**: Converting parent reference back to child type
- **instanceof**: Checking object type at runtime

---

## Types of Polymorphism

### 1. Compile-Time Polymorphism (Method Overloading)

Same method name with different parameters in the same class.

**Rules:**
- Different number of parameters
- Different types of parameters
- Different order of parameters
- Return type alone is NOT sufficient

### 2. Runtime Polymorphism (Method Overriding)

Child class provides specific implementation of a method already defined in parent class.

**Rules:**
- Method signature must be the same
- Child class method cannot be more restrictive
- Use `@Override` annotation (recommended)

---

## Example 1: Method Overloading (Compile-Time Polymorphism)

```java
class Calculator {
    // Method with 2 int parameters
    public int add(int a, int b) {
        return a + b;
    }
    
    // Method with 3 int parameters
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method with 2 double parameters
    public double add(double a, double b) {
        return a + b;
    }
    
    // Method with different order of parameters
    public String add(String a, int b) {
        return a + b;
    }
    
    public String add(int a, String b) {
        return a + b;
    }
}

public class MethodOverloadingExample {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        System.out.println("2 + 3 = " + calc.add(2, 3));              // Calls add(int, int)
        System.out.println("2 + 3 + 4 = " + calc.add(2, 3, 4));       // Calls add(int, int, int)
        System.out.println("2.5 + 3.5 = " + calc.add(2.5, 3.5));      // Calls add(double, double)
        System.out.println("Hello + 5 = " + calc.add("Hello", 5));    // Calls add(String, int)
        System.out.println("10 + World = " + calc.add(10, "World"));  // Calls add(int, String)
    }
}
```

**Output:**
```
2 + 3 = 5
2 + 3 + 4 = 9
2.5 + 3.5 = 6.0
Hello + 5 = Hello5
10 + World = 10World
```

---

## Example 2: Method Overriding (Runtime Polymorphism)

```java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
    
    public void sleep() {
        System.out.println("Animal is sleeping");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks: Woof! Woof!");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow! Meow!");
    }
}

class Cow extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cow moos: Moo! Moo!");
    }
}

public class MethodOverridingExample {
    public static void main(String[] args) {
        // Runtime polymorphism - Parent reference, child object
        Animal myAnimal;
        
        myAnimal = new Dog();
        myAnimal.makeSound();  // Dog's makeSound() is called
        myAnimal.sleep();      // Animal's sleep() is called
        
        myAnimal = new Cat();
        myAnimal.makeSound();  // Cat's makeSound() is called
        
        myAnimal = new Cow();
        myAnimal.makeSound();  // Cow's makeSound() is called
    }
}
```

**Output:**
```
Dog barks: Woof! Woof!
Animal is sleeping
Cat meows: Meow! Meow!
Cow moos: Moo! Moo!
```

---

## Example 3: Upcasting and Downcasting with instanceof

```java
class Vehicle {
    String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public void start() {
        System.out.println(brand + " vehicle is starting");
    }
}

class Car extends Vehicle {
    int numberOfDoors;
    
    public Car(String brand, int doors) {
        super(brand);
        this.numberOfDoors = doors;
    }
    
    @Override
    public void start() {
        System.out.println(brand + " car is starting with " + numberOfDoors + " doors");
    }
    
    public void playMusic() {
        System.out.println("Playing music in the car");
    }
}

class Bike extends Vehicle {
    boolean hasCarrier;
    
    public Bike(String brand, boolean carrier) {
        super(brand);
        this.hasCarrier = carrier;
    }
    
    @Override
    public void start() {
        System.out.println(brand + " bike is starting. Carrier: " + hasCarrier);
    }
    
    public void ringBell() {
        System.out.println("Ring ring!");
    }
}

public class UpcastingDowncastingExample {
    public static void main(String[] args) {
        // Upcasting (Automatic/Implicit)
        Vehicle vehicle1 = new Car("Toyota", 4);  // Car object, Vehicle reference
        Vehicle vehicle2 = new Bike("Honda", true);
        
        vehicle1.start();  // Calls Car's start() - Runtime polymorphism
        vehicle2.start();  // Calls Bike's start()
        
        // vehicle1.playMusic();  // ERROR! Vehicle reference doesn't know about playMusic()
        
        System.out.println("\n--- Downcasting Examples ---");
        
        // Downcasting (Explicit) - Need to check type first
        if (vehicle1 instanceof Car) {
            Car myCar = (Car) vehicle1;  // Downcasting
            myCar.playMusic();
            System.out.println("This car has " + myCar.numberOfDoors + " doors");
        }
        
        if (vehicle2 instanceof Bike) {
            Bike myBike = (Bike) vehicle2;  // Downcasting
            myBike.ringBell();
            System.out.println("Has carrier: " + myBike.hasCarrier);
        }
        
        System.out.println("\n--- instanceof checks ---");
        System.out.println("vehicle1 instanceof Car: " + (vehicle1 instanceof Car));
        System.out.println("vehicle1 instanceof Vehicle: " + (vehicle1 instanceof Vehicle));
        System.out.println("vehicle1 instanceof Bike: " + (vehicle1 instanceof Bike));
        
        // Unsafe downcasting example
        System.out.println("\n--- Unsafe downcasting (will cause exception) ---");
        try {
            Bike wrongCast = (Bike) vehicle1;  // ClassCastException!
        } catch (ClassCastException e) {
            System.out.println("Error: Cannot cast Car to Bike!");
        }
    }
}
```

**Output:**
```
Toyota car is starting with 4 doors
Honda bike is starting. Carrier: true

--- Downcasting Examples ---
Playing music in the car
This car has 4 doors
Ring ring!
Has carrier: true

--- instanceof checks ---
vehicle1 instanceof Car: true
vehicle1 instanceof Vehicle: true
vehicle1 instanceof Bike: false

--- Unsafe downcasting (will cause exception) ---
Error: Cannot cast Car to Bike!
```

---

## Key Points to Remember

✅ **Method Overloading:**
- Same method name, different parameters
- Happens in the same class
- Compile-time polymorphism
- Return type can be different but not sufficient alone

✅ **Method Overriding:**
- Same method signature
- Happens in parent-child relationship
- Runtime polymorphism
- Use `@Override` annotation

✅ **Upcasting:**
- Automatic (implicit)
- Parent reference = new Child()
- Safe operation
- Can only access parent class methods

✅ **Downcasting:**
- Manual (explicit)
- Child reference = (Child) parentReference
- Can be unsafe - use `instanceof` check first
- Allows access to child class methods

✅ **instanceof operator:**
- Checks if object is an instance of a class
- Returns boolean (true/false)
- Always check before downcasting

---

## 2025 Interview Questions

### Basic Level

**Q1: What is polymorphism in Java?**
**A:** Polymorphism means "many forms". It's the ability of an object to take many forms. In Java, we achieve polymorphism through method overloading (compile-time) and method overriding (runtime).

**Q2: What is the difference between method overloading and method overriding?**
**A:**
- **Overloading**: Same method name, different parameters, same class, compile-time
- **Overriding**: Same method signature, parent-child relationship, runtime

**Q3: Can we overload the main method in Java?**
**A:** Yes, we can overload the main method, but JVM will only call `public static void main(String[] args)`. Other overloaded versions won't be called automatically.

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("Original main");
        main(5);
    }
    
    public static void main(int x) {  // Overloaded
        System.out.println("Overloaded main: " + x);
    }
}
```

**Q4: What is the use of the instanceof operator?**
**A:** The `instanceof` operator checks whether an object is an instance of a specific class or implements an interface. It returns true or false and is commonly used before downcasting to avoid ClassCastException.

**Q5: Can we override static methods?**
**A:** No, static methods cannot be overridden. They can be redeclared in the child class (method hiding), but it's not polymorphism. Static methods belong to the class, not the object.

### Intermediate Level

**Q6: What is dynamic method dispatch in Java?**
**A:** Dynamic method dispatch is the mechanism by which a call to an overridden method is resolved at runtime rather than compile-time. It's the basis for runtime polymorphism in Java.

```java
Animal animal = new Dog();  // Reference type: Animal, Object type: Dog
animal.makeSound();  // Calls Dog's makeSound() - decided at runtime
```

**Q7: Can we override private methods?**
**A:** No, private methods cannot be overridden because they are not visible to child classes. If you declare a method with the same name in the child class, it's a new method, not an override.

**Q8: What happens if we change the return type while overriding?**
**A:** From Java 5+, we can change the return type to a covariant type (subtype of the original return type). Changing to an unrelated type will cause a compilation error.

```java
class Parent {
    Object getData() {
        return new Object();
    }
}

class Child extends Parent {
    @Override
    String getData() {  // String is a subtype of Object - Valid (Covariant)
        return "Hello";
    }
}
```

**Q9: What is upcasting and downcasting? Which is safer?**
**A:**
- **Upcasting**: Converting child class reference to parent class reference (automatic, safe)
- **Downcasting**: Converting parent class reference to child class reference (manual, can throw ClassCastException)
- Upcasting is safer as it's always valid. Downcasting should be done after instanceof check.

**Q10: Can we achieve polymorphism without inheritance?**
**A:** Yes, through interfaces. A class can implement multiple interfaces, and we can achieve polymorphism using interface references.

```java
interface Drawable {
    void draw();
}

class Circle implements Drawable {
    public void draw() { System.out.println("Drawing Circle"); }
}

class Rectangle implements Drawable {
    public void draw() { System.out.println("Drawing Rectangle"); }
}

// Polymorphism without inheritance
Drawable d = new Circle();
d.draw();
```

### Advanced Level

**Q11: What is the difference between compile-time binding and runtime binding?**
**A:**
- **Compile-time binding** (static/early binding): Method call resolved at compile time. Used for method overloading, private, static, and final methods.
- **Runtime binding** (dynamic/late binding): Method call resolved at runtime based on object type. Used for method overriding.

**Q12: Can constructor be overloaded and overridden?**
**A:** 
- Constructors can be **overloaded** (same class, different parameters)
- Constructors **cannot be overridden** because they are not inherited
- Child class can call parent constructor using `super()`

**Q13: What is the purpose of the @Override annotation?**
**A:** The `@Override` annotation:
1. Tells the compiler that the method should override a parent class method
2. Generates compile-time error if the method doesn't actually override
3. Improves code readability
4. Helps prevent bugs (e.g., typos in method names)

**Q14: Can we override a method that throws an exception?**
**A:** Yes, but with restrictions:
- Can override without any throws clause
- Can throw same exception
- Can throw subclass of the exception
- Cannot throw broader/checked exceptions

```java
class Parent {
    void method() throws IOException { }
}

class Child extends Parent {
    void method() throws FileNotFoundException { }  // FileNotFoundException is subclass of IOException
    // void method() throws Exception { }  // ERROR! Exception is broader than IOException
}
```

**Q15: Explain the concept of polymorphism in the context of collections.**
**A:** Collections use polymorphism extensively. We can store different types of objects in a collection using parent type reference:

```java
List<Animal> animals = new ArrayList<>();
animals.add(new Dog());
animals.add(new Cat());
animals.add(new Cow());

for (Animal animal : animals) {
    animal.makeSound();  // Calls appropriate overridden method - polymorphism
}
```

**Q16: What will happen if both parent and child class have static methods with the same signature?**
**A:** This is called **method hiding**, not overriding. The method called depends on the reference type, not the object type.

```java
class Parent {
    static void display() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    static void display() {
        System.out.println("Child static method");
    }
}

// Usage
Parent p = new Child();
p.display();  // Output: "Parent static method" (reference type decides)
```

**Q17: Can you have polymorphism with private or final methods?**
**A:** 
- **Private methods**: Cannot participate in polymorphism as they're not visible to child classes
- **Final methods**: Cannot be overridden, so no runtime polymorphism. Can be overloaded.

**Q18: How does polymorphism help in writing maintainable code?**
**A:** Polymorphism enables:
1. **Flexibility**: Write code that works with parent types, automatically works with all child types
2. **Extensibility**: Add new child classes without changing existing code
3. **Loose coupling**: Code depends on abstractions (parent type), not concrete implementations
4. **Code reusability**: Single method can work with multiple types

**Q19: What is the difference between IS-A and HAS-A relationship? How does polymorphism apply?**
**A:**
- **IS-A** (Inheritance): Dog IS-A Animal → Polymorphism applies
- **HAS-A** (Composition): Car HAS-A Engine → Polymorphism doesn't directly apply to relationship, but Engine can be polymorphic

**Q20: In Java 8+, can default methods in interfaces be overridden?**
**A:** Yes, default methods in interfaces can be overridden by implementing classes. The overridden method will be called at runtime (polymorphism).

```java
interface MyInterface {
    default void display() {
        System.out.println("Default method");
    }
}

class MyClass implements MyInterface {
    @Override
    public void display() {
        System.out.println("Overridden default method");
    }
}

MyInterface obj = new MyClass();
obj.display();  // Output: "Overridden default method"
```

---

## Practice Exercises

1. Create a `Shape` hierarchy with `Circle`, `Rectangle`, and `Triangle`. Demonstrate polymorphism with `calculateArea()` method.

2. Create a payment processing system with different payment methods (`CreditCard`, `PayPal`, `Cryptocurrency`) using polymorphism.

3. Build a zoo management system where different animals make different sounds using runtime polymorphism.

4. Implement a calculator class with overloaded methods for different operations and different data types.

5. Create an example demonstrating safe downcasting using `instanceof` operator.

---

**Next Step:** [Step 8.4: Abstraction](../Step-8.4-Abstraction/README.md)

# Step 8.2: Inheritance - Code Reusability in Java

## What is Inheritance?

**Inheritance** is a mechanism where a new class (child/subclass) inherits properties and methods from an existing class (parent/superclass). It allows code reusability and establishes a hierarchical relationship between classes.

### Simple Explanation
Think of inheritance like **family traits** 👨‍👩‍👧‍👦:
- Children inherit characteristics from their parents (eye color, height genes)
- Children can have their own unique features too
- Children can also modify inherited traits

**Real-world analogy:** Vehicle hierarchy
- All vehicles have common features (wheels, engine)
- Cars, Bikes, Trucks inherit these features
- Each adds its own specific features (Car has 4 wheels, Bike has 2)

---

## Key Concepts

### 1. **Terminology**
- **Superclass/Parent class/Base class**: Class being inherited from
- **Subclass/Child class/Derived class**: Class that inherits
- **`extends` keyword**: Used to inherit from a class

### 2. **Syntax**
```java
class Parent {
    // Parent members
}

class Child extends Parent {
    // Child inherits Parent members
    // Child can have additional members
}
```

### 3. **`super` Keyword**
- Refers to the parent class
- Used to access parent class methods and constructors
- `super()` calls parent constructor

### 4. **Method Overriding**
- Child class provides specific implementation of parent method
- Same method signature as parent
- `@Override` annotation (recommended)

### 5. **`final` Keyword**
- **`final` class**: Cannot be inherited
- **`final` method**: Cannot be overridden
- **`final` variable**: Constant, cannot be changed

### 6. **Types of Inheritance in Java**
- ✅ **Single Inheritance**: One parent, one child
- ✅ **Multilevel Inheritance**: Chain of inheritance (A → B → C)
- ✅ **Hierarchical Inheritance**: One parent, multiple children
- ❌ **Multiple Inheritance**: NOT supported (one class cannot extend multiple classes)
- ❌ **Hybrid Inheritance**: NOT supported directly (can be achieved with interfaces)

---

## Examples

### Example 1: Basic Inheritance

```java
// Parent class (Superclass)
class Animal {
    String name;
    int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " is eating...");
    }
    
    public void sleep() {
        System.out.println(name + " is sleeping...");
    }
    
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

// Child class (Subclass)
class Dog extends Animal {
    String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age); // Call parent constructor
        this.breed = breed;
    }
    
    // Dog-specific method
    public void bark() {
        System.out.println(name + " is barking: Woof! Woof!");
    }
    
    // Overriding parent method
    @Override
    public void displayInfo() {
        super.displayInfo(); // Call parent's displayInfo
        System.out.println("Breed: " + breed);
    }
}

// Another child class
class Cat extends Animal {
    String color;
    
    public Cat(String name, int age, String color) {
        super(name, age);
        this.color = color;
    }
    
    // Cat-specific method
    public void meow() {
        System.out.println(name + " is meowing: Meow! Meow!");
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Color: " + color);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy", 3, "Golden Retriever");
        dog.displayInfo();
        dog.eat();    // Inherited from Animal
        dog.sleep();  // Inherited from Animal
        dog.bark();   // Dog's own method
        
        System.out.println("\n-------------------\n");
        
        Cat cat = new Cat("Whiskers", 2, "White");
        cat.displayInfo();
        cat.eat();    // Inherited from Animal
        cat.meow();   // Cat's own method
    }
}
```

**Output:**
```
Name: Buddy
Age: 3
Breed: Golden Retriever
Buddy is eating...
Buddy is sleeping...
Buddy is barking: Woof! Woof!

-------------------

Name: Whiskers
Age: 2
Color: White
Whiskers is eating...
Whiskers is meowing: Meow! Meow!
```

---

### Example 2: Method Overriding and `super` Keyword

```java
class BankAccount {
    protected String accountNumber;
    protected double balance;
    
    public BankAccount(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Insufficient balance!");
        }
    }
    
    public void displayBalance() {
        System.out.println("Account: " + accountNumber + ", Balance: $" + balance);
    }
}

class SavingsAccount extends BankAccount {
    private double interestRate;
    
    public SavingsAccount(String accountNumber, double balance, double interestRate) {
        super(accountNumber, balance); // Call parent constructor
        this.interestRate = interestRate;
    }
    
    public void addInterest() {
        double interest = balance * interestRate / 100;
        balance += interest;
        System.out.println("Interest added: $" + interest);
    }
    
    // Overriding withdraw method with additional restriction
    @Override
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance - 1000) {
            // Savings account must maintain minimum balance of $1000
            balance -= amount;
            System.out.println("Withdrawn: $" + amount + " (Minimum balance maintained)");
        } else {
            System.out.println("Cannot withdraw! Must maintain minimum balance of $1000");
        }
    }
    
    @Override
    public void displayBalance() {
        super.displayBalance(); // Call parent's method
        System.out.println("Interest Rate: " + interestRate + "%");
    }
}

class CurrentAccount extends BankAccount {
    private double overdraftLimit;
    
    public CurrentAccount(String accountNumber, double balance, double overdraftLimit) {
        super(accountNumber, balance);
        this.overdraftLimit = overdraftLimit;
    }
    
    // Overriding withdraw to allow overdraft
    @Override
    public void withdraw(double amount) {
        if (amount > 0 && amount <= (balance + overdraftLimit)) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
            if (balance < 0) {
                System.out.println("Warning: Using overdraft! Balance: $" + balance);
            }
        } else {
            System.out.println("Exceeds overdraft limit!");
        }
    }
    
    @Override
    public void displayBalance() {
        super.displayBalance();
        System.out.println("Overdraft Limit: $" + overdraftLimit);
    }
}

public class Main {
    public static void main(String[] args) {
        SavingsAccount savings = new SavingsAccount("SA001", 5000, 5.0);
        savings.displayBalance();
        savings.deposit(1000);
        savings.addInterest();
        savings.withdraw(2000); // Will maintain $1000 minimum
        savings.displayBalance();
        
        System.out.println("\n-------------------\n");
        
        CurrentAccount current = new CurrentAccount("CA001", 3000, 2000);
        current.displayBalance();
        current.withdraw(4000); // Using overdraft
        current.displayBalance();
    }
}
```

**Output:**
```
Account: SA001, Balance: $5000.0
Interest Rate: 5.0%
Deposited: $1000.0
Interest added: $300.0
Withdrawn: $2000.0 (Minimum balance maintained)
Account: SA001, Balance: $4300.0
Interest Rate: 5.0%

-------------------

Account: CA001, Balance: $3000.0
Overdraft Limit: $2000.0
Withdrawn: $4000.0
Warning: Using overdraft! Balance: $-1000.0
Account: CA001, Balance: $-1000.0
Overdraft Limit: $2000.0
```

---

### Example 3: Multilevel Inheritance and `final` Keyword

```java
// Level 1: Base class
class Vehicle {
    protected String brand;
    protected int year;
    
    public Vehicle(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }
    
    public void displayInfo() {
        System.out.println("Brand: " + brand);
        System.out.println("Year: " + year);
    }
    
    // final method - cannot be overridden
    public final void startEngine() {
        System.out.println("Engine started with ignition system");
    }
}

// Level 2: Intermediate class
class Car extends Vehicle {
    protected int numberOfDoors;
    
    public Car(String brand, int year, int numberOfDoors) {
        super(brand, year);
        this.numberOfDoors = numberOfDoors;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Number of Doors: " + numberOfDoors);
    }
    
    public void honk() {
        System.out.println("Car horn: Beep! Beep!");
    }
    
    // Cannot override startEngine() - it's final in Vehicle
    // @Override
    // public void startEngine() { } // ERROR!
}

// Level 3: Most derived class
class ElectricCar extends Car {
    private int batteryCapacity;
    
    public ElectricCar(String brand, int year, int numberOfDoors, int batteryCapacity) {
        super(brand, year, numberOfDoors);
        this.batteryCapacity = batteryCapacity;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Battery Capacity: " + batteryCapacity + " kWh");
    }
    
    public void charge() {
        System.out.println("Charging electric car...");
    }
}

// final class - cannot be extended
final class SportsCar extends Car {
    private int topSpeed;
    
    public SportsCar(String brand, int year, int numberOfDoors, int topSpeed) {
        super(brand, year, numberOfDoors);
        this.topSpeed = topSpeed;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Top Speed: " + topSpeed + " km/h");
    }
}

// This would cause ERROR - SportsCar is final
// class SuperSportsCar extends SportsCar { }

public class Main {
    public static void main(String[] args) {
        ElectricCar tesla = new ElectricCar("Tesla", 2024, 4, 100);
        tesla.displayInfo();
        tesla.startEngine(); // Inherited from Vehicle (final method)
        tesla.honk();        // Inherited from Car
        tesla.charge();      // ElectricCar's own method
        
        System.out.println("\n-------------------\n");
        
        SportsCar ferrari = new SportsCar("Ferrari", 2024, 2, 350);
        ferrari.displayInfo();
        ferrari.startEngine();
        ferrari.honk();
    }
}
```

**Output:**
```
Brand: Tesla
Year: 2024
Number of Doors: 4
Battery Capacity: 100 kWh
Engine started with ignition system
Car horn: Beep! Beep!
Charging electric car...

-------------------

Brand: Ferrari
Year: 2024
Number of Doors: 2
Top Speed: 350 km/h
Engine started with ignition system
Car horn: Beep! Beep!
```

---

## Interview Questions (2025)

### Question 1: What is inheritance and what are its advantages?

**Answer:**
Inheritance is a mechanism where a class (child/subclass) acquires properties and methods from another class (parent/superclass).

**Advantages:**

1. **Code Reusability**: Write code once, use in multiple classes
2. **Method Overriding**: Provide specific implementation in child class
3. **Extensibility**: Add new features without modifying existing code
4. **Polymorphism**: Achieve runtime polymorphism
5. **Maintainability**: Changes in parent reflect in all children
6. **Hierarchical Classification**: Organize classes in a logical hierarchy

**Example:**
```java
class Employee {
    String name;
    double salary;
    
    void work() {
        System.out.println("Employee is working");
    }
}

class Developer extends Employee {
    @Override
    void work() {
        System.out.println("Developer is coding");
    }
}

class Manager extends Employee {
    @Override
    void work() {
        System.out.println("Manager is managing team");
    }
}
```

---

### Question 2: Why doesn't Java support multiple inheritance? How can we achieve it?

**Answer:**
Java doesn't support multiple inheritance of classes to avoid the **Diamond Problem** - ambiguity when two parent classes have the same method.

**Diamond Problem Example:**
```
    ClassA
    /    \
ClassB  ClassC
    \    /
    ClassD
```

If both ClassB and ClassC have a method `display()`, which one should ClassD inherit?

**Why Java doesn't allow:**
```java
// This is INVALID in Java
class ClassD extends ClassB, ClassC { } // ERROR!
```

**How to achieve multiple inheritance in Java:**

**1. Using Interfaces (Recommended):**
```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// A class can implement multiple interfaces
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
```

**2. Default Methods in Interfaces (Java 8+):**
```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle started");
    }
}

interface Electric {
    default void charge() {
        System.out.println("Charging...");
    }
}

class ElectricCar implements Vehicle, Electric {
    // Inherits both default methods
}

// Usage:
ElectricCar car = new ElectricCar();
car.start();   // From Vehicle
car.charge();  // From Electric
```

**3. If both interfaces have same method:**
```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B {
    default void show() {
        System.out.println("B's show");
    }
}

class C implements A, B {
    // Must override to resolve conflict
    @Override
    public void show() {
        A.super.show(); // Can call specific interface's method
        B.super.show();
    }
}
```

---

### Question 3: What is method overriding? What are the rules for overriding?

**Answer:**
Method overriding occurs when a subclass provides a specific implementation of a method already defined in its superclass.

**Rules for Method Overriding:**

1. **Same signature**: Method name, parameters, return type must be same
2. **Access modifier**: Cannot be more restrictive
   - Parent: public → Child: public ✅
   - Parent: public → Child: private ❌
3. **Return type**: Must be same or covariant (subtype)
4. **Exceptions**: Can throw fewer or narrower exceptions (not broader)
5. **`final` methods**: Cannot be overridden
6. **`static` methods**: Cannot be overridden (method hiding instead)
7. **`private` methods**: Cannot be overridden (not inherited)

**Example demonstrating rules:**
```java
class Parent {
    // public method
    public Number getValue() throws IOException {
        return 10;
    }
    
    public final void finalMethod() {
        System.out.println("Cannot override");
    }
    
    private void privateMethod() {
        System.out.println("Not inherited");
    }
}

class Child extends Parent {
    // ✅ Valid: Covariant return type (Integer is subtype of Number)
    @Override
    public Integer getValue() throws FileNotFoundException {
        return 20; // FileNotFoundException is subtype of IOException
    }
    
    // ❌ ERROR: Cannot override final method
    // @Override
    // public void finalMethod() { }
    
    // ❌ ERROR: Cannot reduce visibility
    // @Override
    // protected Number getValue() { return 10; }
    
    // This is NOT overriding - just a new method in Child
    private void privateMethod() {
        System.out.println("Child's private method");
    }
}
```

**Access Modifier Rules:**
```
private < default < protected < public

Overriding progression (allowed):
private → default → protected → public ✅
public → protected → default → private ❌
```

---

### Question 4: Explain the difference between `super` and `this` keywords.

**Answer:**

| Feature | `this` | `super` |
|---------|--------|---------|
| **Refers to** | Current class object | Parent class object |
| **Constructor call** | `this()` - current class constructor | `super()` - parent class constructor |
| **Variable access** | Current class variable | Parent class variable |
| **Method call** | Current class method | Parent class method |
| **Usage** | Differentiate instance var from parameter | Access parent members |

**Example:**
```java
class Parent {
    String name = "Parent";
    
    public Parent() {
        System.out.println("Parent constructor");
    }
    
    public void display() {
        System.out.println("Parent display");
    }
}

class Child extends Parent {
    String name = "Child";
    
    public Child() {
        super(); // Calls Parent's constructor (must be first line)
        System.out.println("Child constructor");
    }
    
    public Child(String name) {
        this(); // Calls Child's no-arg constructor
        this.name = name; // this.name = instance var, name = parameter
    }
    
    @Override
    public void display() {
        System.out.println("this.name: " + this.name);     // Child
        System.out.println("super.name: " + super.name);   // Parent
        super.display(); // Calls Parent's display()
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child("Custom Child");
        child.display();
    }
}
```

**Output:**
```
Parent constructor
Child constructor
this.name: Custom Child
super.name: Parent
Parent display
```

**Key Points:**
- `super()` must be the first statement in constructor
- Can use either `this()` or `super()`, not both
- `super` gives access to hidden parent members

---

### Question 5: What is the difference between method overriding and method hiding (static methods)?

**Answer:**
**Method Overriding** applies to instance methods, while **Method Hiding** applies to static methods.

**Method Overriding (Instance Methods):**
- Runtime polymorphism
- Decision made at runtime based on object type
- Uses `@Override` annotation

**Method Hiding (Static Methods):**
- Compile-time resolution
- Decision made at compile-time based on reference type
- Cannot use `@Override` annotation

**Example:**
```java
class Parent {
    // Instance method
    public void instanceMethod() {
        System.out.println("Parent instance method");
    }
    
    // Static method
    public static void staticMethod() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    // Overriding instance method
    @Override
    public void instanceMethod() {
        System.out.println("Child instance method");
    }
    
    // Hiding static method (NOT overriding!)
    public static void staticMethod() {
        System.out.println("Child static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p1 = new Parent();
        Parent p2 = new Child(); // Upcasting
        Child c = new Child();
        
        // Instance method - Runtime polymorphism (method overriding)
        p1.instanceMethod(); // Parent instance method
        p2.instanceMethod(); // Child instance method (runtime decision)
        c.instanceMethod();  // Child instance method
        
        System.out.println();
        
        // Static method - Compile-time resolution (method hiding)
        p1.staticMethod(); // Parent static method
        p2.staticMethod(); // Parent static method (reference type!)
        c.staticMethod();  // Child static method
        
        // Better to call static methods using class name
        Parent.staticMethod(); // Parent static method
        Child.staticMethod();  // Child static method
    }
}
```

**Output:**
```
Parent instance method
Child instance method
Child instance method

Parent static method
Parent static method
Child static method
Parent static method
Child static method
```

**Key Difference:**
```java
Parent p = new Child();
p.instanceMethod(); // Calls Child's version (overriding - runtime)
p.staticMethod();   // Calls Parent's version (hiding - compile-time)
```

**Best Practice:** Always call static methods using the class name to avoid confusion.

---

## Practice Exercises

1. Create a `Shape` hierarchy (Circle, Rectangle, Triangle) with method overriding for `calculateArea()`
2. Build a `Vehicle` system (Car, Bike, Truck) demonstrating multilevel inheritance
3. Implement `Employee` hierarchy (Manager, Developer, Intern) with different salary calculations
4. Create a `BankAccount` system with SavingsAccount and CurrentAccount having different withdrawal rules
5. Design a `Person` → `Student` → `GraduateStudent` multilevel inheritance with proper constructor chaining

---

## Key Takeaways

✅ Inheritance promotes code reusability and extensibility  
✅ Use `extends` keyword for inheritance  
✅ `super` refers to parent class, `this` refers to current class  
✅ Method overriding allows specific implementation in child class  
✅ Java supports single and multilevel inheritance, not multiple  
✅ `final` class cannot be inherited, `final` method cannot be overridden  
✅ Multiple inheritance can be achieved using interfaces  
✅ Static methods are hidden, not overridden  
✅ Access modifiers can be made more accessible, not more restrictive  

**Next Step:** Move to [Step 8.3: Polymorphism](../Step-8.3-Polymorphism/) to learn about one interface, multiple implementations!

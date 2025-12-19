# Step 8.4: Abstraction

## What is Abstraction?

**Abstraction** is the process of hiding implementation details and showing only essential features to the user. It focuses on **what an object does** rather than **how it does it**.

### Real-World Example:
- When you drive a car, you use the steering wheel, accelerator, and brakes
- You don't need to know how the engine works internally
- The complex internal mechanism is **abstracted** away

### In Java:
- We achieve abstraction using **Abstract Classes** and **Interfaces**
- Abstract classes allow partial abstraction (0-100%)
- Interfaces provide full abstraction (100%)

---

## Abstract Classes

An **abstract class** is a class that cannot be instantiated and may contain abstract methods (methods without implementation).

### Key Points:
- Declared using `abstract` keyword
- Can have abstract methods (without body) and concrete methods (with body)
- Cannot create objects of abstract class
- Child class must implement all abstract methods (or be abstract itself)
- Can have constructors, static methods, and final methods
- Can have instance variables

### Syntax:
```java
abstract class ClassName {
    // Abstract method (no body)
    abstract returnType methodName();
    
    // Concrete method (with body)
    returnType normalMethod() {
        // implementation
    }
}
```

---

## Example 1: Basic Abstract Class

```java
// Abstract class
abstract class Animal {
    String name;
    
    // Constructor
    public Animal(String name) {
        this.name = name;
    }
    
    // Abstract method - no implementation
    abstract void makeSound();
    
    // Concrete method - has implementation
    public void sleep() {
        System.out.println(name + " is sleeping...");
    }
    
    // Concrete method
    public void eat() {
        System.out.println(name + " is eating...");
    }
}

// Concrete class - must implement abstract methods
class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    void makeSound() {
        System.out.println(name + " says: Woof! Woof!");
    }
}

class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    @Override
    void makeSound() {
        System.out.println(name + " says: Meow! Meow!");
    }
}

class Cow extends Animal {
    public Cow(String name) {
        super(name);
    }
    
    @Override
    void makeSound() {
        System.out.println(name + " says: Moo! Moo!");
    }
}

public class AbstractClassExample {
    public static void main(String[] args) {
        // Animal animal = new Animal("Generic");  // ERROR! Cannot instantiate abstract class
        
        Animal dog = new Dog("Buddy");
        Animal cat = new Cat("Whiskers");
        Animal cow = new Cow("Bessie");
        
        dog.makeSound();  // Woof! Woof!
        dog.eat();        // inherited concrete method
        dog.sleep();      // inherited concrete method
        
        System.out.println();
        
        cat.makeSound();  // Meow! Meow!
        cat.eat();
        
        System.out.println();
        
        cow.makeSound();  // Moo! Moo!
        cow.sleep();
    }
}
```

**Output:**
```
Buddy says: Woof! Woof!
Buddy is eating...
Buddy is sleeping...

Whiskers says: Meow! Meow!
Whiskers is eating...

Bessie says: Moo! Moo!
Bessie is sleeping...
```

---

## Example 2: Banking System with Abstraction

```java
// Abstract class
abstract class BankAccount {
    protected String accountNumber;
    protected String accountHolder;
    protected double balance;
    
    // Constructor
    public BankAccount(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }
    
    // Abstract methods - must be implemented by child classes
    abstract void calculateInterest();
    abstract double getMinimumBalance();
    
    // Concrete methods - common to all accounts
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
            System.out.println("New balance: $" + balance);
        } else {
            System.out.println("Invalid deposit amount!");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && balance - amount >= getMinimumBalance()) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
            System.out.println("New balance: $" + balance);
        } else {
            System.out.println("Insufficient balance or invalid amount!");
        }
    }
    
    public void displayAccountInfo() {
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Account Holder: " + accountHolder);
        System.out.println("Current Balance: $" + balance);
    }
}

// Savings Account
class SavingsAccount extends BankAccount {
    private double interestRate = 4.5; // 4.5% per annum
    
    public SavingsAccount(String accountNumber, String accountHolder, double initialBalance) {
        super(accountNumber, accountHolder, initialBalance);
    }
    
    @Override
    void calculateInterest() {
        double interest = balance * interestRate / 100;
        balance += interest;
        System.out.println("Interest added: $" + interest);
        System.out.println("New balance: $" + balance);
    }
    
    @Override
    double getMinimumBalance() {
        return 1000.0;  // Minimum balance: $1000
    }
}

// Current Account
class CurrentAccount extends BankAccount {
    private double overdraftLimit = 5000.0;
    
    public CurrentAccount(String accountNumber, String accountHolder, double initialBalance) {
        super(accountNumber, accountHolder, initialBalance);
    }
    
    @Override
    void calculateInterest() {
        System.out.println("No interest for current accounts");
    }
    
    @Override
    double getMinimumBalance() {
        return -overdraftLimit;  // Can go negative up to overdraft limit
    }
    
    public void displayOverdraftLimit() {
        System.out.println("Overdraft Limit: $" + overdraftLimit);
    }
}

// Fixed Deposit Account
class FixedDepositAccount extends BankAccount {
    private double interestRate = 7.0; // 7% per annum
    private int tenure; // in years
    
    public FixedDepositAccount(String accountNumber, String accountHolder, 
                                double initialBalance, int tenure) {
        super(accountNumber, accountHolder, initialBalance);
        this.tenure = tenure;
    }
    
    @Override
    void calculateInterest() {
        double interest = balance * interestRate * tenure / 100;
        System.out.println("Interest for " + tenure + " years: $" + interest);
        System.out.println("Maturity amount: $" + (balance + interest));
    }
    
    @Override
    double getMinimumBalance() {
        return balance;  // Cannot withdraw from FD
    }
    
    @Override
    public void withdraw(double amount) {
        System.out.println("Cannot withdraw from Fixed Deposit before maturity!");
    }
}

public class BankingSystemExample {
    public static void main(String[] args) {
        System.out.println("=== Savings Account ===");
        SavingsAccount savings = new SavingsAccount("SA001", "John Doe", 5000);
        savings.displayAccountInfo();
        savings.deposit(2000);
        savings.calculateInterest();
        savings.withdraw(500);
        
        System.out.println("\n=== Current Account ===");
        CurrentAccount current = new CurrentAccount("CA001", "Jane Smith", 10000);
        current.displayAccountInfo();
        current.displayOverdraftLimit();
        current.withdraw(3000);
        current.calculateInterest();
        
        System.out.println("\n=== Fixed Deposit Account ===");
        FixedDepositAccount fd = new FixedDepositAccount("FD001", "Bob Johnson", 50000, 5);
        fd.displayAccountInfo();
        fd.calculateInterest();
        fd.withdraw(1000);  // Not allowed
    }
}
```

**Output:**
```
=== Savings Account ===
Account Number: SA001
Account Holder: John Doe
Current Balance: $5000.0
Deposited: $2000.0
New balance: $7000.0
Interest added: $315.0
New balance: $7315.0
Withdrawn: $500.0
New balance: $6815.0

=== Current Account ===
Account Number: CA001
Account Holder: Jane Smith
Current Balance: $10000.0
Overdraft Limit: $5000.0
Withdrawn: $3000.0
New balance: $7000.0
No interest for current accounts

=== Fixed Deposit Account ===
Account Number: FD001
Account Holder: Bob Johnson
Current Balance: $50000.0
Interest for 5 years: $17500.0
Maturity amount: $67500.0
Cannot withdraw from Fixed Deposit before maturity!
```

---

## Example 3: Shape Hierarchy with Abstraction

```java
// Abstract class
abstract class Shape {
    protected String color;
    
    public Shape(String color) {
        this.color = color;
    }
    
    // Abstract methods
    abstract double calculateArea();
    abstract double calculatePerimeter();
    
    // Concrete method
    public void displayColor() {
        System.out.println("Color: " + color);
    }
    
    public void displayInfo() {
        displayColor();
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    
    @Override
    double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;
    
    public Rectangle(String color, double length, double width) {
        super(color);
        this.length = length;
        this.width = width;
    }
    
    @Override
    double calculateArea() {
        return length * width;
    }
    
    @Override
    double calculatePerimeter() {
        return 2 * (length + width);
    }
}

class Triangle extends Shape {
    private double side1, side2, side3;
    
    public Triangle(String color, double side1, double side2, double side3) {
        super(color);
        this.side1 = side1;
        this.side2 = side2;
        this.side3 = side3;
    }
    
    @Override
    double calculateArea() {
        // Using Heron's formula
        double s = (side1 + side2 + side3) / 2;
        return Math.sqrt(s * (s - side1) * (s - side2) * (s - side3));
    }
    
    @Override
    double calculatePerimeter() {
        return side1 + side2 + side3;
    }
}

public class ShapeExample {
    public static void main(String[] args) {
        Shape circle = new Circle("Red", 5.0);
        Shape rectangle = new Rectangle("Blue", 4.0, 6.0);
        Shape triangle = new Triangle("Green", 3.0, 4.0, 5.0);
        
        System.out.println("=== Circle ===");
        circle.displayInfo();
        
        System.out.println("\n=== Rectangle ===");
        rectangle.displayInfo();
        
        System.out.println("\n=== Triangle ===");
        triangle.displayInfo();
        
        // Polymorphism with abstraction
        System.out.println("\n=== Using Polymorphism ===");
        Shape[] shapes = {circle, rectangle, triangle};
        
        double totalArea = 0;
        for (Shape shape : shapes) {
            totalArea += shape.calculateArea();
        }
        System.out.println("Total area of all shapes: " + totalArea);
    }
}
```

---

## When to Use Abstract Classes?

✅ **Use Abstract Classes When:**
1. You want to share code among related classes
2. Classes extending abstract class have many common methods/fields
3. You want to declare non-static, non-final fields
4. You need constructors
5. You want to provide default implementation for some methods

❌ **Don't Use Abstract Classes When:**
1. You need multiple inheritance (use interfaces instead)
2. You want to define only method signatures without any implementation
3. Unrelated classes need to implement the same behavior

---

## Abstract Class vs Concrete Class vs Interface

| Feature | Abstract Class | Concrete Class | Interface |
|---------|---------------|----------------|-----------|
| Instantiation | Cannot create objects | Can create objects | Cannot create objects |
| Abstract methods | Can have (0 or more) | Cannot have | All methods abstract (before Java 8) |
| Concrete methods | Can have | Can have | Can have (default/static in Java 8+) |
| Variables | All types | All types | Only public static final |
| Multiple inheritance | No | No | Yes |
| Constructor | Yes | Yes | No |
| Access modifiers | All | All | public only (for methods) |

---

## 2025 Interview Questions

### Basic Level

**Q1: What is abstraction in Java?**
**A:** Abstraction is hiding implementation details and showing only essential features. It focuses on "what" rather than "how". We achieve abstraction using abstract classes and interfaces.

**Q2: What is an abstract class?**
**A:** An abstract class is a class declared with the `abstract` keyword that cannot be instantiated. It can have both abstract methods (without implementation) and concrete methods (with implementation).

**Q3: Can we create an object of an abstract class?**
**A:** No, we cannot create objects of an abstract class. However, we can create reference variables of abstract class type that point to objects of concrete child classes.

```java
abstract class Animal { }
class Dog extends Animal { }

// Animal a = new Animal();  // ERROR!
Animal a = new Dog();  // Correct
```

**Q4: Can an abstract class have a constructor?**
**A:** Yes, abstract classes can have constructors. They are called when an object of a child class is created using `super()`.

**Q5: Do we need to implement all abstract methods in the child class?**
**A:** Yes, a concrete child class must implement all abstract methods from the parent abstract class. If it doesn't, the child class must also be declared abstract.

### Intermediate Level

**Q6: Can an abstract class have final methods?**
**A:** Yes, abstract classes can have final methods. Final methods cannot be overridden by child classes.

**Q7: Can an abstract class be final?**
**A:** No, an abstract class cannot be final. Final means it cannot be extended, but abstract classes are meant to be extended. These two keywords are contradictory.

**Q8: Can we have an abstract class without any abstract methods?**
**A:** Yes, we can declare a class as abstract even if it has no abstract methods. This is useful when we want to prevent direct instantiation of the class.

```java
abstract class Vehicle {
    void start() {
        System.out.println("Vehicle started");
    }
}
```

**Q9: Can abstract methods be static?**
**A:** No, abstract methods cannot be static. Static methods belong to the class and cannot be overridden, while abstract methods must be implemented by child classes.

**Q10: What is the difference between abstraction and encapsulation?**
**A:**
- **Abstraction**: Hiding implementation details (focuses on what to do)
- **Encapsulation**: Hiding data using access modifiers (focuses on data security)

### Advanced Level

**Q11: Can we have an abstract class inside another abstract class?**
**A:** Yes, we can have nested abstract classes.

```java
abstract class Outer {
    abstract class Inner {
        abstract void display();
    }
}
```

**Q12: What happens if a child class doesn't implement an abstract method?**
**A:** The child class must be declared abstract. The implementation responsibility passes to the next concrete child class.

```java
abstract class A {
    abstract void method1();
}

abstract class B extends A {
    // Doesn't implement method1()
    // So B must also be abstract
}

class C extends B {
    void method1() {
        // C must implement method1()
    }
}
```

**Q13: Can we use abstract keyword with variables?**
**A:** No, the `abstract` keyword cannot be used with variables, only with classes and methods.

**Q14: When should you use an abstract class vs an interface?**
**A:**

**Use Abstract Class when:**
- Classes share common code
- You need non-public members
- You need non-static/non-final fields
- You want to provide default implementation

**Use Interface when:**
- Multiple inheritance needed
- Unrelated classes implement same behavior
- Define a contract without any implementation (before Java 8)

**Q15: Can an abstract class implement an interface?**
**A:** Yes, an abstract class can implement an interface and may choose not to implement all interface methods. Concrete child classes must implement remaining methods.

```java
interface Flyable {
    void fly();
}

abstract class Bird implements Flyable {
    // May or may not implement fly()
    abstract void eat();
}

class Sparrow extends Bird {
    void fly() {
        System.out.println("Sparrow flies");
    }
    
    void eat() {
        System.out.println("Sparrow eats");
    }
}
```

**Q16: What is the advantage of using abstraction?**
**A:**
1. **Reduces complexity**: Hides unnecessary details
2. **Improves maintainability**: Changes in implementation don't affect users
3. **Increases security**: Internal implementation is hidden
4. **Promotes code reusability**: Common functionality in abstract class
5. **Provides a template**: Defines structure for child classes

**Q17: Can we override a concrete method from an abstract class?**
**A:** Yes, child classes can override concrete methods from abstract classes just like normal inheritance.

**Q18: What is the difference between abstraction and polymorphism?**
**A:**
- **Abstraction**: Hiding implementation complexity (what object does)
- **Polymorphism**: One interface, multiple implementations (how object behaves in different forms)

They often work together but serve different purposes.

**Q19: Can an abstract class extend another abstract class?**
**A:** Yes, an abstract class can extend another abstract class. It may or may not implement the parent's abstract methods.

**Q20: Is it mandatory to use the @Override annotation when implementing abstract methods?**
**A:** No, it's not mandatory but highly recommended. It helps catch errors at compile time and improves code readability.

---

## Key Takeaways

✅ Abstract class provides partial abstraction (0-100%)
✅ Cannot instantiate abstract class directly
✅ Child class must implement all abstract methods (or be abstract)
✅ Can have constructors, static methods, instance variables
✅ Use when you have common code to share among related classes
✅ Cannot be final (contradictory keywords)
✅ Abstract methods cannot be static, final, or private

---

## Practice Exercises

1. Create an abstract class `Employee` with abstract method `calculateSalary()`. Create child classes `FullTimeEmployee`, `PartTimeEmployee`, and `ContractEmployee`.

2. Design a payment system with abstract class `Payment` and concrete classes for `CreditCardPayment`, `DebitCardPayment`, and `UPIPayment`.

3. Create an abstract class `Vehicle` with abstract methods `start()` and `stop()`. Implement concrete classes `Car`, `Bike`, and `Truck`.

4. Build a notification system with abstract class `Notification` and implementations for `EmailNotification`, `SMSNotification`, and `PushNotification`.

5. Create a game character hierarchy with abstract class `GameCharacter` and concrete classes `Warrior`, `Mage`, and `Archer`.

---

**Next Step:** [Phase 3: Step 9 - Interfaces](../../Phase-3-Advanced-OOP-Concepts/Step-9-Interfaces/README.md)

# ⚡ Overloading vs Overriding — Quick Notes

---

## 🔁 Method Overloading

- **Same class**, same method name, **different parameters**
- Decided at **Compile time** → Static binding
- Java picks the right method by counting your arguments

```java
void order(String flavour) { }
void order(String flavour, String size) { }  // same name, different params ✅
```

---

## 🦸 Method Overriding

- **Child class** rewrites a method from the **parent class**
- Same name, **same parameters**, different behaviour
- Decided at **Run time** → Dynamic binding
- Use `@Override` annotation (best practice)

```java
class Animal { void makeSound() { ... } }
class Dog extends Animal {
    @Override
    void makeSound() { System.out.println("Woof! 🐶"); } // rewrites parent ✅
}
```

---

## 🆚 Key Differences

| | Overloading | Overriding |
|---|---|---|
| Class | Same class | Parent → Child |
| Parameters | Different | Same |
| Decided when? | Compile time | Run time |
| Binding | Static | Dynamic |

---

## 🧠 Memory Trick

```
OverLOADing  →  L = Locked at compile time
OverRIDing   →  R = Runtime decides
```

---

## ⏱️ Compile Time vs Run Time — Deep Dive

### Overloading → Compile Time ⚙️

> Java decides **which method to call** while **compiling** — before the program even runs!

```java
p.order("Cheese");           // Java sees 1 argument → picks 1st method
p.order("Cheese", "Large"); // Java sees 2 arguments → picks 2nd method
```

```
You write code
      ↓
javac compiles    ← ✅ Overloading decided HERE
      ↓
java runs
```

---

### Overriding → Run Time 🏃

> Java decides **which method to call** WHILE the program is **actually running!**

```java
Animal myPet;           // Java doesn't know what type yet!

myPet = new Dog();      // known at RUNTIME
myPet.makeSound();      // → Woof! 🐶  decided WHILE running

myPet = new Cat();      // changed at RUNTIME
myPet.makeSound();      // → Meow! 🐱  decided WHILE running
```

```
You write code
      ↓
javac compiles
      ↓
java runs         ← ✅ Overriding decided HERE
      ↓
"it's a Dog → call Dog's makeSound() 🐶"
"it's a Cat → call Cat's makeSound() 🐱"
```

> 💡 Overriding is more **powerful & flexible** — it decides based on the **actual object at runtime!**

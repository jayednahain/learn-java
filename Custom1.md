# ☕ Java Learning Summary

---

## 1. 🏗️ Classes & Objects

- A **class** is a blueprint — it defines variables and methods
- An **object** is a real instance created from the class
- Use `new` keyword to create an object → `Car car1 = new Car()`
- Each object gets its **own copy** of instance variables

---

## 2. 🔨 Constructors

- A constructor runs **automatically** when an object is created
- **Default constructor** → no arguments → sets default values
- **Parameterized constructor** → takes arguments → sets custom values
- `this.brand = brand` → `this` refers to the **current object's** variable

---

## 3. 🚀 The `main` Method

- `main` is the **entry point** — JVM starts execution here
- Signature must be exactly: `public static void main(String[] args)`
- **NOT mandatory** for every class — only the class you run needs it
- Inside `main` (static) → you **must create an object** before using instance variables/methods

---

## 4. 📄 File Name = Class Name Rule

- A `public` class name **must match** the file name exactly
- `Car.java` → `public class Car` ✅
- Only **ONE** `public` class allowed per file
- Other classes in the same file → remove `public` keyword
- Java is **case-sensitive** → `Car` ≠ `car`

---

## 5. ⚡ `static` Keyword

- `static` members belong to the **CLASS** — not to any object
- Created **once**, shared across **ALL** objects
- Can use on: variables, methods, blocks, nested classes
- Inside a `static` method → **cannot** use instance variables directly
- Common uses: utility methods (`Math.abs()`), counters, Singleton pattern

```
static   → whiteboard in classroom  (everyone sees the SAME)
instance → each student's notebook  (everyone has their OWN)
```

---

## 6. 🔒 Access Modifiers

| Modifier | Your Words | Accessible From |
|---|---|---|
| `private` | Class scope | Only inside that class |
| *(none)* | File scope | Same file / same package only |
| `protected` | Family scope | Class + child classes |
| `public` | Global scope | Everywhere |

### `private` vs `protected`:

```
private   → locked to THIS class only
              even child classes CANNOT access it ❌

protected → open to THIS class + child classes + same package
              children CAN access it ✅
```

### Example:

```java
public class BankAccount {
    private double balance;       // class scope  — only BankAccount
    protected String ownerName;   // family scope — child classes too
    public void deposit() { }     // global scope — everyone
}

// In same file:
class Main {
    void test() {
        BankAccount a = new BankAccount();
        a.balance = 100;      // ❌ private  — class scope, blocked!
        a.ownerName = "Ali";  // ✅ protected — same file, allowed!
        a.deposit(100);       // ✅ public    — global, allowed!
    }
}
```

### Rule of Thumb:
- Use `private` by default
- Only upgrade to `protected` when a **child class needs it**
- `protected` is mainly used with **Inheritance** (parent → child)

---

## 7. 🔐 Encapsulation

- **Hiding data** with `private` + **controlling access** with getters/setters
- `private` variable → no one can touch it directly from outside
- **Getter** → safely READ the data → `getBalance()`
- **Setter** → safely CHANGE the data with validation → `deposit(amount)`
- Prevents invalid data from entering your object

```
Encapsulation = private variable + getter + setter
```

---

## 8. 🏦 `BankAccount` Example — Concepts Applied

```java
public class BankAccount {
    private double balance;        // Encapsulation — data hidden

    public void deposit(double amount) {  // Setter with validation
        if (amount > 0) {
            balance += amount;     // instance variable — each account owns its own
        }
    }

    public double getBalance() {   // Getter — read only access
        return balance;
    }
}

class Main {                       // no 'public' — file is BankAccount.java
    public static void main(String[] args) {   // entry point
        BankAccount myAccount = new BankAccount();  // object created
        myAccount.deposit(50.0);
        System.out.println(myAccount.getBalance());
    }
}
```

---

## 📦 Quick Reference

| Concept | Keyword | Purpose |
|---|---|---|
| Entry point | `main` | JVM starts here |
| Shared data | `static` | One copy for all objects |
| Hide data | `private` | No outside access |
| Open access | `public` | Accessible everywhere |
| Read data | getter | `getBalance()` |
| Write data | setter | `deposit()` |
| Current object | `this` | Refers to own instance |
| Create object | `new` | `new BankAccount()` |

---

> 💡 **Key Takeaway:** Java is all about **organizing** and **protecting** your data
> through classes, objects, access modifiers, and encapsulation! 🎯

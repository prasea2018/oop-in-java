
# **📘Abstract Classes in Java**

### **1️⃣ What is an Abstract Class?**

- A class declared with the `abstract` keyword is called an **abstract class**.

- **Purpose:** Represents a class that is **not completely defined**.

- **Key Rules:**

  1. **Cannot create objects** of an abstract class.

     ```java
     abstract class Super { }
     Super s = new Super(); // ❌ Not allowed
     ```

  2. Can have a **constructor**, fields, and methods (both abstract and concrete).
  3. A class **may have zero or more abstract methods**.
  4. If a class has **at least one abstract method**, it **must** be declared abstract.

- **Difference from Concrete Class:**

  | Feature             | Abstract Class  | Concrete Class      |
  | ------------------- | --------------- | ------------------- |
  | Object Creation     | ❌ Not allowed  | ✅ Allowed          |
  | Abstract Methods    | ✅ Can have     | ❌ Cannot have      |
  | Complete Definition | ❌ Not required | ✅ Must be complete |

---

### **2️⃣ What is an Abstract Method?**

- Declared using `abstract` keyword.
- **No method body** (only a semicolon at the end).
- Must be **overridden in subclasses** to make them concrete.

```java
abstract class Super {
  Super() {
    System.out.println("Super");
  }
  abstract void display(); // abstract method
  void show() {           // concrete method
    System.out.println("Show method");
  }
}
```

---

### **3️⃣ Rules for Subclasses**

- **Subclass of an abstract class:**

  1. **If concrete**, must **override all abstract methods** of the superclass.
  2. **If not overriding**, subclass must be declared `abstract`.

- Only a **concrete subclass** can be instantiated.

```java
abstract class Super {
  Super() {
    System.out.println("Super");
  }
  abstract void display(); 
  void show() {           
    System.out.println("Show method");
  }
}

class Sub extends Super {
  @Override
  void display() {
    System.out.println("Sub display");
  }
}

public class Main {
  public static void main(String[] args) {
    Sub s = new Sub(); // ✅ Allowed
    s.display();
  }
}
```

✅ **Key Idea:** Abstract class provides a **template**; concrete subclass provides **implementation**.

---

### **4️⃣ Philosophy / Real-life Analogy**

- Abstract classes define **“what should be done”**, not **“how it should be done”**.
- Example:

  - `Vehicle` is abstract → defines abstract method `startEngine()`.
  - `Car` and `Bike` are concrete subclasses → implement `startEngine()` differently.

- Benefits:

  1. Forces subclasses to provide implementation.
  2. Allows **polymorphism**:

     ```java
     Vehicle v = new Car();
     v.startEngine(); // Calls Car's implementation
     ```

---

### **5️⃣ Summary**

1. Abstract classes = partially defined classes.
2. Abstract methods = methods without a body, to be defined in subclasses.
3. Cannot create objects of abstract classes.
4. Concrete subclasses must implement all abstract methods to be instantiable.
5. Useful for **designing templates and enforcing rules** in OOP.

---

# **Practising Abstract Class**

After studying this part, you will be able to:

1. Recognize how abstract and concrete classes behave during compilation and runtime
2. Understand how Java enforces rules about instantiation and abstract method implementation
3. Trace object creation and method calling in an inheritance hierarchy
4. Observe how overriding works for abstract methods
5. Correctly interpret compiler errors related to abstract classes
6. Understand why abstract classes are used, through a practical example

---

# **Key Concepts Covered**

* Abstract classes **cannot be instantiated**
* Abstract methods **must** be implemented by subclasses
* A subclass becomes **concrete** only after overriding all abstract methods
* You can use a **superclass reference** to refer to a subclass object
* Constructor chaining occurs: superclass constructor runs first
* Abstract classes are primarily used **for inheritance and polymorphism**

---

# **Detailed Breakdown (Step-by-Step Explanation)**

## **1. Starting with a Concrete Class**

Instructor begins with:

```java
class Super {
  Super() {
      System.out.println("Super class constructor");
  }

  void method1() {
    System.out.println("Method1 of Super");
  }
}
```

Since all methods are defined:

* The class is **concrete**
* You *can* create an object:

```java
Super s = new Super();
s.method1();
```

Output:

```
Super class constructor
Method1 of Super
```

---

## **2. Turning the Class into an Abstract Class**

Instructor adds:

```java
abstract class Super { ... }
```

Immediately, IDE shows an error:

> **Cannot instantiate type Super**

Because:

* Abstract classes **cannot have objects**

So this is illegal:

```java
Super s = new Super(); // ERROR
```

---

## **3. Adding an Abstract Method**

Inside the class:

```java
public abstract void method2();
```

The IDE shows a warning:

> Missing method body: either give a body or declare abstract.

Because a method without a body **must** be marked abstract.

Now the class has:

* A normal method (`method1`)
* An abstract method (`method2`)
* Therefore, Java requires the **class to be abstract**

So this is correct:

```java
abstract class Super {
  public Super() { System.out.println("Super constructor"); }
  void method1() { ... }
  abstract void method2();
}
```

---

## **4. Abstract Classes Need Subclasses**

Since `Super` is incomplete (because of `method2()`), a subclass must implement the missing behavior.

```java
class Sub extends Super {
  @Override
  public void method2() {
    System.out.println("Method2 of Subclass");
  }
}
```

If you do NOT override method2, Java gives:

> `Sub is not abstract and does not override abstract method method2()`

Meaning:

* Either override it
* Or mark the subclass abstract

---

## **5. Subclass Is a Concrete Class**

After overriding:

```java
class Sub extends Super {
    @Override
    public void method2() {
        System.out.println("Method2 of Subclass");
    }
}
```

The class is now **concrete**, so you can create objects:

```java
Sub obj = new Sub();
```

---

## **6. Using Superclass Reference for Subclass Object**

This is allowed:

```java
Super ref = new Sub();
```

You can call all methods *declared* in Super:

```java
ref.method1();  // concrete in Super
ref.method2();  // overridden in Sub
```

Output sequence:

```
Super class constructor   ? from constructor chaining
Method1 of Super
Method2 of Subclass
```

Explanation:

1. Sub constructor implicitly calls `super()`
2. `method1()` is executed from the superclass
3. `method2()` is dynamically dispatched ? Subclass version runs

---

## **7. Important Runtime Behaviors Demonstrated**

### **A. Constructor Chaining**

When you create:

```java
new Sub()
```

Java automatically executes:

1. Superclass constructor
2. Subclass constructor

This confirms: *superclass constructor always runs first*.

---

### **B. Dynamic Method Dispatch**

Even though the reference type is `Super`:

```java
Super ref = new Sub();
ref.method2();
```

Java determines method implementation **at runtime**, not compile time.

So **subclass method runs**, not the abstract method placeholder.

---

### **C. No Object of Abstract Class**

Abstract class can have:

```java
Super ref;     // allowed
ref = new Sub(); // allowed
ref = new Super(); // NOT allowed
```

---

# **Summary**

* Abstract classes cannot be instantiated
* Abstract methods require subclasses to provide implementations
* A subclass becomes concrete only after overriding all abstract methods
* Abstract classes are used for inheritance and polymorphism
* Superclass references can point to subclass objects
* Actual object type decides which overridden method runs at runtime

---

# **Application Exercises**

1. Modify the example by adding a `method3()` abstract method.

   * What compiler error do you see?
2. Create another subclass (e.g., `Sub2`) and override `method2()` differently.
3. Assign subclass objects to superclass references and call methods.
4. Add constructors to the subclass and observe constructor chaining.

---

# **Self-Assessment Questions**

1. Why can't you create an object of an abstract class?
2. What happens if a subclass does NOT override all abstract methods?
3. What is the purpose of using superclass references?
4. Explain dynamic method dispatch in this context.
5. Why does the superclass constructor run before the subclass constructor?

---



# **3. Example#1 Abstract Class**

By the end of this segment, learners will be able to:

1. Understand the **purpose of abstract classes** in programming
2. Relate abstract classes to **real-life standards and templates**
3. Explain why abstract classes **cannot be instantiated**
4. Use subclassing to **implement abstract methods**
5. Apply abstract class concepts through a **practical, real-world analogy**

---

# **Key Concepts**

### **1. Purpose of Abstract Classes**

Abstract classes are useful for:

* Defining a **template or standard**
* Imposing **rules that subclasses must follow**
* Representing concepts that are **incomplete on their own**

They **cannot be instantiated** because they are just standards, not fully implemented objects.

---

### **2. Real-Life Analogy: Hospitals**

#### Scenario:

* **Government authority** defines the standards for opening a hospital:

  * Emergency services must exist
  * Appointment systems must be in place
  * Other operational procedures must be followed

* The authority itself does **not operate a hospital**; it only provides **standards**.

#### Mapping to Java:

* **Abstract class `Hospital`** ? Represents the authority with guidelines (abstract methods)
* **Concrete subclass `MyHospital`** ? Represents a real hospital that **implements all abstract methods**

```java
abstract class Hospital {
  abstract void emergency();
  abstract void appointment();
}

class MyHospital extends Hospital {
  @Override
  void emergency() {
    System.out.println("Emergency handled at MyHospital");
  }

  @Override
  void appointment() {
    System.out.println("Appointments managed at MyHospital");
  }
}
```

---

### **3. Rules Illustrated**

1. **Cannot create object of abstract class:**

```java
Hospital h = new Hospital(); // ERROR
```

Reason: `Hospital` is abstract � it only defines the template.

2. **Can create object of concrete subclass:**

```java
MyHospital mh = new MyHospital();
```

3. **Can use a superclass reference for subclass object:**

```java
Hospital hRef = new MyHospital();
hRef.emergency();  // Calls MyHospital�s implementation
```

* This demonstrates **polymorphism**: the method called depends on the **actual object**, not the reference type.

---

### **4. Conceptual Takeaways**

* **Abstract classes = templates/standards**
* **Concrete classes = actual implementations that fulfill the standards**
* **Abstract methods = rules that must be followed**
* Subclasses **must implement all abstract methods** to become concrete and useful

**Analogy Recap:**

| Concept              | Real-life Analogy                                   |
| -------------------- | --------------------------------------------------- |
| Abstract class       | Government standards for hospitals                  |
| Abstract method      | Required hospital services (emergency, appointment) |
| Concrete subclass    | Actual hospital implementing the standards          |
| Superclass reference | Referring to a hospital in general terms            |
| Polymorphism         | Calling services based on the actual hospital       |

---

### **5. Summary Points from the Example**

1. Abstract classes **cannot be instantiated**.
2. Abstract classes **define a contract** that subclasses must fulfill.
3. Subclasses **override abstract methods** to become concrete.
4. Superclass references can refer to subclass objects, enabling **flexible and reusable code**.
5. Abstract classes are **conceptually similar to templates or standards in real life**.

---

### **Application Exercise**

1. Define an abstract class `Bank` with abstract methods: `openAccount()` and `loanProcessing()`.
2. Create a concrete class `MyBank` that implements all abstract methods.
3. Instantiate `MyBank` and call methods using both `MyBank` reference and `Bank` reference.
4. Explain how this models **standards vs actual implementation**.

---

### **Self-Assessment Questions**

1. Why are abstract classes like �standards� in the real world?
2. Can you create an object of the `Hospital` abstract class? Why or why not?
3. What happens if `MyHospital` does not implement all abstract methods?
4. How does a superclass reference (`Hospital hRef`) help achieve polymorphism?
5. Give another real-world example where abstract classes could represent a standard.

---


# **3. Example#2 Abstract Class**

By the end of this segment, learners will be able to:

1. Understand abstract classes using a **franchise business analogy**
2. Recognize which methods/classes are **provided by the parent company vs implemented by the franchise**
3. Relate **abstract methods** to tasks that the subclass must implement
4. Understand rules about **object creation and superclass references**
5. Reinforce previous concepts with **practical, real-world examples**

---

# **Key Concepts**

### **1. Abstract Class = Parent Company / Standard Provider**

* Abstract classes **cannot be instantiated**
* They define **standards and templates** for subclasses
* Contain a mix of:

  * **Concrete methods** → provided by the company (e.g., recipes, preparation instructions)
  * **Abstract methods** → tasks the franchise must define (e.g., building design, local offers)

---

### **2. Concrete Subclass = Franchise Outlet**

* Subclass implements **all abstract methods**
* Subclass becomes **concrete**, so objects can be created
* In the analogy:

  * `MyKFC` extends `KFC`
  * Implements abstract methods like `buildOutlet()` and `provideOffers()`
  * Uses concrete methods like `prepareMenuItems()` from the abstract class

```java
abstract class KFC {
  KFC() {
    System.out.println("Standard KFC setup provided");
  }

  void prepareMenuItems() {
    System.out.println("Preparing menu items according to KFC standard");
  }

  abstract void buildOutlet();
  abstract void provideOffers();
}

class MyKFC extends KFC {
  @Override
  void buildOutlet() {
    System.out.println("Building MyKFC outlet according to local choice");
  }

  @Override
  void provideOffers() {
    System.out.println("Providing local offers and discounts");
  }
}
```

---

### **3. Rules Highlighted**

1. **Cannot create object of abstract class**

```java
KFC k = new KFC(); // ERROR
```

2. **Can create object of concrete subclass**

```java
MyKFC myShop = new MyKFC();
```

3. **Must implement all abstract methods**

* If `buildOutlet()` or `provideOffers()` is missing, `MyKFC` becomes abstract → cannot instantiate

4. **Superclass reference can point to subclass object**

```java
KFC kRef = new MyKFC();
kRef.buildOutlet();  // Calls MyKFC implementation
```

5. **Concrete methods from abstract class are inherited**

```java
kRef.prepareMenuItems(); // Uses KFC's recipe
```

---

### **4. Real-Life Analogy Summary**

| Java Concept              | KFC Analogy                                      |
| ------------------------- | ------------------------------------------------ |
| Abstract class `KFC`      | KFC company, defines standard recipes & rules    |
| Concrete methods          | Menu preparation instructions                    |
| Abstract methods          | Tasks franchise must define (building, offers)   |
| Concrete subclass `MyKFC` | Individual franchise outlet implementing tasks   |
| Object creation           | Only franchises can be opened                    |
| Superclass reference      | People see a KFC outlet but don’t know the owner |

---

### **5. Conceptual Takeaways**

* Abstract classes provide **standards**
* Subclasses provide **implementation details**
* Objects **cannot** be created from abstract classes
* Subclass **must override all abstract methods** to become concrete
* Superclass reference allows **polymorphism**
* Analogy reinforces why abstract classes are useful in real-world design

---

### **Application Exercise**

1. Define an abstract class `Restaurant` with:

   * Concrete method: `prepareMenu()`
   * Abstract methods: `buildOutlet()`, `offerDiscounts()`
2. Create a concrete subclass `MyRestaurant` implementing all abstract methods
3. Instantiate `MyRestaurant` and call all methods using:

   * Subclass reference
   * Superclass reference
4. Explain which methods are **fixed standards** and which are **franchise-specific choices**

---

### **Self-Assessment Questions**

1. In the KFC analogy, which methods are abstract and which are concrete? Why?
2. Why can’t we create an object of the `KFC` class?
3. What must a franchise implement before it becomes a usable outlet?
4. How does using a superclass reference help when working with multiple outlets?
5. Can a concrete subclass choose **not to implement an abstract method**? What happens if it doesn’t?

---

# **Do_s and Don_t_s of Abstract Class and Methods**

---

### **1. Abstract Class Rules**

* **Cannot instantiate abstract class**

  ```java
  abstract class Super { }
  Super s = new Super(); // ERROR
  ```

  * **Reason:** Abstract classes are incomplete; only subclasses can be instantiated.

* **Can have a reference of abstract class**

  ```java
  Super sRef; // Allowed
  ```

* **If a class has at least one abstract method, the class must be declared abstract**

```java
abstract class Super {
  abstract void method1();
}
```

---

### **2. Abstract Method Rules**

* **Abstract methods cannot have a body**

```java
abstract void method1(); // Correct
abstract void method2() { } // ERROR
```

* **Abstract methods must be implemented in concrete subclasses**

```java
class Sub extends Super {
  @Override
  void method1() {
    System.out.println("Implemented");
  }
}
```

* **Abstract methods cannot be final**

```java
abstract class Super {
    abstract final void method1(); // ERROR
}
```

  * **Reason:** `final` methods cannot be overridden, but abstract methods must be overridden.

* **Abstract methods cannot be static**

```java
abstract class Super {
    abstract static void method1(); // ERROR
}
```

  * **Reason:** Static methods belong to the class, not to instances, and must have a body.

---

### **3. Abstract Class Restrictions**

* **Cannot be final**

  ```java
  final abstract class Super { } // ERROR
  ```

  * **Reason:** Final classes cannot be extended, but abstract classes are meant for inheritance.

* **Cannot be static (top-level)**

  ```java
  static abstract class Super { } // ERROR
  ```

  * Note: Nested static classes are allowed, but top-level classes cannot be static.

---

### **4. Subclass Rules**

* **Subclass must implement all abstract methods of its superclass**
* If it doesn’t, the subclass **must also be declared abstract**:

  ```java
  abstract class Super {
      abstract void method1();
  }

  class Sub extends Super { 
      // ERROR if method1() is not implemented
  }

  abstract class Sub extends Super { 
      // OK, subclass remains abstract
  }
  ```

---

### **Summary Table**

| Rule                                        | Allowed? | Explanation                                             |
| ------------------------------------------- | -------- | ------------------------------------------------------- |
| Instantiate abstract class                  | ❌        | Abstract classes are incomplete templates               |
| Reference of abstract class                 | ✅        | Can refer to a subclass object                          |
| Class with abstract method must be abstract | ✅        | Required by Java compiler                               |
| Abstract method with body                   | ❌        | Abstract methods cannot have implementation             |
| Abstract method final                       | ❌        | Must be overridden, final prevents overriding           |
| Abstract method static                      | ❌        | Static methods cannot be abstract                       |
| Abstract class final                        | ❌        | Abstract classes are for inheritance; final prevents it |
| Subclass must implement abstract methods    | ✅        | Otherwise subclass must be abstract                     |

---

### **Application Exercise**

1. Create an abstract class `Vehicle` with:

   * Concrete method: `startEngine()`
   * Abstract method: `fuelType()`
2. Try declaring `fuelType()` as `final` or `static` → note compiler errors.
3. Create a concrete subclass `Car` and implement `fuelType()`.
4. Test both subclass reference and superclass reference calling methods.

---

### **Self-Assessment Questions**

1. Why can’t abstract classes be final?
2. Can you declare an abstract method as static? Why not?
3. What happens if a concrete subclass doesn’t implement all abstract methods?
4. How do final and abstract modifiers conflict for methods?
5. Can you have an abstract class with no abstract methods? Give an example.

---



# **Rules for Abstract Classes**

By the end of this segment, learners will be able to:

1. Recall key rules for **abstract classes and methods** in Java
2. Understand **what is allowed and what is not allowed**
3. Apply these rules correctly while designing abstract classes and subclasses
4. Use superclass references effectively and avoid common mistakes

---

# **Key Rules for Abstract Classes and Methods**

### **1. Abstract Class Rules**

* **Abstract classes must use the `abstract` keyword**
* **Cannot instantiate abstract classes**

  ```java
  abstract class Test { }
  Test obj = new Test(); // ❌ ERROR
  ```
* **Can have references of abstract class**

  ```java
  Test ref; // ✅ Allowed
  ```
* **Abstract classes are meant for inheritance** → cannot be `final`

  ```java
  final abstract class Test { } // ❌ ERROR
  ```
* **Abstract classes cannot be static** (for top-level classes)

---

### **2. Abstract Method Rules**

* **Abstract methods must be declared without a body**

  ```java
  abstract void display(); // ✅
  ```
* **Cannot be declared `final`**

  ```java
  abstract final void display(); // ❌ ERROR
  ```

  * Reason: Abstract methods must be overridden; final prevents overriding
* **Cannot be declared `static`**

  ```java
  abstract static void display(); // ❌ ERROR
  ```

  * Reason: Static methods belong to the class and must have a body

---

### **3. Subclass Rules**

* **Subclasses extending an abstract class must implement all abstract methods**

  * Otherwise, the subclass itself becomes abstract

  ```java
  abstract class Test1 {
      abstract void display();
  }

  class Test2 extends Test1 { 
      @Override
      void display() { 
          System.out.println("Implemented"); 
      }
  }
  ```
* **If not overridden**, subclass must be declared abstract:

  ```java
  abstract class Test2 extends Test1 { } // ✅ Allowed
  ```

---

### **4. Summary Table**

| Concept                                  | Allowed? | Explanation                                |
| ---------------------------------------- | -------- | ------------------------------------------ |
| Instantiate abstract class               | ❌        | Objects cannot be created directly         |
| Reference of abstract class              | ✅        | Can hold subclass object                   |
| Abstract class final                     | ❌        | Abstract classes are meant for inheritance |
| Abstract class static                    | ❌        | Top-level classes cannot be static         |
| Abstract method with body                | ❌        | Must be declared without a body            |
| Abstract method final                    | ❌        | Cannot override if final                   |
| Abstract method static                   | ❌        | Static methods must have a body            |
| Subclass overriding abstract methods     | ✅        | Must implement to be concrete              |
| Subclass not overriding abstract methods | ✅        | Must declare subclass abstract             |

---

### **Tips for Remembering Rules**

1. Abstract = incomplete → meant for subclassing
2. Final = cannot change → conflicts with abstract’s purpose
3. Static = belongs to class → cannot be abstract
4. Subclasses must **fill in all blanks** from abstract class to become concrete

---

### **Application Exercise**

1. Create an abstract class `School` with:

   * Concrete method: `generalRules()`
   * Abstract methods: `conductExam()`, `organizeEvent()`
2. Create a concrete subclass `MySchool` that implements all abstract methods
3. Attempt to make abstract methods `final` or `static` → observe compiler errors
4. Use a superclass reference to call both concrete and overridden abstract methods

---

### **Self-Assessment Questions**

1. Why cannot an abstract class be final?
2. Can a subclass be concrete if it does not implement all abstract methods?
3. Why cannot abstract methods be final or static?
4. What is the difference between having a reference of abstract class vs creating an object?
5. How do these rules enforce design consistency in Java programs?

---

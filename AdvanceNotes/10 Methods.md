# **📘 Methods in Java**

Methods are member of class which provide functionality for class. 

### **1️⃣ How to Write a Method**

A method in Java has the following components:

```java
modifier returnType methodName(parameters) {
    // method body
}
```

* **Modifier:** `public`, `private`, `static`, etc.
* **Return type:** Type of value the method returns (`int`, `void`, etc.)
* **Method name:** Identifier (e.g., `max`, `increment`)
* **Parameters (optional):** Values passed to the method
* **Method body:** Code to execute

---

### **2️⃣ Example: Finding Maximum of Two Numbers**

```java
class MethodPractice {

    static int max(int x, int y) {    // static method
        if(x > y)
            return x;
        else
            return y;
    }

    public static void main(String[] args) {
        int a = 10, b = 15;
        int result = max(a, b);      // Calling static method
        System.out.println(result);  // Output: 15
    }
}
```

---

### **3️⃣ Static vs Non-Static Methods**

* **Static method:** Can be called directly from `main` without creating an object.

  ```java
  int result = max(a, b);
  ```
* **Non-static method:** Must be called via an object of the class.

  ```java
  MethodPractice mp = new MethodPractice();
  int result = mp.max(a, b);
  ```

---

### **4️⃣ Parameters in Methods**

* **Formal parameters:** Variables declared in the method definition (`x` and `y` in `max(x, y)`).

* **Actual parameters:** Values passed during method call (`a` and `b`).

* **Behavior:** Java uses **pass by value**, meaning:

  * Changes to formal parameters **do not affect actual variables**.
  * Example:

    ```java
    static void increment(int x) {
        x++;
        System.out.println("Inside method: " + x); // prints incremented value
    }

    public static void main(String[] args) {
        int a = 10;
        increment(a);                     // prints 11
        System.out.println(a);            // prints 10 (unchanged)
    }
    ```

---

### **5️⃣ Summary of Key Points**

1. Every method must have a **return type**; if nothing is returned, use `void`.
2. Parameters are optional; methods can have zero or more.
3. **Static methods** can be called directly; **non-static methods** require an object.
4. Java is **pass-by-value**: changing formal parameters does not affect actual parameters.

---

# **📌 Passing Objects as Parameters in Java**

### **1️⃣ Key Concept**

* Java **always passes arguments by value**.
* **For primitive types** (int, float, etc.), the value itself is copied.
* **For objects**, the **reference (address) is copied** into formal parameter, not the object itself.
* Result: The method works on the **same object** in the heap, so changes to the object **are reflected outside** the method.

---

### **2️⃣ Example: Modifying an Array Inside a Method**

```java
public class MethodPractice {

    public static void update(int[] arr) {
        arr[0] = 25;  // Modify first element
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 4, 5, 6};
        update(a);                     // Pass array object
        System.out.println(a[0]);      // Output: 25
    }
}
```

**Explanation:**

* `a` holds a reference to the array in the heap.
* `update(a)` copies the reference to the formal parameter `arr`.
* Both `a` and `arr` point to **the same array**.
* Modifying `arr[0]` also changes `a[0]`.

---

### **3️⃣ Difference from Primitive Types**

```java
public static void increment(int x) {
    x++;
}

public static void main(String[] args) {
    int a = 10;
    increment(a);
    System.out.println(a);  // Output: 10 (unchanged)
}
```

* Primitive values are copied; changing them **does not affect the original variable**.

---

# **📌 Returning Objects from Methods**

* Methods can return any type, including **objects**.
* Objects created inside a method are stored in the **heap**, so the caller can use them after the method returns.

---

### **4️⃣ Example: Returning a String Object**

```java
public class MethodPractice {

    public static String getUsername(String email) {
        int index = email.indexOf('@');
        return email.substring(0, index);  // Return username part
    }

    public static void main(String[] args) {
        String email = "john.doe@example.com";
        String username = getUsername(email);
        System.out.println(username);      // Output: john.doe
    }
}
```

**Explanation:**

* The method extracts the part of the string before `@`.
* It returns a new `String` object.
* The caller stores this in `username` and uses it as needed.

---

### **5️⃣ Summary of Object Passing**

1. Objects are **passed by reference value** → method receives a copy of the reference.
2. Modifications inside the method **affect the original object** in the heap.
3. Returning objects allows methods to **produce reusable results**.
4. Primitives behave differently → they are copied, not references.


---

# **Parameter Passing in Java — Structured Learning Material**

## **1. Learning Objectives**

By the end of this lesson, you will be able to:

* Understand how **method calls** work in Java.
* Distinguish between **caller**, **called method**, and **parameters**.
* Differentiate **actual parameters** vs **formal parameters**.
* Explain how **parameter passing** works for **primitive types** and **object references**.
* Correctly state Java’s parameter passing model (what it *really* is).
* Avoid the common confusion about *call by value* vs *call by reference*.

---

## **2. Key Concepts (with clear definitions)**

### ✓ **Caller**

The method that *invokes* another method.
Example: `main()` calling `add()` → `main` is the caller.

### ✓ **Called Method / Called Function**

The method that gets invoked.
Example: `add()` is the called/target method.

### ✓ **Actual Parameters (Arguments)**

Values passed during the method call.
Example: `add(a, b)` → `a` and `b` are actual parameters.

### ✓ **Formal Parameters**

Variables in the method definition that receive the values.
Example: `add(int x, int y)` → `x` and `y` are formal parameters.

### ✓ **Return Value (Output)**

The value a method sends back after finishing execution.

### ✓ **Java Parameter Passing Model**

Java uses **only one** parameter passing mechanism:

> **Java is strictly *pass-by-value*.**

But what is “value”?

* For primitives → the *actual data*
* For objects → the *reference (address)* to the object


---

## **3. Detailed Breakdown of the Transcript Content**

### **A. Parameter Passing with Primitive Data Types**

Example:

```
int a = 10;
int b = 5;
int c = add(a, b);
```

Method:

```
int add(int x, int y) {
    return x + y;
}
```

#### What happens?

* `b` (value 5) is copied into `y`
* `a` (value 10) is copied into `x`

So:

* `x = 10`
* `y = 5`

Java creates **new independent variables** `x` and `y` inside the method.
Then it computes `x + y = 15` and returns it.

#### Key Point:

> For primitives: **values are copied**.

Diagram (simplified):

```
main:      a → 10
           b → 5

add():     x → 10 (copy)
           y → 5 (copy)
```

---

### **B. Parameter Passing with Objects (Reference Types)**

Example:

```
String name = "Victor";
welcome(name);
```

Method:

```
void welcome(String n) {
    System.out.println("Welcome " + n);
}
```

#### What happens?

* `name` contains a *reference* (address) to the string `"Victor"`
* That reference (not the object) is copied into `n`

So:

* Both `name` and `n` refer to the **same String object**

Diagram:

```
name ─────────┐
              │
              ▼
         "Victor" (object)

n ────────────┘  (same reference copied)
```

Note:

* Java does **not** create a new `"Victor"` object.
* Only the reference is copied.

#### Key Point:

> For objects: **the reference (address) value is copied**, not the object itself.

---

### **C. Why People Get Confused: "Call by Value" vs "Call by Reference"**

Some people (especially from C/C++ background) describe it like this:

* **Primitives → Passed by Value**
* **Objects → Passed by Reference**

**This is incorrect in Java.**

### The truth:

> Java is 100% *call-by-value*.
> What gets passed for objects is the *value of the reference*.

So:

* You cannot change which object the caller’s variable refers to.
* But you *can modify the internals* of the object if it is mutable.

---

## **4. Summary**

* Methods have **actual parameters** at call site and **formal parameters** in definitions.
* Java uses **only one parameter passing mechanism**.
* That mechanism is **pass-by-value**.
* For primitives, the value is the *data*.
* For objects, the value is the *reference* (address).
* The object itself is *not* copied during method call.

---

## **5. Practical Applications**

* When debugging, always remember variables inside a method are **separate copies**.
* If you want to modify an object inside a method:

  * It must be mutable.
  * You must modify its internal fields.
* If you want to reassign an object for the caller:

  * You cannot (because reference copies are local).
  * You must return the new object or use wrappers.

---

## **6. Self-Assessment Questions**

1. What is the difference between **actual** and **formal** parameters?
2. When you pass a primitive to a method, what exactly gets copied?
3. When you pass an object to a method, what exactly gets copied?
4. Why is Java considered strictly *pass-by-value*?
5. Can a method change what object a caller's reference variable points to? Why or why not?
6. What happens if you modify the object’s internal state inside the method?

---



```java 
package scmethod1;

public class SCMethod1 
{
    
  int gcd(int m,int n)
  {
    while(m!=n)
    {
      if(m>n)m=m-n;
      else n=n-m;
    }
    return m;
  }
          
  public static void main(String[] args) 
  {
    SCMethod1 x=new SCMethod1();
    System.out.println(x.gcd(35,56));
  } 
              
  static boolean isPrime(int n)
  {
    for(int i=2;i<n/2;i++)
    {
      if(n%i==0)
          return false;
    }
    return true;      
  }
}
```
---

# **📘Method Overloading in Java — Complete Learning Material**

## **1. Learning Objectives**

After this lesson, you will be able to:

* Understand what **method overloading** is in Java.
* Identify the **two rules** that allow methods to be overloaded.
* Recognize what *cannot* be overloaded.
* Predict which overloaded method will be called in a given situation.
* Understand how the compiler selects the correct overloaded method.

---

## **2. What is Method Overloading?**

**Method Overloading** means:

> Defining **multiple methods** with the **same method name**, but with **different parameter lists**.

Java allows this because sometimes you want one “concept” (like finding max) to work with different inputs.

---

## **3. Example: Finding Maximum of Numbers**

### **A. First method: Maximum of two integers**

```java
int max(int x, int y) {
    return (x > y) ? x : y;
}
```

This method returns the greater of two `int` values.

---

### **B. Second method: Maximum of two floats**

```java
float max(float x, float y) {
    return (x > y) ? x : y;
}
```

Now the method has:

* The **same name**: `max`
* **Different parameter types**: `float, float`

So overloading is allowed.

---

### **C. Third method: Maximum of three integers**

```java
int max(int x, int y, int z) {
    int temp = (x > y) ? x : y;
    return (temp > z) ? temp : z;
}
```

This differs by:

* **Number of parameters** (3 instead of 2)

So this is also valid overloading.

---

# **4. Overloading Rules (Very Important)**

### A method can be overloaded if:

### **✔ Rule 1 — Number of parameters is different**

Example:

* `max(int, int)`
* `max(int, int, int)`

### **✔ Rule 2 — Parameter types are different**

Example:

* `max(int, int)`
* `max(float, float)`

### Java uses the **method signature** to distinguish overloaded methods:

> **Method name + parameter list**
> (return type is NOT part of signature)

---

# **5. What is *NOT* Allowed?**

You CANNOT overload by:

### ✘ Only changing return type

Example:
`int max(int x, int y)`
`float max(int x, int y)`
❌ ERROR (same parameter list → same method signature)

### ✘ Only changing variable names

`max(int a, int b)`
`max(int x, int y)`
❌ ERROR (parameter list is same → duplicate definition)

---

## **6. How the Compiler Chooses the Correct Overloaded Method**

### Case 1 — Two integers

```java
max(15, 10);   // integers
```

Compiler picks:

```
max(int, int)
```

### Case 2 — Two floats

```java
max(5F, 7F);
```

* `5F` and `7F` are float literals
  Compiler picks:

```
max(float, float)
```

### Case 3 — Three integers

```java
max(8, 10, 3);
```

Compiler picks:

```
max(int, int, int)
```

### **Important:**

The compiler always chooses the method whose **parameter types exactly match** the arguments passed.

---

## **7. Summary**

* **Method Overloading** = multiple methods with the same name and different parameter lists.
* Allowed differences:

  * number of parameters
  * parameter data types
  * (order also matters)
* Not allowed:

  * return type difference alone
  * parameter name difference alone
* Compiler chooses the appropriate method based on the **type and number of arguments**.

---

## **8. Self-Assessment Questions**

1. What is method overloading?
2. Can two overloaded methods have the same number of parameters?
3. Can we overload a method by changing only the return type? Why not?
4. What will happen when you call `max(3, 5F)`? Which overload will be picked?
5. What is the difference between method overloading and method overriding?

---

# **Recursion in Java — Complete Learning Material**

## **1. What You Will Learn**
- What recursion is  
- How recursive methods work internally (call stack mechanics)  
- Forward vs backward recursion  
- Tracing recursive execution  
- Why recursion exists if loops can do the same thing  
- Where recursion is used in real problem solving  
- Practical Java examples  

---

## **2. What Is Recursion?**

**Recursion** means:

> A method calling *itself* repeatedly until a stopping condition is met.

Example idea:
A method `fun(n)` prints `n`, then calls `fun(n - 1)`, which again prints the next value, and so on.

A recursive method **must** have:

1. **Base Case** → the condition that stops recursion  
2. **Recursive Call** → the method calling itself

---

## **3. Example 1 — Forward Recursion (Print Before Calling)**

```java
void fun(int n) {
  if (n > 0) {
    System.out.println(n);  
    fun(n - 1);
  }
}
```

### **If we call:**
```java
fun(3);
```

### **Execution Trace**
- `fun(3)`  
  - prints → **3**
  - calls `fun(2)`
- `fun(2)`
  - prints → **2**
  - calls `fun(1)`
- `fun(1)`
  - prints → **1**
  - calls `fun(0)`
- `fun(0)`
  - condition false → stop

### **Output**
```
3
2
1
```

This is a simple **downward recursion**.

---

## **4. How Recursion Works Internally (Call Stack)**

Think of recursion like:

- Stretching a rubber band (going deeper in calls)  
- Releasing it (returning back through previous calls)

Each recursive call **waits** until the next call finishes.

The calls do **not** finish until the deepest call returns.

Example:

`fun(3)` waits for `fun(2)`  
`fun(2)` waits for `fun(1)`  
`fun(1)` waits for `fun(0)`  
`fun(0)` returns → then unwinding starts  
Returning: `fun(1)` → `fun(2)` → `fun(3)`  

---

## **5. Example 2 — Backward Recursion (Call Before Printing)**

```java
void fun(int n) {
  if (n > 0) {
    fun(n - 1);
    System.out.println(n);
  }
}
```

This time:

- First recursive call happens  
- Printing happens *while returning*

### **Trace for `fun(3)`**
- `fun(3)` calls `fun(2)`
- `fun(2)` calls `fun(1)`
- `fun(1)` calls `fun(0)`
- `fun(0)` → stops  
Now returning:
- print **1**
- print **2**
- print **3**

### **Output**
```
1
2
3
```

This shows the power of recursion:  
**What you do after the recursive call happens in reverse order**.

---

## **6. Recursion vs Loops**

### **Loops can do everything recursion does.**
Example using a loop:

```java
for (int i = 3; i >= 1; i--) {
    System.out.println(i);
}
```

### So why use recursion?

Because:

- **Programming is built on mathematics**
- Mathematics describes problems recursively (not with loops)
- Many problems are naturally recursive:
  - Tree traversals  
  - Graph search  
  - Tower of Hanoi  
  - Fibonacci calculations  
  - Divide & Conquer algorithms (Merge sort, Quick sort)

Loops can replicate recursion, but sometimes the recursive version is:

- Cleaner  
- Closer to the mathematical definition  
- Easier to understand conceptually  

### But…

**Recursion uses more memory**  
(since every call creates a new stack frame)

So in programming:

> We use loops when possible  
> We use recursion when necessary

---

## **7. The Base Condition — Why It Matters**

```java
if (n > 0) { … }
```

This is the **base case**.

Without it → infinite recursion → **StackOverflowError**.

Every recursive method needs a well-defined **stopping condition**.

---

## **8. Ready-To-Use Java Demo Code**

### **A) Print 3 2 1**
```java
void fun(int n) {
  if (n > 0) {
    System.out.println(n);
    fun(n - 1);
  }
}

public static void main(String[] args) {
  fun(3);
}
```

### **B) Print 1 2 3**
```java
void fun(int n) {
  if (n > 0) {
    fun(n - 1);
    System.out.println(n);
  }
}
```

---

## **9. Summary**

- Recursion = method calling itself  
- Needs:
  - **Base case**
  - **Recursive step**
- Two patterns:
  - **Forward recursion** → print, then call  
  - **Backward recursion** → call, then print  
- Loops can replace recursion  
- Recursion is essential in mathematics, tree problems, divide & conquer  
- Should be used when it simplifies problem-solving  

---

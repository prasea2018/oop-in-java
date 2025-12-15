# **📘 Learning Module: Java Output & println() Behavior**

---

## **1. Learning Objectives**

By the end of this lesson, you will be able to:

1. Understand the purpose of **System.out** and how Java prints data to the console.
2. Differentiate between `print()`, `println()`, and `printf()`.
3. Explain **method overloading** in the context of `print()` and `println()`.
4. Predict how Java handles **expressions** and **concatenation** inside `println()`.
5. Identify and avoid common mistakes with the **+ operator**.
6. Construct meaningful formatted print statements in Java.

---

## **2. Conceptual Breakdown (Cleaned & Structured)**

### **A. System.out and the Printing Mechanism**

* Java provides a built-in class called **System**.
* Inside it, there is a **static object** called `out`.
* `out` is an instance of **PrintStream**.
* `System.out` is connected to the **standard output** (the monitor/console).
* Because `out` is static, we access it using `System.out`.

---

## **B. Printing Methods in PrintStream**

`System.out` provides several methods for printing:

| Method      | Behavior                             |
| ----------- | ------------------------------------ |
| `print()`   | Prints without a newline             |
| `println()` | Prints and moves cursor to next line |
| `printf()`  | C-style formatted output             |
| `format()`  | Formatting similar to `printf()`     |

Most commonly used: **`println()`**

---

### **C. Overloaded print() and println() Methods**

Java provides **multiple versions** of `print()` and `println()`, differing by **parameter type**:

Examples:

* `println(int)`
* `println(float)`
* `println(char)`
* `println(String)`
* `println(boolean)`
* `println(double)`
* `println(Object)`

Because they share the same method name but accept different parameters, they are called **overloaded methods**.

---

### **D. Printing Different Data Types**

Given:

```java
int a = 10;
float b = 12.5f;
char c = 'A';
String str = "Hello";
```

The following all work:

```java
System.out.println(a);   // prints 10
System.out.println(b);   // prints 12.5
System.out.println(c);   // prints A
System.out.println(str); // prints Hello
```

Java automatically calls the correct overloaded version.

---

### **E. `println()` With Expressions**

Example:

```java
int x = 10, y = 20;
System.out.println(x + y);
```

Output:

```
30
```

Reason:
`x + y` is an **expression**, evaluated first, then printed.

---

### **F. Common Mistake: Using Comma Inside println()**

Incorrect:

```java
System.out.println(x, y);
```

Reason:
`println()` accepts **only one argument**. No version of `println()` takes two parameters.

Correct approach:

```java
System.out.println("Number is " + y);
```

---

### **G. Concatenation vs Addition: The + Operator**

The **+ operator** can either:

1. **Add numbers**
2. **Concatenate strings**

The behavior depends on the **type of the first operand**.

#### **Case 1: Numbers first → Addition happens first**

```java
System.out.println(x + y + " Sum");
```

Steps:

* `x + y` → 30
* `"30" + " Sum"` → `"30 Sum"`

Output:

```
30 Sum
```

---

#### **Case 2: String first → Everything becomes concatenation**

```java
System.out.println("Sum " + x + y);
```

Steps:

* `"Sum " + x` → `"Sum 10"`
* `"Sum 10" + y` → `"Sum 1020"`

Output:

```
Sum 1020
```

🧠 **Key Rule:**
Once a string appears on the left of `+`, all further `+` operations become string concatenation.

---

#### **Fixing the Problem With Parentheses**

```java
System.out.println("Sum " + (x + y));
```

Now `(x+y)` is evaluated first → 30
Output:

```
Sum 30
```

---

### **H. Building Meaningful Output Messages**

Example goal:

**"Sum of 10 and 20 is 30"**

Correct statement:

```java
System.out.println("Sum of " + x + " and " + y + " is " + (x + y));
```

Output:

```
Sum of 10 and 20 is 30
```

Notice:

* Spaces must be added manually.
* Use parentheses for numeric addition.

---

## **3. Summary**

* `System.out` is a built-in output stream connected to the console.
* `print()` prints without a newline; `println()` prints with one.
* Java provides many overloaded versions of print methods.
* The **+ operator** can act as:

  * Addition (if numbers come first)
  * Concatenation (if a string comes first)
* Use parentheses to force evaluation of numeric expressions.
* Constructing clear output requires careful placing of strings, variables, and spaces.

---

## **4. Practical Application**

✔ Build user-friendly messages in console applications
✔ Debug programs by printing variable states
✔ Prepare readable logs and output
✔ Understand how Java interprets mixed-type expressions
✔ Avoid common pitfalls in concatenation-heavy statements

---

## **5. Self-Assessment Questions**

1. What class does `System.out` belong to?
2. What is the difference between `print()` and `println()`?
3. Why is `System.out.println(a)` able to print both an int and a String?
4. What happens when a string appears before numbers in a `+` expression?
5. Predict the output:

   ```java
   System.out.println(5 + 10 + " value");
   ```
6. Predict the output:

   ```java
   System.out.println("value " + 5 + 10);
   ```
7. Why does `System.out.println(x, y)` cause an error?
8. Write a single println() that outputs:

   ```
   Total of 4 and 6 is 10
   ```

---

# **📘 Learning Module: Java `printf()` and `format()`**

---

## **1. Learning Objectives**

By the end of this lesson, you will be able to:

1. Understand what `printf()` and `format()` do in Java.
2. Use **format specifiers** (`%d`, `%f`, `%c`, `%s`, etc.).
3. Print values in **decimal, octal, and hexadecimal** using conversion codes.
4. Format floating-point numbers in **scientific notation**.
5. Use **argument indexes** (e.g., `%1$d`, `%2$f`) to print values in any order.
6. Understand variable arguments (`...`) in `printf()`.
7. Correctly combine strings and format specifiers to produce structured output.

---

## **2. Detailed Breakdown (Structured Explanation)**

---

### **A. Understanding `printf()` and `format()`**

Java provides:

* `System.out.println()` → Prints text + moves to next line
* `System.out.print()` → Prints text without newline
* **`System.out.printf()`** → Prints text *using formatting rules*
* **`System.out.format()`** → Same as `printf()` (just another name)

`printf()` is similar to C language’s `printf`.
It uses a **format string** + **variable arguments list**.

#### Syntax:

```java
System.out.printf(String format, Object... values);
```

The `...` means **you can pass any number of arguments** (even zero).

---

### **B. The Simplest Example**

```java
System.out.printf("Hello");
```

Output:

```
Hello
```

No newline appears unless you use `\n`:

```java
System.out.printf("Hello\n");
```

---

### **C. Using Format Specifiers**

Format specifiers start with **%** and specify **how to print a value**.

| Specifier    | Meaning             |
| ------------ | ------------------- |
| `%d`         | Integer (decimal)   |
| `%f`         | Float / double      |
| `%c`         | Character           |
| `%s`         | String              |
| `%o`         | Octal               |
| `%x` or `%X` | Hexadecimal         |
| `%e` or `%E` | Scientific notation |

---

### **D. Example With Multiple Variables**

```java
int x = 10;
float y = 12.56f;
char z = 'A';

System.out.printf("Hello %d %f %c\n", x, y, z);
```

Output:

```
Hello 10 12.560000 A
```

✔ Values are inserted into the placeholders in order.

---

### **E. Decimal, Octal, Hexadecimal**

Given:

```java
int x = 10;
```

| Specifier | Output | Meaning               |
| --------- | ------ | --------------------- |
| `%d`      | 10     | decimal               |
| `%o`      | 12     | octal                 |
| `%x`      | a      | hexadecimal           |
| `%X`      | A      | uppercase hexadecimal |

Example:

```java
System.out.printf("%d %o %x\n", x, x, x);
```

---

### **F. Scientific Notation Using `%e`**

Example:

```java
float y = 12.56f;
System.out.printf("%e\n", y);
```

Output (example):

```
1.256000e+01
```

Explanation:

* `1.256000 × 10^1 = 12.56`

Works for both float & double.

For very small numbers:

```java
float y = 0.0012f;
System.out.printf("%e\n", y);
```

Output:

```
1.200000e-03
```

---

### **G. Printing Strings Using `%s`**

```java
String str = "Java Program";
System.out.printf("Hello %s\n", str);
```

Output:

```
Hello Java Program
```

---

### **H. Argument Indexing (Advanced But Powerful)**

Format:

```
%index$specifier
```

Example:

```java
int x = 10;
System.out.printf("%1$d %1$d %1$d\n", x);
```

Output:

``` 
10 10 10
```

Because `%1$d` uses the **first argument** each time.

---

#### **Changing Order of Printing**

Example:

```java
int x = 10;
float y = 12.56f;
String s = "Java";

System.out.printf("%3$s %2$f %1$d\n", x, y, s);
```

Output:

```
Java 12.560000 10
```

✔ Very useful when reusing values
✔ Or printing them in any sequence regardless of argument order.

---

### **I. Why Argument Index Is Useful**

* Reuse the same argument multiple times
* Change the order without changing program logic
* Create complex patterns easily
* Helps in localization (different languages require different word orders)

---

## **3. Summary**

* `printf()` and `format()` provide C-style formatted printing.
* Format specifiers control how each value is printed.
* `%d`, `%f`, `%c`, `%s` are common; `%o`, `%x`, `%e` are advanced.
* Scientific notation uses `%e`.
* Argument index (`%1$d`, `%2$f`) lets you print variables in any order.
* Variable arguments (`...`) let you pass unlimited parameters.

---

# **4. Practical Applications**

- Printing structured tabular data
- Formatting reports, logs, and console UI
- Debugging complex calculations
- Creating multi-language output using argument indexing
- Ensuring numbers appear with consistent formatting

---

# **5. Self-Assessment Questions**

1. What is the difference between `printf()` and `println()`?
2. What does `%d` print?
3. Write a statement that prints an integer in hexadecimal.
4. How do you print a float in scientific notation?
5. What does `%1$d` mean in formatting?
6. Predict the output:

   ```java
   System.out.printf("%2$f %1$d", 10, 12.5f);
   ```
7. Write code to print:

   ```
   Value: 10.56
   ```

   using `printf()`.

---

# ** 📘Java Strings — Complete Lecture Notes**

---


## **1. What Is a String?**

* In Java, **String** is a *built-in class* (in `java.lang` package).
* Although it's a class, it behaves like a **data type** (similar to `int`, `float`, `double`).
* A string is a **collection of characters**—used to store words, sentences, names, etc.

Example:

```java
String str1 = "Java program";
```

### **Important Terminology**

| Term                       | Meaning                                                                |
| -------------------------- | ---------------------------------------------------------------------- |
| **Class (String)**         | Blueprint/type from which objects are made                             |
| **Object (String object)** | Actual data stored in memory                                           |
| **Reference (str1)**       | Variable that *refers to* the object                                   |
| **Literal**                | Fixed constant value written directly in code (e.g., `"Java"` or `10`) |

---

## **2. How Java Stores String Literals in Memory**

When you write:

```java
String str1 = "Java program";
```

* The literal `"Java program"` is stored in the **String Constant Pool (SCP)**.
* `str1` does *not* store the object itself—it stores a **reference** pointing to that pooled object.

Memory model:

```
String Constant Pool
--------------------
"Java program"  <--- str1 points here
```

---

## **3. Ways to Create Strings**

Java provides several constructors for creating `String` objects.

### **Method 1 — Using a String Literal**

```java
String str1 = "Java";
```

* Creates **one object in the String Constant Pool**.
* `str1` refers to the pooled object.

---

### **Method 2 — From a Character Array**

```java
char[] c = { 'A', 'B', 'C', 'D' };
String str1 = new String(c);
```

Memory:

```
Heap:
"ABCD" <--- str1
```

* A **new object is created in the heap** using the characters in the array.

---

### **Method 3 — From a Byte Array**

```java
byte[] b = { 65, 66, 67, 68 };
String str2 = new String(b);
```

* ASCII codes → characters
* `"ABCD"` is created as a **new heap object**.

---

### **Method 4 — Using a String Inside Constructor**

```java
String str3 = new String("Java");
```

⚠️ Critical point: **This creates two objects** (in many cases):

1. `"Java"` literal → **String Pool**
2. `new String("Java")` → **Heap**

So memory has:

```
String Pool:  "Java"
Heap:         "Java" <--- str3
```

---

## **4. String Pool Reuse Behavior**

### **Case 1 — Using the Same Literal Repeatedly**

```java
String s1 = "Java";
String s2 = "Java";
System.out.println(s1 == s2);
```

* Only **one object** in the String Constant Pool.
* Both variables point to the *same pool object*.

```
String Pool:
"Java" <--- s1, s2
```

---

### **Case 2 — Using `new` Keyword**

```java
String s1 = "Java";
String s3 = new String("Java");
System.out.prinln(s1 == s3);
```

* Always creates a **new heap object**, even if the same literal exists in the pool.
* Literal `"Java"` is reused from pool, not recreated.

```
String Pool:
"Java"
Heap:
"Java" <--- s3
```

---

## **5. Why Do Literals Also Take Memory?**

Just like:

```java
int x = 10;
```

* `x` gets 4 bytes.
* The **literal** `10` must also exist in memory during compilation/execution.

Similarly, `"Java"` is a literal → it must occupy memory → stored in **String Constant Pool**.

---

## **6. Summary of All Rules**

### **Rule 1:**

Literal assignment → object in **String Constant Pool**

### **Rule 2:**

`new String()` → always creates a **new object in Heap**

### **Rule 3:**

If the literal already exists in pool → **reuse** it

### **Rule 4:**

Using `new` + literal → may require two objects
(heap + pool)

---

## **7. Why Java Uses the String Pool?**

Because strings are:

* very commonly used
* immutable
* expensive to create repeatedly

So the pool helps in:

* memory optimization
* faster access
* reducing duplicate string objects

---

## **8. What We Will See in the Next Lecture**

➡️ Important **String methods** (`length()`, `charAt()`, `equals()`, `substring()`, etc.)

---

# **📘 Java String Class – Methods (Lecture Notes)**

---


### **1. Introduction**

* `String` is a **built-in class** in Java.
* String objects are **immutable** → once created, their contents **cannot be changed**.
* Any operation that *seems* to modify a string actually **creates a new String object**.

---

#### **2. Example String**

```java
String str = "Java";
```

* `"Java"` is a **string literal**.
* Since no `new` keyword is used, Java stores it in the **String Constant Pool**, not the heap.
* `str` is a **reference variable** pointing to that pool object.

---

### **3. Important String Methods**

---

#### **3.1 `length()`**

Returns the number of characters in a string.

```java
int l = str.length();   // l = 4
```

---

#### **3.2 `toLowerCase()` and `toUpperCase()`**

Used to convert the case of letters in a string.

##### Important:

* Does *not* modify the original string.
* **Creates a new String object** in the heap.

Example:

```java
String str = "Java";
String str1 = str.toLowerCase();  
```

Memory behavior:

* Original `"Java"` remains unchanged in the pool.
* New object `"java"` is created in the heap → `str1` points to it.

If you write:

```java
str = str.toLowerCase();
```

* A new `"java"` object is created.
* `str` now points to the **new** object, not the old pool literal.

---

#### **3.3 `trim()`**

Removes leading and trailing spaces.

Example:

```java
String str = "   welcome   ";
str = str.trim();  
```

Result:

* `"welcome"` (no spaces)
* New object created — original is not modified.

Usage:

* Very useful when taking user input.
* Removes accidental spaces from keyboard input.

---

#### **3.4 `substring()`**

Extracts a portion of a string and **returns a new string**.

##### **Version 1:** `substring(startIndex)`

Extracts from `startIndex` to the end.

```java
String str = "Welcome";
String sub = str.substring(3);
```

Example with `"welcome"`:

Indices:
`w(0) e(1) l(2) c(3) o(4) m(5) e(6)`

`str.substring(3)` → `"come"`

---

##### **Version 2:** `substring(startIndex, endIndex)`

* Extracts from `startIndex` **up to endIndex-1**.
* `endIndex` is exclusive.

Example:

```java
String sub = str.substring(3, 6);
```

Extracts:

* characters at index 3, 4, 5 → `"com"`

---

#### **3.5 `replace(oldChar, newChar)`**

Replaces all occurrences of one character with another.

Example:

```java
String str = "welcome";
str = str.replace('e', 'k');
```

Result:

* `"wklcomk"`
  All 'e' characters are replaced.

Again:

* Original string unchanged
* New string returned



### **3.6 `startsWith(String prefix)`**

#### **Checking the Start or End of a String**

Useful for:

* URLs
* Names
* Email domains
* File extensions


Returns **true/false**.

```java
str.startsWith("www");   // Check if URL starts with www
str.startsWith("https"); // Check if URL is secure
str.startsWith("Mr.");   // Title check
```

### **3.7 `endsWith(String suffix)`**

```java
str.endsWith(".org");   // Organization site
str.endsWith(".com");   // Commercial site
str.endsWith(".gov");   // Government site
```

---

### **3.8 Getting a Character — `charAt(int index)`**

```java
String str = "welcome";
char c = str.charAt(6);
```

Example:
`"welcome".charAt(6)` → `'c'`

---

### **Searching in Strings**

Two powerful search methods:

---

### **3.9 `indexOf()` — Search Left → Right**

#### **Find character or string**

```java
str.indexOf('.');
str.indexOf("ab");
```

#### **Find with starting position**

```java
str.indexOf('.', 4);  // Start searching from index 4
```

#### **If not found**

Returns **-1**

```java
str.indexOf('?'); // returns -1
```

---

### **3.10 `lastIndexOf()` — Search Right → Left**

```java
str.lastIndexOf('.');
```

#### **Specify starting position**

```java
str.lastIndexOf('.', 7);  // Search backward from index 7
```

### **If not found**

Returns **-1**

---

### **4. Key Concept: Immutability**

**Strings are immutable in Java.**
Any modifying method (trim, replace, substring, toLowerCase, toUpperCase) will:

1. Take the current string
2. Create a **new String object** with the modification
3. Return the new object
4. You must store it somewhere if you want to use it

Example:

```java
str = str.replace('a', 'b');
```

If you **don’t** assign the result, the change is lost.

---

#### **5. Methods Covered So Far**

* **Strings are immutable** → operations create **new objects**.
* `length()` → size
* `toLowerCase()`, `toUpperCase()` → case change
* `trim()` → remove outer spaces
* `substring()` → extract part of string
* `replace()` → replace characters
* `startsWith()` / `endsWith()` → check patterns
* `charAt()` → get single character
* `indexOf()` / `lastIndexOf()` → search characters/strings

---

### 🛠️ **Practical Applications**

You can use these methods for:

* Validating URLs
* Checking email domain (`endsWith("@gmail.com")`)
* Parsing file names
* Cleaning user input (`trim()`, `toLowerCase()`)
* Extracting first/last names
* Data validation and preprocessing
* Keyword searching within text

---

## 📝 **Self-Assessment Questions**

Test your understanding:

### **1. Conceptual**

1. Why are strings in Java immutable?
2. What is the difference between String Constant Pool and Heap?

### **2. Method Behavior**

3. What does `substring(2, 5)` return?
4. What is returned when `indexOf()` cannot find a character?

### **3. Code Output**

5. What is the output?

   ```java
   String s = "Hello World";
   System.out.println(s.trim().substring(0, 5).toUpperCase());
   ```

6. What does this return?

   ```java
   "programming".lastIndexOf('g', 3)
   ```

### **4. Practical**

7. How would you check if a URL uses HTTPS?
8. How do you remove extra spaces before/after a username?

---

#  **Learning Module: String Comparison & Conversion Methods in Java**

---


## **1. Learning Objectives**

By the end of this lesson, you will be able to:

* Understand and apply key Java String methods:

  * `equals()`
  * `equalsIgnoreCase()`
  * `compareTo()`
  * `valueOf()`
* Distinguish between **content comparison** and **reference comparison** (`==`)
* Explain how String literals and `new String()` differ in memory (String Pool vs Heap)
* Interpret dictionary (lexicographical) order comparison rules
* Predict return values of `compareTo()` (−1, 0, +1)
* Convert primitive values into Strings using `String.valueOf()`

---

## **2. Detailed Breakdown**

### ✅ **A. equals(String s)**

**Purpose:** Checks whether two strings have *exactly the same* characters (case-sensitive).

### How it works:

```java
String str1 = "JAVA"; 
String str2 = "java"; 
String str3 = "python";
String str4 = "python";
str3.equals(str4); //true
str1.equals(str2); // false
```

If:

* Characters match
* Case matches
* No extra spaces

Then → returns **true**.


---

### ✅ **B. equalsIgnoreCase(String s)**

**Purpose:** Compares strings while **ignoring letter case**.

```java
str1.equalsIgnoreCase(str2);
```

Example:

```java
"JAVA".equalsIgnoreCase("java"); // true
```

---

### ✅ **C. compareTo(String s)**

**Purpose:** Compares two strings in **dictionary (lexicographical) order**.

### Return Values:

* **0** → both strings are exactly equal
* **−1** → first string comes first in dictionary
* **+1** → first string comes later in dictionary

#### Example 1:

```java
String str2 = "java";
String str3 = "python";
str2.compareTo(str3); // "java" vs "python"
str3.compareTo(str2); // "python" vs "java"
```

* "java" comes before "python"
  → returns **−1**

* "python" comes after "java"
  → returns **+1**

### Important detail:

Uppercase letters have **smaller ASCII values** than lowercase letters.

* 'A' to 'Z' → 65 to 90
* 'a' to 'z' → 97 to 122

So `"JAVA"` is considered **smaller** than `"java"`.

---

### ⚡ **D. The Big Difference: equals() vs ==**

#### `equals()`

* Compares **content**
* Correct way to compare Strings

#### `==`

* Compares **references** (memory addresses)
* Checks if both variables point to the **same object**

### Example:

```java
String str1 = "java";
String str2 = "java";   // same literal → stored in String Pool
str1 == str2; // true
```

#### But with `new`:

```java
String str3 = new String("java");
```

Now:

```java
str1.equals(str3); // true  (content same)
str1 == str3;      // false (different objects)
```

**Reason:**

* String literals → stored in **String Pool**
* `new String()` → stored in **Heap**

---

### ✅ **E. valueOf(int i)**

**Purpose:** Converts any primitive type → String.

```java
String s1 = String.valueOf(10);      // "10"
String s2 = String.valueOf(3.14);    // "3.14"
String s3 = String.valueOf(true);    // "true"
```

Useful for:

* Printing mixed data
* UI display
* Logging
* String concatenation

---

## **3. Summary**

| Method               | Purpose                      | Case-sensitive? | Returns    |
| -------------------- | ---------------------------- | --------------- | ---------- |
| `equals()`           | Check exact content equality | Yes             | true/false |
| `equalsIgnoreCase()` | Check content ignoring case  | No              | true/false |
| `compareTo()`        | Dictionary comparison        | Yes             | -1/0/1     |
| `==`                 | Compare memory references    | N/A             | true/false |
| `valueOf()`          | Convert value → string       | N/A             | string     |

Important concepts:

* String Pool vs Heap memory
* Uppercase < lowercase (ASCII values)
* Use `equals()` instead of `==` for accurate string comparison

---

## **4. Application (Practical Use Cases)**

### ✔ Validating user input:

```java
if (userRole.equalsIgnoreCase("admin")) { ... }
```

### ✔ Sorting names alphabetically:

```java
names.sort((a, b) -> a.compareTo(b));
```

### ✔ Case-insensitive login:

```java
username.equalsIgnoreCase(storedUsername);
```

### ✔ Building messages:

```java
String msg = "Your score is " + String.valueOf(score);
```

---

## **5. Self-Assessment Questions**

### **Conceptual**

1. What is the difference between `equals()` and `==`?
2. Why does `"JAVA".compareTo("java")` return −1?
3. What does `compareTo()` return when two strings are identical?
4. Why is a string created using `new String("text")` stored in the heap?

### **Predict Output**

Write the expected output:

1.

```java
"Cat".equalsIgnoreCase("cAt")
```

2.

```java
"apple".compareTo("banana")
```

3.

```java
String a = "hello";
String b = new String("hello");
a == b;
```

4.

```java
String.valueOf(25.6)
```

---
